# Introduction to Design Patterns

- The book Design Patterns - Elements of Reusable Object-Oriented Software _by Erich Gamma, Richard Helm, Ralph Johnson
  and John Vlissides_ published in 1994 initiated the concept of design patterns in software development.
- This book is widely known as the **Gang of Four (GoF) book.**
    - Software engineers must program to an interface not an implementation.
    - OOSD must favor object composition over inheritance.
- Design patterns describe how to solve recurring design problems with a best of class design solution.

<img alt="Classification of Design Patterns.png" src="images/Classification of Design Patterns.png"/>

- **Creational Patterns**: Deal with object creation mechanisms, trying to create objects in a manner suitable to the
  situation.
- **Structural Patterns**: Deal with object composition, creating relationships between objects to form larger
  structures.
- **Behavioral Patterns**: Deal with object interaction, how objects communicate with each other.

## Key Concepts

- **Design Patterns**: General reusable solutions to common problems in software design.
- **Object-Oriented Software Design (OOSD)**: A design paradigm based on the concept of objects.


- **Open-Closed Principle**: Software entities should be open for extension but closed for modification.
- **Single Responsibility Principle**: A class should have only one reason to change.
- **Substitution Principle**: Objects of a superclass shall be replaceable with objects of its subclasses without
  affecting the functionality.
- **Interface Segregation Principle**: A client should not be forced to implement an interface that it does not use.
- **Dependency Inversion Principle**: High-level modules should not depend on low-level modules. Both should depend on
  abstractions. Abstractions should not depend on details. Details should depend on abstractions.
- **Composition over Inheritance**: Favor object composition over class inheritance.


- **Composition**: Combining objects or data types into more complex ones.
- **Inheritance**: Mechanism where a new class inherits attributes and methods from an existing class.
- **Encapsulation**: Bundling the data (attributes) and methods (functions) that operate on the data into a single unit.
- **Polymorphism**: The ability of an object to take on many forms.
- **Association**: A relationship where all objects have their lifecycle managed by another object.
- **Aggregation**: A special form of association where objects are assembled or configured together to create a more
  complex object.