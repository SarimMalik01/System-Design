# Builder Design Pattern

## Definition

The **Builder Pattern** separates the construction of a complex object from its representation so that the same construction process can create different representations.

It helps construct complex objects step-by-step without exposing construction logic to the client.

---

# Why Builder Is Needed

## The Telescoping Constructor Problem

When a class has many parameters (especially optional ones), constructors start multiplying:

```java
class User {
    String name;
    int age;
    String email;
    String phone;
    String address;

    User(String name) { ... }

    User(String name, int age) { ... }

    User(String name, int age, String email) { ... }

    User(String name, int age, String email, String phone) { ... }

    User(String name, int age, String email, String phone, String address) { ... }
}
```

### Problems

- Too many overloaded constructors  
- Hard to read  
- Error-prone parameter ordering  
- Poor maintainability  
- Difficult to extend  

This is known as the **Telescoping Constructor Anti-Pattern**.

The Builder Pattern eliminates this problem by moving object construction into a separate builder class.

---

# 1. Simple Builder (Fluent Builder)

## Intent

Encapsulate complex object construction logic inside a builder class while allowing the client to configure the object step-by-step using method chaining.

The **client directly controls** the construction process.

---

## Structure

- Product class  
- Static or separate Builder class  
- Builder holds reference to the product  
- `build()` returns the final object  

---

## Characteristics

- No Director  
- Client defines build sequence  
- Uses method chaining (Fluent API)  
- Eliminates telescoping constructors  
- Improves readability  
- Supports immutability  

---

## Flow

```
Client → Builder → Product
```

Example:

```java
Product p = new ProductBuilder()
                .setX(...)
                .setY(...)
                .build();
```

### What Happens Internally

- Builder creates product instance  
- Modifies it step-by-step  
- Returns final constructed object  

---

## When To Use Simple Builder

- Object has many optional parameters  
- Constructor becomes unreadable  
- You want fluent, readable creation  
- Order of steps is not strict  
- Modern API-style design is preferred  

---

# 2. Builder with Director (Classic GoF Builder)

## Intent

Separate the **construction algorithm** from the **representation**, so the same construction process can produce different representations.

The **Director defines the sequence**.
The **Builder defines how each step is executed**.

---

## Structure

- Client  
- Director  
- IBuilder (interface)  
- ConcreteBuilder1  
- ConcreteBuilder2  
- Product  

---

## Roles

### Product

The complex object being constructed.

```java
class A {
    int r, x, y;
}
```

---

### Builder Interface

Defines construction steps.

```java
interface IBuilder {
    void setR();
    void setX();
    void setY();
    A getResult();
}
```

---

### Concrete Builders

Different representations of the same product.

```java
class Builder1 implements IBuilder { ... }
class Builder2 implements IBuilder { ... }
```

Each builder configures `Product A` differently.

---

### Director

Controls the construction sequence.

```java
class Director {
    public A construct(IBuilder b) {
        b.setR();
        b.setX();
        b.setY();
        return b.getResult();
    }
}
```

The Director enforces a fixed build sequence.

---

### Client

```java
A obj = new Director().construct(new Builder1());
```

Client does not know internal construction details.

---

## Flow

```
Client → Director → Builder → Product
```

### Director Responsibilities

- Controls order of steps  
- Calls builder methods  
- Returns final product  

### Builder Responsibilities

- Implements each construction step  
- Produces specific representation  

---

# Key Difference: Simple Builder vs Director Builder

| Simple Builder | Builder with Director |
|---------------|----------------------|
| Client controls build steps | Director controls build steps |
| Flexible order | Fixed construction algorithm |
| Eliminates telescoping constructors | Separates algorithm from representation |
| Common in modern APIs | Classic GoF implementation |
| Focused on clean object creation | Focused on reusable construction workflow |

---

# When To Use Director

- Construction sequence must be enforced  
- Same algorithm should produce different representations  
- Building logic is complex  
- Reusable construction workflow is needed  

---

# When Director Is Not Needed

- Order of steps does not matter  
- Client customization is required  
- Fluent style is preferred  
- Object creation is straightforward  

---

# Summary

Builder Pattern solves:

- Telescoping constructor anti-pattern  
- Complex object initialization  
- Readability issues  
- Poor maintainability  
- Tight coupling between construction and representation  

---

## Final Insight

- **Simple Builder** → Focus on clean, readable object creation  
- **Director Builder** → Focus on separating construction algorithm from representation  

In modern software development, the **Fluent Builder** is more commonly used, while the **Director version** is conceptually important for understanding the original GoF design.
