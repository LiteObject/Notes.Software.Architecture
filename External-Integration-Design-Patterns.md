# Design Patterns and Best Practices for External Libraries and Integrations

The core principle is: **treat external libraries and systems as volatile details, not as part of your domain model**.

Your application should depend on *your own stable abstractions*, while the external system sits behind a boundary that can be replaced, upgraded, mocked, or adapted later.

## Key Patterns

These patterns overlap, but they solve slightly different problems:

- **Adapter**: converts one API shape into another shape your code prefers.
- **Facade**: exposes a smaller, simpler API over a large or awkward library.
- **Ports and Adapters**: makes your business logic depend on internal interfaces instead of external implementations.
- **Anti-Corruption Layer**: translates external concepts, terminology, and data models into your domain model.

In practice, a single integration boundary may use several of these patterns together.

### When to Use Each Pattern

| Pattern | Use It When | Common Use Cases | How It Is Different |
| --- | --- | --- | --- |
| Adapter | The external API shape does not match the way your application wants to call it. | Wrapping an SDK, converting a third-party client call into a domain-friendly method, hiding vendor-specific request objects. | Focuses on translating one interface into another. It is usually narrower than a facade and less architectural than ports and adapters. |
| Ports and Adapters / Hexagonal Architecture | You want business logic to depend on your own interfaces instead of external systems, frameworks, databases, or vendors. | Payment processing, email sending, file storage, search indexing, identity providers, message buses. | Defines the architectural dependency direction: the domain owns the port, and external systems implement adapters. |
| Facade | A library or system has a large, complex, or low-level API, and most callers only need a small set of operations. | Simplifying cloud storage SDKs, reporting libraries, analytics clients, document generation tools, complex vendor SDKs. | Focuses on reducing and simplifying an API surface. It may still use adapters or mappers underneath. |
| Anti-Corruption Layer | The external system has different terminology, data structures, business rules, or lifecycle concepts than your domain. | Integrating with legacy systems, ERPs, CRMs, billing platforms, vendor APIs with awkward or incompatible models. | Focuses on semantic translation, not just method signatures. It protects your domain model from foreign concepts. |
| Repository / Gateway | You need a named boundary for a specific external capability or data source. | UserRepository for persistence, EmailGateway for email, SearchIndexGateway for search, MessageBus for queues, IdentityProvider for auth. | Gives a specific external dependency a clear role. Repositories usually represent data collections; gateways usually represent external services or capabilities. |
| Strategy | The behavior may vary by provider, tenant, region, feature flag, environment, or business rule. | Choosing tax providers by region, payment providers by market, shipping calculators by carrier, AI models by workload, notification channels by user preference. | Focuses on selecting among interchangeable behaviors. It is useful after you already have a stable abstraction to switch behind. |

Use this quick decision guide:

- If the problem is **API shape mismatch**, use an **Adapter**.
- If the problem is **dependency direction**, use **Ports and Adapters**.
- If the problem is **too much API surface**, use a **Facade**.
- If the problem is **foreign domain concepts leaking in**, use an **Anti-Corruption Layer**.
- If the problem is **a named integration boundary**, use a **Repository or Gateway**.
- If the problem is **choosing among interchangeable implementations**, use a **Strategy**.

### 1. Adapter Pattern

Wrap the external library/system in your own interface.

Instead of this throughout the codebase:

```ts
stripeClient.customers.create(...)
```

Prefer this:

```ts
paymentService.createCustomer(...)
```

Where `paymentService` is your abstraction and Stripe is only one implementation.

This makes it easier to replace Stripe, upgrade its SDK, fake it in tests, or add logging/retry behavior in one place.

### 2. Ports and Adapters / Hexagonal Architecture

Define a "port" inside your application:

```ts
interface PaymentGateway {
  charge(request: ChargeRequest): Promise<ChargeResult>;
}
```

Then implement it externally:

```ts
class StripePaymentGateway implements PaymentGateway {
  async charge(request: ChargeRequest): Promise<ChargeResult> {
    // Stripe-specific code here
  }
}
```

Your business logic depends on `PaymentGateway`, not Stripe.

### 3. Facade Pattern

If a library has a large or awkward API, expose only the operations your application actually needs.

