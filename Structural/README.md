# Structural Design Patterns

Structural Design Patterns focus on how classes and objects are composed to form larger structures.  
They help ensure flexibility and efficiency in relationships between entities while keeping systems loosely coupled.

These patterns deal primarily with object composition, interface compatibility, and relationship management.

---

## 1. Adapter Pattern

**Intent:**  
Convert the interface of a class into another interface that clients expect. Adapter allows classes with incompatible interfaces to work together.

Adapter solves interface mismatch problems without modifying existing code.

---

## 2. Bridge Pattern

**Intent:**  
Decouple an abstraction from its implementation so that the two can vary independently.

Bridge prevents combinatorial class explosion by separating two orthogonal dimensions of variation.

---

## 3. Composite Pattern

**Intent:**  
Compose objects into tree structures to represent part-whole hierarchies. Composite lets clients treat individual objects and compositions of objects uniformly.

It simplifies client code when dealing with hierarchical structures.

---

## 4. Decorator Pattern

**Intent:**  
Attach additional responsibilities to an object dynamically. Decorators provide a flexible alternative to subclassing for extending functionality.

It allows stacking and runtime behavior composition.

---

## 5. Facade Pattern

**Intent:**  
Provide a unified, simplified interface to a set of interfaces in a subsystem.

Facade hides subsystem complexity and reduces client coupling.

---

## 6. Flyweight Pattern

**Intent:**  
Use sharing to support a large number of fine-grained objects efficiently.

Flyweight minimizes memory usage by separating intrinsic (shared) state from extrinsic (context-specific) state.

---

## 7. Proxy Pattern

**Intent:**  
Provide a surrogate or placeholder for another object to control access to it.

Proxy can manage lazy loading, access control, logging, caching, or remote communication.

---

# Summary

Structural design patterns primarily address:

- Object composition
- Interface adaptation
- Responsibility distribution
- Memory optimization
- Access control
- Subsystem simplification

They help build scalable and maintainable architectures by structuring relationships between classes and objects efficiently.

---

# Structural Patterns UML Overview

<p align="center">
  <img src="Structural_Pattern.png" width="800"/>
</p>
