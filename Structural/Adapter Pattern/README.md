# Adapter Pattern

## Definition

The **Adapter Pattern** allows incompatible interfaces to work together by introducing a compatibility layer between the client and an existing class (Adaptee).

It converts the interface of a class into another interface that the client expects, without modifying the original source code.

---

## Intent

> Convert the interface of an existing class into a format expected by the client, enabling collaboration between otherwise incompatible interfaces.

---

## Problem It Solves

In many real-world systems:

- A client expects a specific interface.
- A third-party or legacy class provides similar functionality but exposes a different interface.
- Modifying the third-party code is either impossible or undesirable.

Without an Adapter:

- The client would need to change.
- Tight coupling would increase.
- Integration logic would pollute business code.

---

## Solution

The Adapter Pattern introduces a **Target interface**, which defines the contract expected by the client.

The Adapter:

- Implements the Target interface.
- Wraps the incompatible class (Adaptee).
- Translates client requests into calls understood by the Adaptee.

This ensures:

- Reduced coupling
- Better extensibility
- No modification of legacy or third-party code

---

## Structure

### Participants

- **Target** – Interface expected by the client.
- **Adaptee** – Existing incompatible class.
- **Adapter** – Compatibility layer implementing Target and delegating to Adaptee.
- **Client** – Interacts only with the Target interface.

---

## Object Adapter vs Class Adapter

### Object Adapter (Most Common in Java)

Uses composition:

```java
class Adapter implements Target {
    private Adaptee adaptee;
}
```

Adapter has-a Adaptee.

More flexible.

Works well in Java (since Java does not support multiple class inheritance).

### Class Adapter
Uses inheritance:

- class Adapter extends Adaptee implements Target
Adapter is-a Adaptee.

- Less flexible.

- More common in languages supporting multiple inheritance (e.g., C++).

Java primarily uses Object Adapter.

Benefits
- Enables integration with legacy or third-party systems.

- Promotes loose coupling.

- Follows Open/Closed Principle.

- Improves flexibility and maintainability.

- Encapsulates conversion logic in a single place.

# When Adapter Becomes an Anti-Pattern
Adapter should be used carefully. It becomes unnecessary or problematic when:

- The interfaces are already compatible.

- You control both the client and the service code (refactoring is better).

- Every new integration requires an adapter (indicating poor abstraction design).

- There are multiple consecutive adapter layers.
```java
Client-> Adapter 1 -> Adapter 2-> Adapter 3 -> Adapter 4 -> Adapteee
```
- The adapter is used to hide poor architectural decisions.

In such cases, redesigning the interface is a better solution.

## Conclusion
The Adapter Pattern is best suited for integrating incompatible systems without modifying their source code.

It provides a clean compatibility layer, making systems more extensible and maintainable while keeping client code independent from third-party implementations.
