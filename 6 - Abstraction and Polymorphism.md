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

## Polymorphic objects

- An object can be of multiple types.
- A subclass object can be assigned to a superclass reference.
- This is runtime polymorphism.

```java
public class Animal {
    public void eat() {
        System.out.println("Animal is eating");
    }
}

public class Dog extends Animal {
    public void eat() {
        System.out.println("Dog is eating");
    }

    public void bark() {
        System.out.println("Woof! Woof!");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal animal = new Dog();
        animal.eat(); // Dog is eating
        animal.bark(); // Error: bark method is not defined in Animal class
    }
}
```

## Dynamic Binding (Method Overloading)

- Selection of the method to be executed is done at runtime, based on method name and arguments.

```java
public class Dog {
    public void eat() {
        System.out.println("Dog is eating");
    }

    public void eat(String food) {
        System.out.println("Dog is eating " + food);
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.eat(); // Dog is eating
        dog.eat("meat"); // Dog is eating meat
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
public class Animal {
    public void eat() {
        System.out.println("Animal is eating");
    }

    public Animal getAnimal() {
        return this;
    }
}

public class Dog extends Animal {

    public void bark() {
        System.out.println("Woof! Woof!");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal animal = new Dog().getAnimal();
        ((Dog) animal).bark(); // Woof! Woof!
    }
}
```