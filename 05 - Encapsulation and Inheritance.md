# Encapsulation

Encapsulation is a way of data hiding.

- All data members (fields) of a class should be hidden.
- No interface members should be hidden.

Encapsulation is achieved by making all data members private and providing public methods to access them.

```java
public class Account {
    private String accountNumber; // account number cannot be changed
    private double balance; // balance cannot be negative

    public Account(String accountNumber) {
        this.accountNumber = accountNumber;
        this.balance = 0;
    }

    public void deposit(double amount) {
        balance += amount;
    }

    public void withdraw(double amount) {
        if (amount <= balance) {
            balance -= amount;
        } else {
            System.out.println("Insufficient funds");
        }
    }

    public String getAccountNumber() {
        return accountNumber;
    }

    public double getBalance() {
        return balance;
    }
}
```

## Benefits

- Ensures that changes to the internal representation of a class do not affect the code that uses the class.
- Controls/validates the modification of data.
- Reduces complexity.

## Access Modifiers

- `private`: Only accessible within the class.
- `protected`: Accessible within the class and its subclasses.
- `public`: Accessible from anywhere.
- `default`: Accessible within the same package.

<img src="images/Access Modifiers.png" alt="Access Modifiers" width="500"/>

# Inheritance

Inheritance is a way of reusing code and defining structure in a hierarchical manner.

## Subclass

- A class can inherit fields and methods from another class.
- The class that inherits is called a **subclass**.
- The class that is inherited from is called a **superclass**.
- A subclass inherits all the public and protected members of the superclass.
- **Only one superclass can be inherited.**

### Accessing

- Inherited members can be accessed as if they were defined in the subclass.
- `super`: Refers to the superclass and can be used to access superclass constructors, fields and methods.

### Overriding

- A subclass can override a method of its superclass by defining a method with the same signature.

### Hiding

- **Hide a field** by defining a field with the same name.
- **Hide a static method** by defining a static method with the same name.

### Constructors

- If a superclass constructor is called, it must be the first statement in the subclass constructor.
- If a superclass constructor is not explicitly called, the _default constructor_ is called.
- If a superclass does not have a default constructor, the subclass constructor must call a superclass constructor.

```java
public class Animal {
    private String name;

    public Animal(String name) {
        this.name = name;
    }

    public void eat() {
        System.out.println(name + " is eating");
    }
}

public class Dog extends Animal {
    public Dog(String name) {
        super(name);
    }

    public void bark() {
        System.out.println("Woof! Woof!");
    }
}
```

## Interfaces

Interfaces are used to specify the public API. It defines a set of methods that a class must implement.

- An interface can have methods and constants.
    - Methods are by default abstract and public
    - Attributes are by default public, static and final
- A class can **implement multiple interfaces.**
- An interface can **extend multiple interfaces.**

```java
public interface Ball {
    void fetch();
}

public interface ElasticBody {
    void Bounce();
}

public class RubberBall implements Ball, ElasticBody {
    public void fetch() {
        System.out.println("Fetching the ball");
    }

    public void Bounce() {
        System.out.println("Bouncing the ball");
    }
}
```
