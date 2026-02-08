# Proxy Pattern

## 1. Definition

The Proxy Pattern provides a surrogate or placeholder object that controls access to another object.

The proxy and the real object implement the same interface, allowing the proxy to stand in place of the real object.

---

## 2. Intent

- Control access to an object  
- Delay object creation (lazy loading)  
- Add security checks  
- Add logging or caching  
- Represent remote objects  

It acts as an intermediary between the client and the real object.

---

## 3. Problem It Solves

### 3.1 Expensive Object Creation

If object creation is costly (for example, loading an image from disk or establishing a database connection):

Without Proxy:
- The object loads immediately.
- Resources are wasted if the object is never used.

With Proxy:
- Creation is delayed until it is actually required.

---

### 3.2 Access Control

You may require:

- Authentication  
- Authorization  
- Permission validation  

The proxy performs validation checks before delegating execution to the real object.

---

### 3.3 Remote Access

In distributed systems:

- The real object may exist on another machine.
- The proxy handles network communication and forwards requests.

---

## 4. Structure

### 4.1 Subject Interface

```java
interface Image {
    void display();
}
```

Defines the common contract for both Proxy and RealSubject.

---

### 4.2 Real Subject

```java
class RealImage implements Image {

    private String fileName;

    public RealImage(String fileName) {
        this.fileName = fileName;
        loadFromDisk();
    }

    private void loadFromDisk() {
        System.out.println("Loading image from disk: " + fileName);
    }

    public void display() {
        System.out.println("Displaying image: " + fileName);
    }
}
```

This is the heavy object that performs the real work.

---

### 4.3 Proxy Class

```java
class ProxyImage implements Image {

    private RealImage realImage;
    private String fileName;

    public ProxyImage(String fileName) {
        this.fileName = fileName;
    }

    public void display() {

        if (realImage == null) {
            realImage = new RealImage(fileName);
        }

        realImage.display();
    }
}
```

The proxy controls creation and access before delegating to the real object.

---

### 4.4 Client

```java
public class Main {

    public static void main(String[] args) {

        Image image = new ProxyImage("photo.png");

        image.display(); // Loads and displays
        image.display(); // Only displays
    }
}
```

The client is unaware whether it is interacting with the Proxy or the RealImage.

---

## 5. Types of Proxy

### 5.1 Virtual Proxy
- Lazy initialization
- Creates object only when needed

### 5.2 Protection Proxy
- Access control
- Checks permissions before delegation

### 5.3 Remote Proxy
- Represents object in another address space
- Handles network communication

### 5.4 Smart Proxy
- Adds logging
- Adds caching
- Manages reference counting

---

## 6. Call Flow

```
Client → Proxy → RealSubject
```

The proxy:

- Intercepts the call  
- Performs additional logic  
- Delegates to the real object  

---

## 7. Difference from Decorator

| Proxy | Decorator |
|--------|-----------|
| Controls access | Adds behavior |
| Usually transparent | Enhances functionality |
| Same interface | Same interface |
| Focus: control | Focus: extension |
| Typically one-to-one | Can stack multiple decorators |

Decorator modifies behavior.  
Proxy controls access.

---

## 8. Difference from Adapter

| Proxy | Adapter |
|--------|----------|
| Same interface | Different interface |
| Controls access | Converts interface |
| Client unaware of proxy | Client expects Target interface |

Adapter solves compatibility issues.  
Proxy solves control and access problems.

---

## 9. Conclusion

The Proxy Pattern provides controlled access to an object while maintaining the same interface. It allows additional logic such as lazy loading, security checks, logging, or remote handling without modifying the real object.

It promotes:

- Encapsulation  
- Controlled interaction  
- Transparent substitution  
- Open/Closed Principle compliance  
