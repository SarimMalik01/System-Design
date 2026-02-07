# Visitor Pattern

## Definition

The **Visitor Pattern** separates the object structure from the operations performed on it.  
Each operation is encapsulated inside its own Visitor class, allowing new operations to be added without modifying the existing element classes.

The object structure remains stable, while the operations can vary and extend independently.

Visitor achieves this through **double dispatch**, where:

- The runtime type of the element decides which `accept()` method is invoked.
- The runtime type of the visitor decides which `visit()` method is executed.

---

## Intent

> Allow adding new operations to an existing object structure without modifying the classes of that structure.

---

## Problem: Bad Design (Without Visitor Pattern)

![Bad Design UML](Bad%20Design.png)

Consider a system with the following structure:

- `TextFile`
- `Audio`
- `Video`

If we define operations directly inside these classes:

- `exportToPDF()`
- `exportToHTML()`
- `compress()`
- `metaDataExt()`

Then each class must implement all operations.

This leads to:

- Class bloating  
- Harder maintenance  
- Violation of Open/Closed Principle  
- Tight coupling between data and behavior  
- Repeated modification of classes when adding new operations  
- Poor separation of concerns  

Whenever a new operation is introduced, all document classes must be modified.

---

## Solution: Visitor Pattern

In a better design using Visitor Pattern:

- The object structure contains only:
  
  ```java
  void accept(Visitor v);
  ```
All operations are moved into separate Visitor classes.

Example visitors:
```java
ExportToPDFVisitor
```
```java
ExportToHTMLVisitor
```
```java
CompressVisitor
```
```java
MetadataVisitor
```

Now:

The document classes (TextFile, Audio, Video) remain unchanged.

New operations can be added by creating new Visitor classes.

The system becomes open to extension and closed to modification.

Structure
- Element Interface
```java
interface Document {
    void accept(DocumentVisitor visitor);
}
```
- Concrete Elements
```java
class TextFile implements Document {
    public void accept(DocumentVisitor visitor) {
        visitor.visit(this);
    }
}
```
- Visitor Interface
```java
interface DocumentVisitor {
    void visit(TextFile doc);
    void visit(Audio doc);
    void visit(Video doc);
}
```
Double Dispatch
Visitor uses double dispatch:
```java
document.accept(visitor);
```
The runtime type of the document decides which accept() is called.

Inside accept(), the correct overloaded visit() method is selected based on the document type.

Thus, behavior depends on both:

- The type of the element

- The type of the visitor

Benefits
- ✔ Open/Closed Principle for operations

- ✔ Clean separation of concerns

- ✔ Avoids class bloating

- ✔ Easy to add new operations

- ✔ Centralizes related behavior

### Trade-off
Visitor works best when:

- The object structure is stable

- New operations are added frequently

- If new element types are added often, all visitors must be modified.

### Conclusion
Visitor Pattern externalizes operations from the object structure, enabling scalable extension of behavior without modifying existing classes.

It is particularly useful in systems where the data structure remains stable but operations evolve over time.
