# Abstraction

- Abstraction is the concept of hiding the complex implementation details and showing only the necessary features of the
  object.
- Abstraction is achieved by using abstract classes and interfaces.

## Abstract Classes

- Used when a parent class does not have enough information to provide a complete implementation.
- Cannot be instantiated.
- Can have abstract methods (methods without a body).
- Subclasses must implement all abstract methods, or they must be declared as abstract.

```java
public abstract class Animal {
    public abstract void eat();
}

public class Dog extends Animal {
    public void eat() {
        System.out.println("Dog is eating");
    }
}
```

## Interfaces

- Used to specify a public API.
- Defines a set of methods that a class must implement.

```java
import java.util.LinkedList;
import java.util.Queue;

public class ToDoList {
    public ToDoList() {
        Queue<String> tasks = new LinkedList<>(); // tasks only concerns with queue functionality
    }
}
```

### Marker Interfaces

- Interfaces without any methods.
- Used to mark a class as having a special property.
    - `Serializable`
    - `Cloneable`
    - `Remote`

# Polymorphism

- Polymorphism is the ability of an object to take many forms.
- A subclass object can be assigned to a superclass reference.

## Binding

### Static Binding (Method Overloading)

- Defining multiple methods with the same name but different signatures is called method overloading.
- Selection of the overload to be executed is done at **compile-time**, based on method signature and reference type.

### Dynamic Binding (Method Overriding)

- The reference type determines which methods can be called, but the concrete class determines which method
  implementation is executed.
- This is **runtime** polymorphism.

### Example

```java
public class Animal {
    public void eat(String food) {
        eat(food, 1); // Cannot guarantee that Animal.eat(String, int) will be called, could be overridden.
    }

    public void eat(String food, int quantity) {
        System.out.println("Animal is eating " + quantity + " " + food);
    }
}

public class Dog extends Animal {
    public void eat() {
        eat("meat"); // Cannot guarantee that Animal.eat(String) will be called, could be overridden.
    }

    public void eat(String food, int quantity) { // Overrides Animal.eat(String, int)
        System.out.println("Dog is eating " + quantity + " " + food);
    }

    public void bark() {
        System.out.println("Woof! Woof!");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal animal1 = new Animal();
        animal1.eat("grass"); // Animal is eating 1 grass

        Animal animal2 = new Dog();
        animal2.eat(); // Dog is eating 1 meat
        animal2.eat("pizza"); // Dog is eating 1 pizza
        animal2.eat("lasagna", 2); // Dog is eating 2 lasagna
        // animal.bark(); -> Compile-time error: bark() is not defined in Animal
    }
}
```

## Casting

- Converting an object of one type to another type.

### Upcasting

- Converting a subclass object to a superclass reference. Mostly done implicitly.
- This occurs at compile time.

### Downcasting

- Explicitly converting a superclass reference to a subclass object.
- This occurs at runtime.

```java
class Cloud {
}

class Rock {
}

final class Granite extends Rock { // final classes cannot be extended
}

interface Movable {
    void move();
}

public class Main {
    public static void main(String[] args) {
        Rock rock1 = new Rock();
        // rock1 is a Rock reference, Granite is a subclass of Rock
        // Granite granite1 = (Granite) rock1; -> Runtime error: ClassCastException

        Rock rock2 = new Rock();
        // rock2 is a Rock reference, Cloud is not a subclass of Rock.
        // Cloud cloud1 = (Cloud) rock2; -> Compilation error: incompatible types

        Rock rock3 = new Granite();
        // rock3 could be a subclass of Rock that implements Movable.
        // Movable movable1 = (Movable) rock3; -> Runtime error: ClassCastException

        Granite granite1 = new Granite();
        // Granite is a final class, it cannot have subclasses that implement Movable.
        // Movable movable2 = (Movable) granite1; -> Compilation error: incompatible types
    }
}
```