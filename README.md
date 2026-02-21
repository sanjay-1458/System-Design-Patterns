
# Software Design Patterns Repository

This repository contains documentation and examples of commonly used software design patterns. 
Each pattern provides a solution to recurring problems in software design, making code more
flexible, reusable, and maintainable.

---

## Table of Design Patterns

| Pattern Name | Description |
|--------------|-------------|
| [Adapter](Adapter_Design_Pattern.md) | Converts the interface of a class into another interface clients expect. Useful when integrating incompatible interfaces. |
| [Bridge](Bridge_Design_Pattern.md) | Decouples an abstraction from its implementation, allowing them to vary independently. Solves problems of tight coupling between abstractions and implementations. |
| [Builder](Builder_Design_Pattern.md) | Separates construction of a complex object from its representation. Useful for creating different representations of an object using the same process. |
| [Chain of Responsibility](Chain_Of_Responsibility.md) | Passes a request along a chain of handlers. Each handler decides whether to process it or pass it along. Solves the problem of coupling senders to receivers. |
| [Command](Command_Design_Pattern.md) | Encapsulates a request as an object, allowing parameterization of clients and queuing or logging of requests. Useful for undo/redo functionality. |
| [Composite](Composite_Design_Pattern.md) | Composes objects into tree structures to represent part-whole hierarchies. Treats individual objects and compositions uniformly. |
| [Decorator](Decorator_Design_Pattern.md) | Dynamically adds behavior to objects without affecting other objects of the same class. Solves the problem of extending functionality without inheritance. |
| [Facade](Facade_Design_Pattern.md) | Provides a simplified interface to a complex subsystem. Useful for reducing complexity and dependencies in client code. |
| [Factory](Factory_Design_Pattern.md) | Defines an interface for creating objects but lets subclasses decide which class to instantiate. Solves the problem of creating objects without specifying exact classes. |
| [Flyweight](FlyWeight_Design_Pattern.md) | Reduces memory usage by sharing common parts of objects. Solves problems of high memory consumption with many similar objects. |
| [Iterator](Iterator_Design_Pattern.md) | Provides a way to access elements of a collection without exposing its underlying representation. Useful for traversing collections uniformly. |
| [Mediator](Mediator_Design_Pattern.md) | Encapsulates how objects interact, promoting loose coupling. Solves problems of complex communication networks between objects. |
| [Memento](Memento_Design_Pattern.md) | Captures and restores an object's internal state. Useful for implementing undo functionality. |
| [Observer](Observer_Design_Pattern.md) | Defines a one-to-many dependency between objects so that when one changes state, all dependents are notified. Solves the problem of keeping objects in sync. |
| [Prototype](Prototype_Design_Pattern.md) | Creates new objects by copying existing ones. Useful when creating new instances is expensive or complex. |
| [Proxy](Proxy_Design_Pattern.md) | Provides a surrogate or placeholder for another object to control access. Solves problems like lazy loading, access control, or logging. |
| [Singleton](Singleton_Design_Pattern.md) | Ensures a class has only one instance and provides a global point of access to it. Useful for shared resources like configuration objects or logging. |
| [State](State_Design_Pattern.md) | Allows an object to alter its behavior when its internal state changes. Solves the problem of conditional logic scattered across methods. |
| [Strategy](Strategy_Design_Pattern.md) | Defines a family of algorithms, encapsulates each one, and makes them interchangeable. Solves the problem of conditional statements in algorithms. |
| [Template](Template_Design_Pattern.md) | Defines the skeleton of an algorithm in a method, deferring some steps to subclasses. Useful for code reuse and consistent algorithm structure. |
| [Visitor](Visitor_Design_Pattern.md) | Separates an algorithm from the object structure it operates on. Useful for performing operations on object structures without modifying the classes. |

---

## Importance of Design Patterns

- **Code Reusability:** Patterns provide proven solutions that can be reused across projects.
- **Maintainability:** They help in building scalable and easy-to-maintain code.
- **Flexibility:** Decouple classes and allow independent variation of components.
- **Communication:** Provide a common vocabulary for developers to communicate design ideas efficiently.

---


================================================================================
## Common Design Problems & Pattern Solutions
================================================================================

1. **Problem:** You want to **add new operations to a set of classes** without changing the classes themselves.  
   └─ **Solution:** **Visitor** Pattern  
       - Visitor lets you create a separate object (the visitor) that can perform operations on a set of classes.  
       - **Why it works:** You can add new behaviors without touching existing code. The object structure remains stable, while visitors define new actions.  
       - **Cons:** Adding a new class to the structure requires updating all visitors.  

--------------------------------------------------------------------------------

