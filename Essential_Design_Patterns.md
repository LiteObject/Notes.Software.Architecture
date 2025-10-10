# Essential Design Patterns

## **Creational Patterns** (Object Creation)

1. **Singleton** - Ensures a class has only one instance with global access
2. **Factory Method** - Creates objects without naming the exact class up front
3. **Abstract Factory** - Creates families of related objects
4. **Builder** - Constructs complex objects step by step
5. **Prototype** - Creates new objects by cloning existing ones

## **Structural Patterns** (Object Composition)

6. **Adapter** - Makes incompatible interfaces work together (like a plug adapter)
7. **Decorator** - Adds new functionality to objects dynamically without changing the original
8. **Facade** - Provides a simplified interface to complex subsystems (a single front door)
9. **Proxy** - Controls access to objects, acting as a lightweight stand-in
10. **Composite** - Treats individual objects and groups the same way (tree structures)
11. **Bridge** - Separates abstraction from implementation so each can change independently
12. **Flyweight** - Shares intrinsic state (common, reusable data) between similar objects to minimize memory usage

## **Behavioral Patterns** (Object Interaction & Responsibility)

13. **Strategy** - Encapsulates algorithms and makes them interchangeable at runtime
14. **Observer** - Notifies multiple objects about state changes (classic pub/sub)
15. **Command** - Encapsulates requests as objects so they can be queued, logged, or retried
16. **Template Method** - Defines algorithm skeleton, lets subclasses override steps with their own details
17. **Iterator** - Provides sequential access to elements without exposing underlying structure
18. **State** - Alters object behavior when internal state changes (same object, new behavior)
19. **Chain of Responsibility** - Passes requests along a chain of handlers until one handles it
20. **Mediator** - Reduces coupling by centralizing communication between objects
21. **Memento** - Captures and restores object state without exposing internals
22. **Visitor** - Separates algorithms from objects they operate on by moving logic into a visitor

## **Architectural Patterns** (System-Level)

23. **MVC (Model-View-Controller)** - Separates data, UI, and logic
24. **MVVM (Model-View-ViewModel)** - Variation of MVC for data binding
25. **Repository** - Abstracts data access layer
26. **Dependency Injection** - Design principle that inverts control of object creation and wiring (objects receive what they need)
27. **Service Layer** - Delimits business logic boundaries and coordinates application operations (defines clear use cases)

## **Key Principles to Understand**

Along with patterns, master these foundational principles:
- **SOLID** principles (Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, Dependency Inversion)
- **DRY** (Don't Repeat Yourself)
- **KISS** (Keep It Simple, Stupid)
- **YAGNI** (You Aren't Gonna Need It)
- **Composition over Inheritance**

Remember: Design patterns are tools, not rules. Use them when they solve a specific problem, not just because they exist. Over-engineering with unnecessary patterns can be as problematic as not using them at all.