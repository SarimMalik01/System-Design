## Overview

This project demonstrates the **Strategy Design Pattern** using a Robot behavior system modeled in UML.  
Instead of hardcoding behaviors inside subclasses, robot abilities such as **talking**, **walking**, and **flying** are implemented as interchangeable strategy objects.

This design follows the principle of **composition over inheritance** and allows dynamic behavior configuration at runtime.

---

## Strategy Pattern Definition

> The Strategy Pattern defines a family of algorithms, encapsulates each one in a separate class, and makes them interchangeable at runtime.  
> The context delegates the execution of a specific strategy to a strategy object instead of implementing the behavior directly.

---

## Problem With Inheritance-Based Design

Consider a base class:

```java
class Animal {
    eat();
    walk();
}
```

Subclasses:

```java
Dog extends Animal{--}
Cat extends Animal{--}
```

Now we introduce a new subclass:
```java
Duck extends Animal{--}
```

Duck requires an additional behavior:
```java
fly()
```

This creates two problematic design choices.

---

### ❌ Option 1: Add `fly()` to the Parent Class

```java
class Animal {
    eat();
    walk();
    fly();
}
```
Now:

Dog and Cat do not require fly().

They must either provide empty implementations or throw exceptions.

This leads to:

- Violation of YAGNI (You Aren’t Gonna Need It)

- Poor abstraction

- Unnecessary method exposure

❌ Option 2: Implement fly() Only in Duck
```java
class Duck extends Animal {
    fly();
}
```
Later, if we add:

```java
class Dove extends Animal {
    fly();
}
```
We now duplicate fly logic across multiple subclasses.

This leads to:

- Violation of DRY (Don’t Repeat Yourself)

- Code duplication

- Increased maintenance complexity
---

Strategy-Based Solution (As Modeled in UML)
Instead of defining behaviors in the base class, behaviors are extracted into separate strategy interfaces:

- ITalkable
- IWalkable
- IFlyable

Each interface represents a family of related behaviors.

Concrete Strategy Implementations
- YesTalk / NotTalk
- YesWalk / NotWalk
- YesFly / NotFly

Each behavior is encapsulated in its own class.

### Context Class (Robot)
The Context class does not implement behaviors directly.
Instead, it holds references to behavior strategies:

```java
class Robot{
ITalkable t;
IWalkable w;
IFlyable f;
----
}
```
These are injected via constructor:

```java
Context(ITalkable t, IWalkable w, IFlyable f)
```
Behavior execution is delegated:

```java
t.talk();
w.walk();
f.fly();
```
Key Architectural Shift
Instead of:
A robot is defined by its behaviors (inheritance-based design)

We design:

A robot has behaviors (composition-based design)

This shift eliminates:

- Unused methods

- Null implementations

- Code duplication

- Inheritance explosion

Benefits of This Design
- Follows Open/Closed Principle

- Promotes composition over inheritance

- Allows runtime behavior switching

- Eliminates large conditional logic

Avoids DRY and YAGNI violations

- Improves extensibility and maintainability

## Conclusion
This UML implementation demonstrates a clean and scalable application of the Strategy Pattern using interchangeable behavioral components (Talkable, Walkable, and Flyable).
The design ensures flexibility, modularity, and future extensibility without modifying the core context class.
