# Behavioral Design Patterns

## Introduction

- Behavioral design patterns are design patterns that deal with the interaction between objects.
- Behavioral design patterns are composed of two dominant ideas:
    - Simplify the communication between objects.
    - Define how objects interact with each other.

## Chain of Responsibility

- The chain of responsibility pattern is used to pass a request along a chain of handlers.
- Each handler decides either to process the request or call the next handler in the chain.
- The chain could be compiled or dynamic.
- The chain can be implemented as a linked list or a tree.
- The client is unaware of the chain structure. It's only aware of how to send a request to the first handler.

## Command

- The command pattern is used to encapsulate a request as an `Command` object.
- The `Command` object have,
    - A receiver object that knows how to perform the action.
    - An `execute` method that calls the receiver's action.
- The client creates a `Command` object and passes it to an invoker object.
- The invoker object calls the `execute` method on the `Command` object when needed.
- The invoker is decoupled from the receiver.

## Interpreter

- The interpreter pattern is used to define a grammar for interpreting a language and provide an interpreter for the
  grammar.
- The grammar is defined using a class hierarchy.
- The interpreter pattern is used in compilers, interpreters, and regular expressions.
- The interpreter pattern is not commonly used in modern software development.

## Iterator

- The iterator pattern is used to provide a way to iterate (or enumerate) over an aggregate object without exposing the
  underlying representation.
- **Aggregate object:** An object that contains other objects.
- That object implements methods to create iterators.

## Mediator

- The mediator pattern is used to define an object that encapsulates how objects interact.
- The mediator object knows how to communicate with other objects.
- An object can invoke a method on the mediator object, and the mediator object will call the appropriate method on the
  other objects.
- The mediator pattern is used to reduce the coupling between objects.

## Memento

- The memento pattern is used to capture the state of an object and store it in a memento object.
- **Originator:** The object whose state needs to be saved.
- **Memento:** The object that stores the state of the originator. Its class is private to the originator.
- **Caretaker:** The object that manages the memento objects.

## Observer

- The observer pattern is used to define a one-to-many dependency between objects without making the objects tightly
  coupled.
- When the state of the `Observable` object changes, all the Observer `objects` are notified.
- These observers can be added or removed at runtime.
- Commonly used in event-driven systems, and distributed systems.

## State

- The state pattern is used to define a state machine for an object.
- **State-machine:** A system that can be in one of a finite number of states at any given time.
- A `Context` object has state-related fields and a reference to a `State` object.
- When invoking a transition method on the context object, the relevant method in the state object is called.
- The state object has a reference to the context.

## Strategy

- The strategy pattern is used to define a family of strategies (algorithms), encapsulate each one, and make them
  interchangeable.
- The client set which strategy to use at runtime (It's like changing a method at runtime).

## Template Method

- The template method pattern is used to define an algorithm in a method, using possibly abstract helper methods.
- These helper methods can be overridden by subclasses to change the behavior of the algorithm.
- The **template method is declared as final** to prevent subclasses from changing the algorithm's structure.

## Visitor

- The visitor pattern is used when we have to perform an operation on an object based on its class, over a group of
  objects that implement a common interface.
- This pattern is used instead of conditionals with `instanceof`.
- Object classes must have an `accept` method that accepts a visitor object and calls the appropriate method on the
  visitor object passing itself.
- The visitor and the object classes become tightly coupled.