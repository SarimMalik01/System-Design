# Factory Design Patterns

## 1. Simple Factory Pattern

### Intent
Encapsulate object creation logic inside a single factory class to hide instantiation details from the client.

### What It Does
- Centralizes object creation.
- Uses conditional logic to decide which concrete class to instantiate.
- Client depends only on the factory, not concrete classes.

### Limitation
- Violates Open/Closed Principle.
- Adding new product types requires modifying the factory class.
- Can become bloated with many conditional statements.

---

## 2. Factory Method Pattern

### Intent
Define an interface for creating an object, but allow subclasses(factory) to decide which concrete class(product) to instantiate.

### What It Does
- Delegates object creation to subclasses.
- Eliminates large conditional creation logic.
- Promotes extensibility via inheritance.
- Follows Open/Closed Principle better than Simple Factory.

### Limitation
- Increases number of classes.
- Each product variation may require a new factory subclass.
- Can add structural complexity for small systems.

---

## 3. Abstract Factory Pattern

### Intent
Provide an interface for creating families of related or dependent objects without specifying their concrete classes.

### What It Does
- Ensures compatibility among related product families.
- Encapsulates creation logic for multiple related products.
- Decouples client from concrete implementations.
- Strongly supports Open/Closed Principle.

### Limitation
- Adding a new product type requires modifying all factory interfaces and implementations.
- Can introduce significant complexity.
- Not ideal when product families rarely change.

  
