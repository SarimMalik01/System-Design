# Bridge Pattern

## Definition

The **Bridge Pattern** decouples an abstraction from its implementation so that the two can vary independently.

It separates two orthogonal dimensions of a system:

- The abstraction (what it is)
- The implementation (how it works)

This prevents class explosion and improves extensibility.

---

## Problem It Solves

Consider a system with two varying dimensions:

- Car Type → SUV, Sedan
- Engine Type → Petrol, Diesel, Hybrid

If inheritance is used to combine them:
```java
PetrolSUV
DieselSUV
HybridSUV
PetrolSedan
DieselSedan
HybridSedan
```

This leads to combinatorial explosion.

Adding a new engine type requires creating new subclasses for every car type.

---

## Solution – Bridge Pattern

Bridge separates:

- Abstraction hierarchy (Car)
- Implementation hierarchy (Engine)

The abstraction holds a reference to the implementation and delegates behavior to it.

This allows both hierarchies to evolve independently.

Example:

```java
Car suv = new SUV(new PetrolEngine());
Car sedan = new Sedan(new HybridEngine());
```
No new subclasses are required for combinations.

## Key Characteristics
- Uses composition instead of inheritance

- Reduces tight coupling between abstraction and implementation

- Prevents class explosion

- Allows independent extension of both hierarchies

- Uses single dispatch

## Difference Between Bridge and Visitor Pattern
Although both separate concerns, they solve fundamentally different problems.

1️ Nature of the Relationship
1) Bridge:

- The implementation is intrinsic to the abstraction.

- The object is not meaningful without it.

Example: A Car without an Engine is not meaningful.

2) Visitor:

- The operation is external to the object structure.

- The object remains meaningful even without a particular operation.

Example: A TextDocument is meaningful even if no compression operation is applied.

2️ Dispatch Mechanism
1) Bridge:

- Uses single dispatch.

- The abstraction delegates behavior to the implementor.
```java
engine.start();
```
2) Visitor:

- Uses double dispatch.

- Behavior depends on both the element type and the visitor type.

Example : Client Code
```java
element.accept(visitor);
```
Element Code 
```java
visitor.visit(element);
```
## When to Use Bridge
- When there are two independent dimensions of variation

- When inheritance would cause combinatorial explosion

- When abstraction and implementation should evolve separately

- When runtime composition is required

## Summary
Bridge Pattern separates abstraction from implementation, allowing both to vary independently.

It focuses on structural decoupling and preventing subclass explosion, while maintaining flexibility through composition.