```ts
interface DocumentStorage {
  uploadInvoice(invoice: InvoiceDocument): Promise<DocumentId>;
  getSignedDownloadUrl(documentId: DocumentId): Promise<string>;
  deleteDocument(documentId: DocumentId): Promise<void>;
}
```

This prevents the rest of your codebase from learning the library's full API surface.

### 4. Anti-Corruption Layer

When integrating with an external system that has different concepts, naming, data shapes, or lifecycle rules, translate at the boundary.

Do not let external DTOs leak into your domain.

```ts
// External API response
VendorCustomerResponse

// Internal domain model
Customer
```

Use mappers:

```ts
function mapVendorCustomerToCustomer(response: VendorCustomerResponse): Customer {
  return {
    id: response.customer_id,
    email: response.contact.email_address,
    status: mapStatus(response.account_state)
  };
}
```

This protects your system from vendor-specific terminology and weirdness.

### 5. Repository / Gateway Pattern

For persistence, APIs, queues, caches, search engines, and external services, create dedicated gateways:

```ts
UserRepository
EmailGateway
SearchIndexGateway
MessageBus
FeatureFlagClient
IdentityProvider
```

These abstractions clarify intent and keep integration details contained.

### 6. Strategy Pattern

Use this when you may need multiple providers or algorithms.

```ts
interface TaxCalculator {
  calculate(order: Order): TaxAmount;
}
```

Implementations might be:

```ts
AvalaraTaxCalculator
InternalTaxCalculator
NoOpTaxCalculator
```

This is useful when vendors vary by region, customer, environment, feature flag, or pricing tier.

## Best Practices

### 1. Keep External Types at the Boundary

Avoid passing SDK classes, raw JSON responses, vendor enums, or generated API models deep into your application.

Good:

```
OrderService -> PaymentGateway -> Stripe SDK
```

Risky:

```
OrderService -> StripeCustomer -> StripeCharge -> StripeWebhookEvent
```

In the risky example, Stripe-specific types have leaked through multiple layers of the application. That makes later changes to Stripe SDK versions, payment providers, or webhook formats much more expensive.

### 2. Own Your Interfaces

Do not mirror the vendor API exactly. Design your interface around what your application needs.

Bad abstraction:

```ts
createStripePaymentIntent(...)
```

Better abstraction:

```ts
authorizePayment(...)
capturePayment(...)
refundPayment(...)
```

Name things in your domain language, not the vendor's language.

### 3. Use Dependency Injection and a Composition Root

Make integrations explicit dependencies. Business services should receive abstractions through constructors or function parameters, not instantiate SDK clients directly.

Good:

```ts
class CheckoutService {
  constructor(private readonly paymentGateway: PaymentGateway) {}
}
```

Risky:

```ts
class CheckoutService {
  private readonly stripe = new StripeClient(...);
}
```

Create and wire the concrete adapter in one place, often called the composition root. This keeps provider selection, credentials, timeouts, and environment-specific setup out of business logic.

### 4. Centralize Configuration

Keep API keys, URLs, timeouts, retry settings, feature flags, and provider selection in configuration.

Avoid scattering vendor setup throughout the codebase.

### 5. Handle Failure Explicitly

External systems fail. Design for:

- Timeouts
- Retries with backoff
- Rate limits
- Partial failures
- Duplicate requests
- Network errors
- Authentication failures
- Vendor downtime

Use patterns like:

- Circuit breaker
- Retry policy
- Bulkhead isolation
- Dead-letter queue
- Idempotency keys

### 6. Make Operations Idempotent Where Possible

If a request might be retried, make sure it does not accidentally create duplicates or charge twice.

For example:

```ts
paymentGateway.charge(orderId, amount, idempotencyKey)
```

### 7. Normalize Errors

Do not let every caller handle vendor-specific exceptions.

Instead of exposing:

```ts
StripeCardError
StripeRateLimitError
AxiosError
```

Map them to your own errors:

```ts
PaymentDeclinedError
ExternalServiceUnavailableError
ExternalRateLimitError
```

### 8. Add Observability at the Boundary

The adapter or gateway is the natural place to measure and diagnose external behavior.

Capture:

- Request counts
- Latency
- Error rates
- Timeout rates
- Retry counts
- Rate-limit responses
- Circuit breaker state
- Correlation IDs or trace IDs

Use structured logs and distributed tracing around outbound calls. Avoid logging secrets, tokens, full payment details, or sensitive user data.

