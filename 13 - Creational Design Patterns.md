# Creational Design Patterns

## Introduction

- Creational design patterns are design patterns that deal with object creation mechanisms, trying to create objects in
  a manner suitable to the situation.
- Creational design patterns are composed of two dominant ideas:
    - Encapsulate knowledge about which concrete classes the system uses.
    - Hide how instances of these classes are created and combined.

## Abstract Factory

- The class that needs to create objects uses a factory object which was passed to it (Possibly as a constructor
  parameter).
- The factory object is an instance of an **Abstract Factory** interface.

## Builder

- The class that needs to create objects initializes a builder object and then calls methods on the builder object step
  by step to create the object.
- The builder usually has a method that returns the object after it has been fully constructed.

## Factory Method

- The class that needs to create objects uses _one of its methods_ to create the object.
- The method is either,
    - Abstract and implemented by subclasses.
    - Concrete and may be overridden by subclasses.

## Prototype

- The class that needs to create objects uses a prototype object to create new objects by cloning the **prototype
  object.**
- The prototype object is an instance of a **Prototype** interface.
- Cloning is much cheaper than initializing a new object.

## Singleton

- The class that needs to create the object uses a static method in the **Singleton class** to get the instance of the
  class.
- Allows accessing the single instance from anywhere in the application.
- Promotes a global state in the application.
