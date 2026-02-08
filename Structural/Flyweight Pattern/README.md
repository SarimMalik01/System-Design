# Flyweight Pattern

## Overview

The **Flyweight Pattern** is a structural design pattern used to reduce memory usage by sharing common (intrinsic) state across multiple objects while externalizing the varying (extrinsic) state.

Instead of creating fully independent objects that duplicate large portions of identical data, Flyweight separates:

- **Intrinsic State** → Shared, immutable, reusable core state  
- **Extrinsic State** → Context-specific state supplied externally  

This design prevents memory spikes and avoids RAM exhaustion when millions of similar objects are created.

---

## Core Idea

Many objects may look different externally, but internally share the same core properties.

Instead of duplicating the shared core each time:

- Store intrinsic state once.
- Reuse it across multiple wrapper objects.
- Attach extrinsic state per usage.

This dramatically reduces memory footprint.

---

## Participants in the Pattern

### 1. Intrinsic Interface

```java
interface IIntrinsic {
    void render();
}
```

Defines the core behavior that can be shared.

---

### 2. ConcreteIntrinsic

- Holds intrinsic (shared) properties.
- Implements `render()`.
- Objects of this type are stored in the factory pool.

These objects must be **immutable** to remain safe for sharing.

---

### 3. Flyweight Factory

- Maintains a pool of intrinsic objects.
- Uses intrinsic properties as keys.
- Reuses existing objects if available.
- Creates new ones only when necessary.

Example structure:

```java
Map<Key, IIntrinsic> pool;
```

The factory ensures that intrinsic objects are reused rather than recreated.

---

### 4. Extrinsic (Wrapper / Context)

- Holds extrinsic properties (unique per instance).
- Holds a reference to an `IIntrinsic`.
- Delegates rendering to intrinsic.

This class wraps extrinsic state around the shared intrinsic core.

---

## Why This Avoids Memory Spikes

Without Flyweight:

- Millions of objects
- Each object duplicates common properties
- Massive memory usage

With Flyweight:

- One shared intrinsic object
- Many lightweight wrappers with small extrinsic differences
- Efficient memory reuse

This prevents memory choking and large RAM consumption.

---

## Conceptual Flow

1. Client requests object with certain intrinsic + extrinsic values.
2. Factory checks if intrinsic exists.
3. If exists → reuse it.
4. If not → create and store it.
5. Wrap intrinsic inside an extrinsic object.
6. Return final composed object.

Client remains unaware of pooling logic.

---

## Ice Cream Analogy
<p align="center">
  <img src="ICE_CREAM_Analogy.png" width="600" height="400" />
</p>

Imagine ice cream cones:

- **Cone** → Intrinsic (shared, same reference can be reused)
- **Flavour** → Extrinsic (varies per serving)

If 10,000 customers order ice cream:

- We do not create 10,000 cone designs.
- We reuse the same cone type.
- Only the flavour differs per order.

The cone is the shared core.  
The flavour is the contextual variation.

---

## Key Rules

- Intrinsic state must be **immutable**.
- Extrinsic state must be supplied externally.
- Factory manages object reuse.
- Client should not know pooling logic.

---

## When to Use Flyweight

Use Flyweight when:

- You need a very large number of similar objects.
- Many objects share identical state.
- Memory optimization is critical.
