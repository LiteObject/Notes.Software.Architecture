# Essential Design Patterns

## **Creational Patterns** (Object Creation)

1. **Singleton** - Ensures a class has only one instance with global access
2. **Factory Method** - Creates objects without specifying exact classes
3. **Abstract Factory** - Creates families of related objects
4. **Builder** - Constructs complex objects step by step
5. **Prototype** - Creates new objects by cloning existing ones

## **Structural Patterns** (Object Composition)

6. **Adapter** - Makes incompatible interfaces work together
7. **Decorator** - Adds new functionality to objects dynamically
8. **Facade** - Provides a simplified interface to complex subsystems
9. **Proxy** - Controls access to objects
10. **Composite** - Treats individual objects and compositions uniformly
11. **Bridge** - Separates abstraction from implementation
12. **Flyweight** - Shares intrinsic state between many similar objects to minimize memory usage

## **Behavioral Patterns** (Object Interaction & Responsibility)

13. **Strategy** - Encapsulates algorithms and makes them interchangeable
14. **Observer** - Notifies multiple objects about state changes (pub/sub)
15. **Command** - Encapsulates requests as objects
16. **Template Method** - Defines algorithm skeleton, lets subclasses override steps
17. **Iterator** - Provides sequential access to elements
18. **State** - Alters object behavior when internal state changes
19. **Chain of Responsibility** - Passes requests along a chain of handlers
20. **Mediator** - Reduces coupling between communicating objects
21. **Memento** - Captures and restores object state
22. **Visitor** - Separates algorithms from objects they operate on

## **Architectural Patterns** (System-Level)

23. **MVC (Model-View-Controller)** - Separates data, UI, and logic
24. **MVVM (Model-View-ViewModel)** - Variation of MVC for data binding
25. **Repository** - Abstracts data access layer
26. **Dependency Injection** - Design principle that inverts control of object creation and wiring
27. **Service Layer** - Delimits business logic boundaries and coordinates application operations

## **Priority for Senior Engineers**

**Must Know (Critical):**
- Singleton, Factory, Builder
- Adapter, Decorator, Facade, Proxy
- Strategy, Observer, Command, Template Method
- Dependency Injection, Repository

**Should Know (Important):**
- Abstract Factory, Prototype
- Composite, Bridge
- State, Chain of Responsibility, Iterator
- MVC/MVVM, Service Layer

**Good to Know:**
- Flyweight, Mediator, Memento, Visitor

## **Key Principles to Understand**

Along with patterns, master these foundational principles:
- **SOLID** principles (Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, Dependency Inversion)
- **DRY** (Don't Repeat Yourself)
- **KISS** (Keep It Simple, Stupid)
- **YAGNI** (You Aren't Gonna Need It)
- **Composition over Inheritance**

Remember: Design patterns are tools, not rules. Use them when they solve a specific problem, not just because they exist. Over-engineering with unnecessary patterns can be as problematic as not using them at all.