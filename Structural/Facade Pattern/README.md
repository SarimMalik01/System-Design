# Facade Pattern

## Overview

The **Facade Pattern** provides a unified and simplified interface to a complex subsystem, hiding its internal complexity from the client.

Instead of interacting with multiple subsystem classes, the client communicates with a single high-level interface.

---

## Intent

> Provide a simplified interface to a complex subsystem.

Facade focuses on usability and structural simplification.

---

## Principle of Least Knowledge (Law of Demeter)

The Facade Pattern supports the **Principle of Least Knowledge**, which states:

> An object should talk only to its immediate friends and not to strangers.

### Without Facade
```
Client → CPU
Client → Memory
Client → Disk
Client → PowerSupply
```

The client knows too much about the internal subsystem structure.

This increases coupling.

---

### With Facade
```
Client → ComputerFacade
ComputerFacade → CPU
ComputerFacade → Memory
ComputerFacade → Disk
ComputerFacade → PowerSupply
```

The client interacts with only one object.

Internal complexity is hidden.

Coupling is reduced.

---

## Why Facade Encourages Low Coupling

- The client does not depend on subsystem classes.
- Subsystem changes do not directly affect the client.
- Client code becomes cleaner and more readable.
- The dependency graph becomes simpler.

---

# Facade vs Template Method Pattern

Although both patterns may appear similar because they control execution flow, their intent and structure are fundamentally different.

---

## 1️) Orchestration vs Algorithm Skeleton

### Facade Pattern

- Performs **orchestration logic**.
- Calls subsystem methods in a specific sequence.
- Does not define or enforce algorithm steps through inheritance.
- Focuses on simplifying subsystem interaction.

Example:

```java
start() {
   cpu.init();
   memory.load();
   disk.read();
   cpu.execute();
}
```
This is coordination, not customization.

### Template Method Pattern
- Defines the skeleton of an algorithm in a base class.

- Allows subclasses to override specific steps.

- Uses inheritance to control behavior variation.

- Focuses on algorithm structure and reuse.

Example:
```java
process() {
   step1();
   step2();
   step3();
}
```
Subclasses override step2().

## 2️) Intent Difference


| Facade Pattern | Template Method Pattern |
|----------------|--------------------------|
| Provides a unified interface to a complex subsystem | Defines the skeleton of an algorithm |
| Simplifies subsystem usage | Controls algorithm customization |
| Uses composition | Uses inheritance |
| Focused on structural simplification | Focused on reducing redundancy and enforcing a processing pipeline |

## Summary
Facade Pattern simplifies complex subsystems by providing a unified interface and reducing coupling.

Template Method Pattern defines a reusable algorithm structure and allows controlled customization through subclassing.

They may both involve ordered method calls, but their purpose and architectural roles are different.