### 9. Treat Security as Part of the Boundary

External integrations often handle credentials, tokens, customer data, and vendor callbacks. Keep security decisions close to the integration boundary.

Best practices:

- Store secrets in a secret manager or secure environment configuration.
- Rotate credentials without code changes.
- Use least-privilege credentials per integration.
- Validate and sanitize data entering from external systems.
- Verify webhook signatures before processing payloads.
- Avoid logging sensitive payloads, tokens, credentials, or personally identifiable information.
- Make authentication and authorization failures explicit error cases.

### 10. Design Async and Event Integrations Deliberately

Webhooks, queues, message buses, and event subscriptions have different failure modes than synchronous API calls.

Plan for:

- Duplicate delivery
- Out-of-order events
- Replay behavior
- Poison messages
- Dead-letter queues
- Signature verification
- Event schema changes
- Idempotent event handlers

Translate external events into internal domain events before publishing them deeper into your application.

```ts
function handleStripeWebhook(event: StripeWebhookEvent): Promise<void> {
  const domainEvent = mapStripeEventToPaymentEvent(event);
  return paymentEventHandler.handle(domainEvent);
}
```

### 11. Version Your Integration Boundary

If the external API changes significantly, preserve compatibility inside your application by versioning the mapper, request/response contracts, or adapter behavior.

```ts
StripePaymentMapperV1
StripePaymentMapperV2
```

Versioning the whole adapter can be useful during a migration, but it is often enough to isolate version-specific mapping code. The goal is to keep the rest of the application stable while the external contract changes.

### 12. Manage Data Contracts and Schema Evolution

Treat external data contracts with the same care you would give your own APIs.

Prefer:

- Explicit request and response models
- Tolerant readers for additive fields
- Strict handling for required fields
- Contract tests for important workflows
- Consumer-driven contracts when multiple internal services depend on the same integration
- Schema validation at the boundary for incoming external data

Do not assume vendor payloads are stable forever. Make additive changes easy and breaking changes visible.

### 13. Test Against Your Abstractions

Your business logic should be testable without the external system.

Use:

- Unit tests with fake adapters
- Contract tests for your integration boundary
- Integration tests against sandbox/test environments
- Recorded fixtures where appropriate
- End-to-end tests only for critical flows

Run contract or integration tests against the real vendor sandbox periodically. Otherwise, mocks and recorded fixtures can drift away from actual vendor behavior.

### 14. Use Caching Intentionally

Caching can reduce latency, cost, and rate-limit pressure, but it also introduces freshness and invalidation concerns.

Cache only when you understand:

- How stale the data may be
- How cache keys are constructed
- How invalidation works
- Whether responses are user-specific or permission-sensitive
- Whether cached data contains sensitive information
- How vendor rate limits or costs influence cache duration

Keep caching policy near the integration boundary so callers do not need to understand vendor-specific performance limits.

### 15. Track Cost, Quotas, and Rate Limits

Many external systems have usage-based billing, quotas, or throttling rules. This is especially important for payment providers, search APIs, geocoding services, messaging systems, and AI/LLM APIs.

Design for:

- Rate-limit handling
- Backoff and retry budgets
- Per-customer or per-tenant usage limits
- Alerts for quota exhaustion
- Cost visibility by operation or workflow
- Graceful degradation when a vendor limit is reached

### 16. Avoid Premature Generic Abstractions

Do not build a universal provider system unless you need one. Start with a simple boundary.

Good first step:

```ts
EmailSender
```

Only later, if needed:

```ts
SendGridEmailSender
SesEmailSender
MailgunEmailSender
```

Always wrap the external boundary, but do not generalize across providers until you have a real second provider or a clear migration need. Flexibility comes from a clean boundary, not from making everything overly configurable on day one.

### 17. Document the Boundary

For every external integration, document:

- What the external system does
- Where the adapter lives
- What internal abstraction owns it
- Expected failure modes
- Retry/idempotency behavior
- Test strategy
- Operational dashboards/logs
- Vendor-specific assumptions
- Security and secret-management assumptions
- Cost, quota, and rate-limit assumptions

## A Good Mental Model

Ask yourself:

> "If we replaced this vendor or upgraded this library tomorrow, how much of the codebase would need to know?"

The ideal answer is:

> "Only the adapter, mapper, configuration, observability, security settings, and tests around that boundary."

That is the design you want.
