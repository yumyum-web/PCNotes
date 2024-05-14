# Structural Design Patterns

## Introduction

- Structural design patterns are design patterns that deals with assembling objects and classes into larger structures.
- Structural design patterns are composed of two dominant ideas:
  - Simplify the structure by identifying relationships.
  - Make the structure flexible by allowing the relationships to be easily changed.

## Adapter

- An adapter class implements the target interface and wraps an object with a different interface.
- Primarily used when an existing class needs an object with a different interface than the one currently implemented.

## Bridge

- The bridge pattern decouples an abstraction from its implementation so that the two can vary independently.
- **Abstraction:** the high-level interface. clients instantiate and interact with the abstraction.
- **Implementation:** the low-level interface. Abstraction interacts with the implementation.

## Composite

- When we can construct a **tree-like structure** with objects of the same interface, it is called a composite pattern.
- This structure must follow a logical hierarchy.
- When a method is called on any node, it should **account for its children** nodes too.

## Decorator

- A decorator class is used to add new functionality to an existing object by decorating (wrapping) it.
- The decorator class implements the same interface as the object it decorates.
- Decorating vs subclassing:
  - Subclassing adds functionality at compile time.
  - Decorating adds functionality at runtime.
  - Subclassing can lead to a _class explosion._ decorators can be stacked.
- **Class explosion** is a problem that occurs when a class has too many subclasses, which can make the class hierarchy
  difficult to understand and maintain.

## Facade

- A facade class provides a simple interface to a complex subsystem.
- It can loosen the coupling of the client and the subsystem.
- Provides boilerplate code to simplify the client's interaction with the subsystem.

## Flyweight

- The flyweight pattern is used to reduce the memory usage or computational expenses by only storing the intrinsic state
  in shared flyweight objects.
- **Intrinsic state:** Common state for all objects. This is stored in the flyweight object.
- **Extrinsic state:** State that varies between objects. This is stored in the client object and passed to the
  flyweight object when needed.

## Proxy

- A proxy class provides a surrogate or placeholder object to control access to a subject.
- This subject can be another object, a network connection, a large object in memory, a file, etc.
- The proxy implements an interface for interacting with the subject as if it is an object in memory.
- A subject object is not needed to be passed when initiating a proxy object (It could get created inside the proxy).
