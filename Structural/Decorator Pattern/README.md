# Decorator Pattern

## Definition

The **Decorator Pattern** is a structural design pattern that allows behavior to be added dynamically to an object by wrapping it inside another object that implements the same interface. The original object's structure remains unchanged while new functionality is layered on through composition.

---

## Intent

- Attach additional responsibilities to an object dynamically.
- Provide a flexible alternative to subclassing for extending functionality.
- Allow stacking of behaviors at runtime.

It follows the principle of **composition over inheritance**.

---

## Problem It Solves

### 1️) Class Explosion

Without Decorator, extending behavior via inheritance leads to multiple subclass combinations:

```
Coffee
MilkCoffee
SugarCoffee
MilkSugarCoffee
CreamMilkSugarCoffee
...
```

This results in exponential growth of classes.

Decorator solves this by enabling dynamic composition:

```
Milk(Sugar(Coffee))
```

---

### 2️) Open/Closed Principle (OCP)

Without Decorator:
- Adding new features requires modifying base classes.
- Violates OCP.

With Decorator:
- New behavior is added via new decorator classes.
- Existing classes remain unchanged.
- System is open for extension and closed for modification.

---

## Structure

### 1️) Component Interface (IProduct)

```java
interface IProduct {
    String getDescription();
    double cost();
}
```

Defines the contract for both base object and decorators.

---

### 2️) Concrete Component (Base Class)

```java
class Coffee implements IProduct {

    public String getDescription() {
        return "Basic Coffee";
    }

    public double cost() {
        return 5.0;
    }
}
```

This is the core object whose behavior can be extended.

---

### 3️) Abstract Decorator

```java
abstract class ProductDecorator implements IProduct {

    protected IProduct product;

    public ProductDecorator(IProduct product) {
        this.product = product;
    }

    public String getDescription() {
        return product.getDescription();
    }

    public double cost() {
        return product.cost();
    }
}
```

Key characteristics:

- Implements `IProduct`
- Holds reference to `IProduct`
- Delegates method calls to wrapped object

---

### 4️) Concrete Decorators

#### Milk

```java
class Milk extends ProductDecorator {

    public Milk(IProduct product) {
        super(product);
    }

    public String getDescription() {
        return product.getDescription() + ", Milk";
    }

    public double cost() {
        return product.cost() + 1.5;
    }
}
```

#### Sugar

```java
class Sugar extends ProductDecorator {

    public Sugar(IProduct product) {
        super(product);
    }

    public String getDescription() {
        return product.getDescription() + ", Sugar";
    }

    public double cost() {
        return product.cost() + 0.5;
    }
}
```

Each decorator:
- overrides behavior  
- delegates to wrapped object  
- adds additional logic  

---

## Recursive Call Flow

When client writes:

```java
IProduct coffee = new Sugar(new Milk(new Coffee()));
```

The structure becomes:

```
Sugar
  → Milk
      → Coffee
```

Calling:

```java
coffee.cost();
```

Execution flow:

```
Sugar.cost()
    → Milk.cost()
        → Coffee.cost()
```

Then unwinds:

```
Coffee.cost() = 5.0
Milk adds 1.5 → 6.5
Sugar adds 0.5 → 7.0
```

Each layer enhances behavior through recursive delegation.

---

## Difference from Visitor

| Decorator | Visitor |
|------------|----------|
| Adds behavior to a specific object instance | Adds new operations across object types |
| Changes object composition | Does not change object structure |
| Allows stacking multiple behaviors | Executes one operation at a time |
| Uses single dispatch | Uses double dispatch |
| Behavior becomes part of object identity | Operation does not change identity |

Visitor performs operations externally.  
Decorator modifies behavior through composition.

---

## Difference from Bridge

| Decorator | Bridge |
|------------|----------|
| Adds dynamic responsibilities | Separates abstraction from implementation |
| Allows stacking of behaviors | Only one implementation is plugged in |
| Focuses on behavior extension | Focuses on decoupling hierarchy dimensions |
| Runtime composition chain | Single implementation reference |

Bridge solves class explosion due to multiple inheritance dimensions.  
Decorator solves behavioral extension without subclass explosion.

---

## Conclusion

The Decorator Pattern provides a flexible way to extend object behavior dynamically without modifying the original class.

It:

- Prevents subclass explosion
- Preserves Open/Closed Principle
- Enables runtime composition
- Supports recursive behavior stacking

Decorator transforms an object by wrapping it in layers of behavior, allowing scalable and maintainable design.
