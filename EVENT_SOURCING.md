# Event Sourcing

Event sourcing is a pattern in software artchitecture where application state changes are captured as a sequence of events. Here's a simple explanation:

1. Instead of storing just the current state (like in a database), the application stores a log of all state changes that occured over time.
2. These state changes are stored as a sequence of immutable events.
3. The current application state can reconstructed by replaying the stored events.
4. New events are continuously added to the event log as more state changes occur.

## Key benefits
- Provides a complete audit trail of all state changes over time.
- Enables reconstructing past application states for debugging or auditing.
- Supports temporal queries on historic data.
- Facilitates event-driven architectures and reactive systems.

Event sourcing is commonly used in domains with complex business rules, audit requirements, or where reconstructing historical data is important. However, it can add complixity compared to traditional state-based persistence.