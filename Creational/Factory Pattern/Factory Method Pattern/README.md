# Factory Method Pattern

## 1. Definition

The Factory Method Pattern defines an interface for creating an object, but allows subclasses to decide which concrete class to instantiate.

It delegates the responsibility of object creation to subclasses instead of handling it directly in client code.

---

## 2. Intent

- Encapsulate object creation logic.
- Defer instantiation to subclasses.
- Promote loose coupling between client and concrete classes.
- Follow the Open/Closed Principle by allowing new product types without modifying existing code.

---

## 3. Problem It Solves

When client code directly instantiates objects:

```java
Car car = new Sedan();
```

Problems:
- Client becomes tightly coupled to concrete classes.
- Adding new types requires modifying client code.
- Violates Open/Closed Principle.
- Leads to large conditional blocks.

Factory Method moves this creation logic into subclasses.

---

## 4. Visual Mapping Explanation

<p align="center">
  <img src="Mapping.png" width="600" height="600" />
</p>


The above diagram illustrates how different factories are responsible for creating different products.

- **Factory 1** creates Product 1, Product 2, and Product 3.
- **Factory 2** creates Product 3 and Product 4.

Key Observations:

1. Multiple factories can create overlapping products.
2. Each factory controls which concrete products it is responsible for.
3. The client interacts only with the factory abstraction, not with product constructors.
4. The mapping between factory and product is defined inside subclasses, not in the client.

This demonstrates how creation logic is distributed across subclasses rather than centralized in one large conditional factory.

---

## 5. Structure

### 5.1 Product Interface

```java
interface Car {
    void drive();
}
```

Defines the contract for all concrete products.

---

### 5.2 Concrete Products

```java
class Sedan implements Car {
    public void drive() {
        System.out.println("Driving Sedan");
    }
}
```

```java
class SUV implements Car {
    public void drive() {
        System.out.println("Driving SUV");
    }
}
```

---

### 5.3 Creator (Abstract Class)

```java
abstract class CarFactory {

    // Factory Method
    abstract Car createCar();

    // Common business logic
    public void deliverCar() {
        Car car = createCar();
        car.drive();
    }
}
```

The factory method is declared but not implemented here.
Subclasses define the concrete instantiation.

---

### 5.4 Concrete Factories

```java
class SedanFactory extends CarFactory {

    public Car createCar() {
        return new Sedan();
    }
}
```

```java
class SUVFactory extends CarFactory {

    public Car createCar() {
        return new SUV();
    }
}
```

Each concrete factory decides which product to create.

---

## 6. Client Code

```java
public class Main {

    public static void main(String[] args) {

        CarFactory factory = new SedanFactory();
        factory.deliverCar();

        factory = new SUVFactory();
        factory.deliverCar();
    }
}
```

The client depends only on abstractions:
- `CarFactory`
- `Car`

It does not depend on `Sedan` or `SUV` directly.

---

## 7. Key Characteristics

- Uses inheritance for object creation.
- Removes direct dependency on concrete classes.
- Avoids large switch or if-else blocks.
- Supports extension without modifying existing code.

---

## 8. Factory Method vs Simple Factory

| Factory Method | Simple Factory |
|---------------|----------------|
| Uses subclasses to decide creation | Uses conditional logic |
| Supports Open/Closed Principle | Often violates Open/Closed |
| Creation logic distributed | Creation logic centralized |

---

## 9. When to Use Factory Method

Use Factory Method when:

- A class cannot anticipate which object it must create.
- Subclasses should decide instantiation logic.
- You want to eliminate conditional object creation (large if-else or switch blocks).
- You want extensibility without modifying existing code (Open/Closed Principle).
- A factory is responsible for creating only a **subset of products**, and the creation of other product types must be delegated to other concrete factories.

In such cases:

- Each concrete factory handles only the products it is compatible with.
- Different factories manage different product subsets.
- The client chooses the appropriate factory based on context.

This ensures:
- Clear separation of responsibilities.
- Encapsulation of product compatibility rules.
- Scalable design when product families grow.

---

## 10. Conclusion

The Factory Method Pattern separates object creation from usage logic.  
It delegates instantiation responsibility to subclasses, improving maintainability, flexibility, and adherence to the Open/Closed Principle.

The mapping diagram clearly shows how different factories control different product instantiations while keeping client code independent of concrete implementations.
