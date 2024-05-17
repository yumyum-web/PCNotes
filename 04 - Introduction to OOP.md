# Introduction to Object-Oriented Programming

## Procedural Programming

- Break down a programming task into a collection of variables, data structures, and subroutines.
- Uses `procedures` to operate on data structures.

## Object-Oriented Programming

- Break down a programming task into `objects`.
- Bundles the procedures and data structures together, so an "object", which is an instance of a class, operates on
  its "own" data structure.
- Objects can be used effectively to represent entities that have,
    - **State:** descriptive characteristics
    - **Behaviors:** what it can do (might change its state)

## Classes

A class is a blueprint for creating objects. It defines the attributes and methods that an object can have.

- **Attributes:** contain current state of an object.
- **Methods:** define the behaviors of an object.
- **Messages:** requests to an object to perform an action. In java messages are sent by **calling methods.**

### Constructor

A constructor is a special method that is called when an object is created. It is used to initialize the object's
attributes.

### `this` Keyword

- As a reference to the current object.
    - To differentiate between instance variable and local.
    - To invoke current class method explicitly.
    - To return current instance of the class.
    - As a parameter in constructor/method call.
- In **constructor chaining.**

```java
public class Person {
    String name;
    int age;
    int maturity;

    public Person() {
        // Constructor chaining.
        this("John Doe", 30);
    }

    public Person(String name, int age) {
        // Differentiate between instance variable and local
        this.name = name;
        this.age = age;
        // Invoke current class method explicitly
        this.setMaturity();
    }

    private void setMaturity() {
        this.maturity = this.age / 10;
    }

    public void addName(String name) {
        this.name = this.name + name;
    }

    public Person getPerson() {
        // Return current instance of the class
        return this;
    }
}
```

### Overloading

- Defining multiple methods with the same name but different signatures. (Within the same class)

### Static Members (Class Members)

- Belong to the class, not to the object.
- Static members can be accessed without creating an object.
- Static methods can't access/invoke non-static members.
- Static methods can't use `this`, `super` keywords.

```java
public class Math {
    public static int add(int a, int b) {
        return a + b;
    }
}
```

### Initialization Blocks

- **Instance Initialization Block:**
    - Executed when the object is created, before the constructor.
    - Used to reuse constructor code in multiple constructors.

- **Static Initialization Block:**
    - Executed when the class is loaded.
    - Used to initialize static members.
    - Can be used to initialize static final variables.
    - Can't access/invoke non-static members.
    - Can't use `this`, `super` keywords.

```java
public class Math {
    public static final double PI;
    private int x;

    static {
        PI = 3.14;
    }

    {
        x = 10;
        System.out.println("Initialization block");
    }
}
```
