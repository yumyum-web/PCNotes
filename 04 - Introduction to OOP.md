# Introduction to Object-Oriented Programming

Objects can be used effectively to represent entities that have,

- **State:** descriptive characteristics
- **Behaviors:** what it can do

## Classes

A class is a blueprint for creating objects. It defines the attributes and methods that an object can have.

- **Attributes:** contain current state of an object.
- **Methods:** define the behaviors of an object.
- **Messages:** requests to an object to perform an action.

### Constructor

A constructor is a special method that is called when an object is created. It is used to initialize the object's
attributes.

### `this` Keyword

- As a reference to the current object.
- For **constructor chaining.**

```java
public class Person {
    String name;
    int age;
    int maturity;

    public Person() {
        this("John Doe", 30);
    }

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
        this.setMaturity();
    }

    private void setMaturity() {
        this.maturity = this.age / 10;
    }

    public void addName(String name) {
        this.name = this.name + name;
    }

    public Person getPerson() {
        return this;
    }
}
```

### Overloading

- Defining multiple methods with the same name but different signatures.

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

```java
public class Math {
    public static final int PI;
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
