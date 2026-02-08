# Composite Pattern

## Intent

To compose objects into tree structures representing part–whole hierarchies and allow clients to treat individual objects (leaf nodes) and compositions of objects (composite nodes) uniformly.

---

## Definition

The **Composite Pattern** provides a unified abstraction for nested, tree-structured systems.  
It allows clients to interact with both leaf and non-leaf objects through a common interface, while encapsulating recursive traversal logic within the composite structure.

The client should not need to distinguish between a single object and a group of objects.

---

## Problem It Solves

In systems where objects form a hierarchical tree (such as file systems, GUI components, or organization structures):

- Some objects are individual elements (Leaf)
- Some objects contain other elements (Composite)

Without Composite:

- Client must check types (`instanceof`) fpr behavioural operations 
- Recursive traversal logic leaks into client
- Coupling increases
- Code becomes harder to maintain

Composite centralizes and encapsulates this recursive behavior.

---

# Structure

## 1️) Component (Abstraction)

Defines the common interface for both leaf and composite objects.

```java
interface FileSystemNode {
    void showDetails();
}
```
The client interacts only with this abstraction.

2️) Leaf
Represents individual objects in the structure.
It does not contain children.
```
class File implements FileSystemNode {

    private String name;

    public File(String name) {
        this.name = name;
    }

    public void showDetails() {
        System.out.println("File: " + name);
    }
}
```
3️) Composite
Represents objects that can contain other components.

```
class Folder implements FileSystemNode {

    private String name;
    private List<FileSystemNode> children = new ArrayList<>();

    public Folder(String name) {
        this.name = name;
    }

    public void add(FileSystemNode node) {
        children.add(node);
    }

    public void remove(FileSystemNode node) {
        children.remove(node);
    }

    public void showDetails() {
        System.out.println("Folder: " + name);

        for (FileSystemNode child : children) {
            child.showDetails();   // Recursive call (DFS)
        }
    }
}
```
The composite is responsible for:

- Managing children

- Encapsulating recursive traversal

- Delegating operations to child components

## Safe Composite Variation
In the Safe Composite design:

- add() and remove() are declared only in the Composite class.

- The Component interface does not include structural modification methods.

## Why It Is Called "Safe"
- Leaf does not have meaningless methods.

- No runtime UnsupportedOperationException.

- Better adherence to Interface Segregation Principle.

- Structure modification is restricted to composite objects only.

## Trade-off
The client must sometimes know it is working for structural operations ( add() / remove() can't work on leaf ):
```
Folder folder = new Folder("Documents");
folder.add(file);
```
- Full uniformity is slightly sacrificed for cleaner abstraction.

## Key Characteristics
- Represents part–whole hierarchy

- Uses recursion internally

- Treats leaf and composite uniformly

- Encapsulates traversal logic

- Eliminates type-check conditionals

### Conclusion
The Composite Pattern simplifies interaction with tree-structured systems by providing a common abstraction for both individual objects and compositions.

It hides recursive traversal logic within the composite, ensuring that the client interacts only with the abstraction, not with structural complexity.

Composite promotes cleaner architecture, reduced coupling, and improved maintainability in hierarchical systems.