2. **Problem:** An object behaves differently depending on its **internal state**, and you don’t want lots of `if/else` everywhere.  
   └─ **Solution:** **State** Pattern  
       - State moves the behavior for each state into its own class. The object changes its behavior by changing its current state.  
       - **Why it works:** Makes your code cleaner and easier to maintain by keeping behavior logic separate.  
       - **Cons:** Increases the number of classes.  

--------------------------------------------------------------------------------

3. **Problem:** Multiple parts of your program need to **know when something changes** in another object.  
   └─ **Solution:** **Observer** Pattern  
       - Observer lets objects “subscribe” to another object. When the subject changes, all observers are automatically notified.  
       - **Why it works:** Helps keep different parts of your system in sync without tightly connecting them.  
       - **Cons:** Forgetting to remove observers can cause memory issues.  

--------------------------------------------------------------------------------

4. **Problem:** You want to **build a complicated object step by step** (like a custom pizza), sometimes with different variations.  
   └─ **Solution:** **Builder** Pattern  
       - Builder separates the process of creating an object from the final product. Different builders can create different products using the same steps.  
       - **Why it works:** Lets you make complex objects without messy constructors or multiple parameters.  
       - **Cons:** Adds extra builder classes, so more code to manage.  

--------------------------------------------------------------------------------

5. **Problem:** You need to **control access to an object**, or **add extra features** (like logging) without touching the original object.  
   └─ **Solution:** **Proxy** Pattern  
       - Proxy acts as a “middleman” for the real object. It can delay creation, check permissions, or log actions.  
       - **Why it works:** You can add functionality safely without changing the object itself.  
       - **Cons:** Extra layer can make the code slightly slower.  

--------------------------------------------------------------------------------

6. **Problem:** You have **thousands of similar objects** and don’t want to waste memory.  
   └─ **Solution:** **Flyweight** Pattern  
       - Flyweight shares parts of objects (intrinsic data) and keeps only unique parts separate (extrinsic data).  
       - **Why it works:** Reduces memory usage while still keeping objects functional.  
       - **Cons:** Code becomes more complex, managing shared vs unique parts can be tricky.  

--------------------------------------------------------------------------------

7. **Problem:** You want to **switch between different ways of doing something** (algorithms) without changing the main code.  
   └─ **Solution:** **Strategy** Pattern  
       - Strategy wraps each algorithm into its own class. The main code can pick which algorithm to use at runtime.  
       - **Why it works:** Lets you swap behaviors easily and keeps your code flexible.  
       - **Cons:** Adds extra classes for each algorithm.  

--------------------------------------------------------------------------------

8. **Problem:** You want **only one instance of a class** in your program (like a printer manager or a global configuration).  
   └─ **Solution:** **Singleton** Pattern  
       - Singleton ensures only one object exists and gives a global way to access it.  
       - **Why it works:** Controls object creation and avoids multiple conflicting instances.  
       - **Cons:** Overuse can make testing harder and create hidden dependencies.  

--------------------------------------------------------------------------------

9. **Problem:** Your system is **complex**, and you want to **simplify the interface** for clients.  
   └─ **Solution:** **Facade** Pattern  
       - Facade provides a simple interface that hides all the complex details of the system.  
       - **Why it works:** Clients can use a few simple methods instead of understanding all classes.  
       - **Cons:** If too much logic is added to Facade, it can become a “god object.”

--------------------------------------------------------------------------------

10. **Problem:** You want to **pass a request along several objects**, and the first object that can handle it should do so.  
    └─ **Solution:** **Chain of Responsibility** Pattern  
        - Each handler decides to process the request or pass it along.  
        - **Why it works:** Avoids tightly coupling sender and receiver; multiple handlers can share responsibility.  
        - **Cons:** If no handler can process the request, it may go unhandled.  

--------------------------------------------------------------------------------

11. **Problem:** You want to **create a new object by copying an existing one**, instead of building it from scratch.  
    └─ **Solution:** **Prototype** Pattern  
        - Prototype clones an existing object to make a new one.  
        - **Why it works:** Useful when object creation is expensive or complicated.  
        - **Cons:** Cloning objects with complex states can be tricky.  

--------------------------------------------------------------------------------

12. **Problem:** You want to **treat requests as objects**, so they can be queued, logged, or undone.  
    └─ **Solution:** **Command** Pattern  
        - Command wraps a request in an object. It can be stored, executed later, or reversed.  
        - **Why it works:** Separates the sender and receiver, making code flexible and undo-friendly.  
        - **Cons:** More classes if you have many types of commands.  

================================================================================


This repository serves as a reference for developers to understand, implement, and leverage design patterns effectively.
