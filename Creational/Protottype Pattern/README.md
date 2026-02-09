# Prototype Pattern

## 1. Definition

The **Prototype Pattern** is used when object creation is expensive or complex.  
Instead of creating new objects from scratch, new objects are created by **cloning an existing prototype instance**.

---

## 2. Intent

- Avoid repeated expensive object creation  
- Improve performance when initialization is heavy  
- Allow runtime object duplication  
- Reduce subclass explosion  
- Hide complex construction logic from the client  

---

## 3. Problem It Solves

Consider a game where creating an NPC requires:

- Database calls  
- Complex calculations  
- Heavy initialization logic  

If every NPC instance is created using `new`, the setup cost is repeated multiple times.

### Prototype Solution

1. Create one fully initialized template object  
2. Clone it whenever a new instance is required  
3. Tweak only the necessary properties  

This saves computation time and improves efficiency.

---

## 4. Structure

- **Prototype Interface** → declares `clone()`  
- **Concrete Prototype** → implements cloning logic  
- **Client** → clones instead of instantiating  

---

## 5. Implementation

### Prototype Interface

```java
interface Cloneable {
   Cloneable clone();
}
```

---

### Concrete Prototype – NPC

```java
class NPC implements Cloneable {

   public String name;
   public int health;
   public int attack;
   public int defense;
   
   public NPC(String name, int health, int attack, int defense) {
       // heavy initialization
       // database calls
       // complex calculations
       this.name = name; 
       this.health = health; 
       this.attack = attack; 
       this.defense = defense;
       System.out.println("Setting up template NPC '" + name + "'");
   }
   
   // Copy constructor used by clone()
   public NPC(NPC other) {
       name = other.name;
       health = other.health;
       attack = other.attack;
       defense = other.defense;
       System.out.println("Cloning NPC '" + name + "'");
   }
   
   public Cloneable clone() {
       return new NPC(this);
   }
   
   public void describe() {
       System.out.println("NPC " + name + " [HP=" + health 
           + " ATK=" + attack + " DEF=" + defense + "]");
   }
   
   // Setters for customization
   public void setName(String n) { name = n; }
   public void setHealth(int h) { health = h; }
   public void setAttack(int a) { attack = a; }
   public void setDefense(int d){ defense = d; }
}
```

---

### Client

```java
public class PrototypePattern {

   public static void main(String[] args) {

       // 1. Create one heavy template object
       NPC alien = new NPC("Alien", 30, 5, 2);
       
       // 2. Clone and reuse
       NPC alienCopied1 = (NPC) alien.clone();
       alienCopied1.describe();
       
       NPC alienCopied2 = (NPC) alien.clone();
       alienCopied2.setName("Powerful Alien");
       alienCopied2.setHealth(50);
       alienCopied2.describe();
   }
}
```

---

## 6. Execution Flow

1. Template NPC is created once.  
2. `clone()` method calls the copy constructor.  
3. New objects are created without re-running heavy initialization.  
4. Cloned objects can be modified independently.  

---

## 7. Key Insight

- The heavy constructor runs **only once**.  
- Clones:
  - Copy existing state  
  - Avoid repeating setup logic  
  - Can be customized after cloning  

---

## 8. Shallow vs Deep Copy

Your current implementation performs a **shallow copy** because:

- All fields are primitive or immutable.

If the object contained:

- Lists  
- Other objects  
- References  

Then **deep cloning** would be required to avoid shared references.

---

## 9. Difference From Factory Pattern

| Aspect      | Factory Pattern | Prototype Pattern |
|------------|------------------|------------------|
| Creation Style | Creates new objects from scratch | Copies an existing object |
| Focus | Creation logic delegation | Object duplication |
| Initialization Cost | Repeated each time | Heavy setup done once |

---

## 10. Conclusion

The **Prototype Pattern** improves performance by avoiding repeated expensive initialization.  

It allows:

- Dynamic object creation through cloning  
- Greater flexibility  
- Reduced construction overhead  

Especially useful in systems where objects are **heavy to create**.
