# 4 Pillars of Object Oriented Programming
## Abstraction
Abstraction is a process of exposing essential features of an entity by hiding the other irrelevant details. Abstraction mainly reduces complexity and increases efficiency. An entity can have multiple abstractions.

## Encapsulation
Encapsulation is the process of putting data and the operations (functions) that can be performed on that data into a single container called class. Now, any programmer can use this class without knowing how it is implemented. Due to encapsulation, data is insulated, thus not directly accessible from the outside world. This is known as Data Hiding.

Remember, Encapsulation is not data hiding, but, Encapsulation leads to data hiding.

## Inheritance
In a nutshell, inheritance is a process of creating new class from the existing one. The new class may have some additional properties and functionalitiy.

## Polymorphism
Poly means many and Morphs means forms. Polymorphism refers to the ability to take multiple forms and it allows us to invoke derived class methods through a base class reference during run-time.

# DRY, YAGNI & KISS Principles
- Don't Repeat Yourself
- You Aren't Going to Need It
- Keep It Simple Stupid


# SOLID Principles
## Single responsibility principle
a class should have only a single responsibility (i.e. only one potential change in the software's specification should be able to affect the specification of the class)

## Open/closed principle
software entities should be open for extension, but closed for modification.

## Liskov substitution principle
objects in a program should be replaceable with instances of their subtypes without altering the correctness of that program.

## Interface segregation principle
many client-specific interfaces are better than one general-purpose interface.

## Dependency inversion principle
one should Depend upon Abstractions. Do not depend upon concretions.

# GRASP Principles
General Responsibility Assignment Software Patterns (or Principles), abbreviated GRASP, consist of guidelines for assigning responsibility to classes and objects in object-oriented design.

## Controller
The Controller pattern assigns the responsibility of dealing with system events to a non-UI class that represents the overall system or a use case scenario. A Controller object is a non-user interface object responsible for receiving or handling a system event.

A use case controller should be used to deal with all system events of a use case, and may be used for more than one use case (for instance, for use cases Create User and Delete User, one can have a single UserController, instead of two separate use case controllers).

It is defined as the first object beyond the UI layer that receives and coordinates ("controls") a system operation. The controller should delegate the work that needs to be done to other objects; it coordinates or controls the activity. It should not do much work itself. The GRASP Controller can be thought of as being a part of the Application/Service layer \[2\] (assuming that the application has made an explicit distinction between the application/service layer and the domain layer) in an object-oriented system with Common layers in an information system logical architecture.

## Creator
Creation of objects is one of the most common activities in an object-oriented system. Which class is responsible for creating objects is a fundamental property of the relationship between objects of particular classes.

In general, a class B should be responsible for creating instances of class A if one, or preferably more, of the following apply:

``` example
Instances of B contain or compositely aggregate instances of A
Instances of B record instances of A
Instances of B closely use instances of A
Instances of B have the initializing information for instances of A and pass it on creation.
```

## High Cohesion
High Cohesion is an evaluative pattern that attempts to keep objects appropriately focused, manageable and understandable. High cohesion is generally used in support of Low Coupling. High cohesion means that the responsibilities of a given element are strongly related and highly focused. Breaking programs into classes and subsystems is an example of activities that increase the cohesive properties of a system. Alternatively, low cohesion is a situation in which a given element has too many unrelated responsibilities. Elements with low cohesion often suffer from being hard to comprehend, hard to reuse, hard to maintain and averse to change.\[3\]

## Indirection
The Indirection pattern supports low coupling (and reuse potential) between two elements by assigning the responsibility of mediation between them to an intermediate object. An example of this is the introduction of a controller component for mediation between data (model) and its representation (view) in the Model-view-controller pattern. Information Expert See also: Information hiding

## Information Expert
(also Expert or the Expert Principle) is a principle used to determine where to delegate responsibilities. These responsibilities include methods, computed fields, and so on.

Using the principle of Information Expert, a general approach to assigning responsibilities is to look at a given responsibility, determine the information needed to fulfill it, and then determine where that information is stored.

Information Expert will lead to placing the responsibility on the class with the most information required to fulfill it.\[4\]

## Low Coupling
Low Coupling is an evaluative pattern, which dictates how to assign responsibilities to support:

``` example
lower dependency between the classes,
change in one class having lower impact on other classes,
higher reuse potential.
```

## Polymorphism
According to Polymorphism, responsibility of defining the variation of behaviors based on type is assigned to the types for which this variation happens. This is achieved using polymorphic operations.

## Protected Variations
The Protected Variations pattern protects elements from the variations on other elements (objects, systems, subsystems) by wrapping the focus of instability with an interface and using polymorphism to create various implementations of this interface.

## Pure Fabrication
A Pure Fabrication is a class that does not represent a concept in the problem domain, specially made up to achieve low coupling, high cohesion, and the reuse potential thereof derived (when a solution presented by the Information Expert pattern does not). This kind of class is called "Service" in Domain-driven design.

# Design Patterns
## Criticism
The concept of design patterns has been criticized in several ways.

The design patterns may just be a sign of some missing features of a given programming language (Java or C++ for instance). Peter Norvig demonstrates that 16 out of the 23 patterns in the Design Patterns book (that is primarily focused on C++) are simplified or eliminated (via direct language support) in Lisp or Dylan. Related observations were made by Hannemann and Kiczales who implemented several of the 23 design patterns using an aspect-oriented programming language (AspectJ) and showed that code-level dependencies were removed from the implementations of 17 of the 23 design patterns and that aspect-oriented programming could simplify the implementations of design patterns. See also Paul Graham's essay "Revenge of the Nerds".

*Moreover, inappropriate use of patterns may unnecessarily increase complexity.*

## Creational
**Abstract factory** Provide an interface for creating families of related or dependent objects without specifying their concrete classes.

**Builder** Separate the construction of a complex object from its representation, allowing the same construction process to create various representations.

**Factory method** Define an interface for creating a single object, but let subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses (dependency injection\[16\]).

**Lazy initialization** Tactic of delaying the creation of an object, the calculation of a value, or some other expensive process until the first time it is needed. This pattern appears in the GoF catalog as "virtual proxy", an implementation strategy for the Proxy pattern.

**Multiton** Ensure a class has only named instances, and provide a global point of access to them.

**Object pool** Avoid expensive acquisition and release of resources by recycling objects that are no longer in use. Can be considered a generalisation of connection pool and thread pool patterns.

**Prototype** Specify the kinds of objects to create using a prototypical instance, and create new objects by copying this prototype.

**Resource acquisition is initialization** Ensure that resources are properly released by tying them to the lifespan of suitable objects.

**Singleton** Ensure a class has only one instance, and provide a global point of access to it.


## Structural
**Adapter or Wrapper or Translator** Convert the interface of a class into another interface clients expect. An adapter lets classes work together that could not otherwise because of incompatible interfaces. The enterprise integration pattern equivalent is the translator.

**Bridge** Decouple an abstraction from its implementation allowing the two to vary independently.

**Composite** Compose objects into tree structures to represent part-whole hierarchies. Composite lets clients treat individual objects and compositions of objects uniformly.

**Decorator** Attach additional responsibilities to an object dynamically keeping the same interface. Decorators provide a flexible alternative to subclassing for extending functionality.

**Facade** Provide a unified interface to a set of interfaces in a subsystem. Facade defines a higher-level interface that makes the subsystem easier to use.

**Flyweight** Use sharing to support large numbers of similar objects efficiently.

**Front Controller** The pattern relates to the design of Web applications. It provides a centralized entry point for handling requests.

**Module** Group several related elements, such as classes, singletons, methods, globally used, into a single conceptual entity.

**Proxy** Provide a surrogate or placeholder for another object to control access to it.

**Twin** Twin allows modeling of multiple inheritance in programming languages that do not support this feature.


## Behavioral
**Blackboard** Artificial intelligence pattern for combining disparate sources of data

**Chain of responsibility** Avoid coupling the sender of a request to its receiver by giving more than one object a chance to handle the request. Chain the receiving objects and pass the request along the chain until an object handles it.

**Command** Encapsulate a request as an object, thereby letting you parameterize clients with different requests, queue or log requests, and support undoable operations.

**Interpreter** Given a language, define a representation for its grammar along with an interpreter that uses the representation to interpret sentences in the language.

**Iterator** Provide a way to access the elements of an aggregate object sequentially without exposing its underlying representation.

**Mediator** Define an object that encapsulates how a set of objects interact. Mediator promotes loose coupling by keeping objects from referring to each other explicitly, and it lets you vary their interaction independently.

**Memento** Without violating encapsulation, capture and externalize an object's internal state allowing the object to be restored to this state later.

**Null object** Avoid null references by providing a default object.

**Observer or Publish/subscribe** Define a one-to-many dependency between objects where a state change in one object results in all its dependents being notified and updated automatically.

**Servant** Define common functionality for a group of classes.

**Specification** Recombinable business logic in a Boolean fashion.

**State** Allow an object to alter its behavior when its internal state changes. The object will appear to change its class.

**Strategy** Define a family of algorithms, encapsulate each one, and make them interchangeable. Strategy lets the algorithm vary independently from clients that use it.

**Template method** Define the skeleton of an algorithm in an operation, deferring some steps to subclasses. Template method lets subclasses redefine certain steps of an algorithm without changing the algorithm's structure.

**Visitor** Represent an operation to be performed on the elements of an object structure. Visitor lets you define a new operation without changing the classes of the elements on which it operates.


## Concurrency Patterns
**Active Object** Decouples method execution from method invocation that reside in their own thread of control. The goal is to introduce concurrency, by using asynchronous method invocation and a scheduler for handling requests.

**Balking** Only execute an action on an object when the object is in a particular state.

**Binding properties** Combining multiple observers to force properties in different objects to be synchronized or coordinated in some way.

**Block chain** Decentralized way to store data and agree on ways of processing it in a Merkle tree, optionally using Digital signature for any individual contributions.

**Double-checked locking** Reduce the overhead of acquiring a lock by first testing the locking criterion (the 'lock hint') in an unsafe manner; only if that succeeds does the actual locking logic proceed.

Can be unsafe when implemented in some language/hardware combinations. It can therefore sometimes be considered an anti-pattern.

**Event-based asynchronous** Addresses problems with the asynchronous pattern that occur in multithreaded programs.

**Guarded suspension** Manages operations that require both a lock to be acquired and a precondition to be satisfied before the operation can be executed.

**Join** Join-pattern provides a way to write concurrent, parallel and distributed programs by message passing. Compared to the use of threads and locks, this is a high level programming model.

**Lock** One thread puts a "lock" on a resource, preventing other threads from accessing or modifying it.

**Messaging design pattern (MDP)** Allows the interchange of information (i.e. messages) between components and applications.

**Monitor object** An object whose methods are subject to mutual exclusion, thus preventing multiple objects from erroneously trying to use it at the same time.

**Reactor** A reactor object provides an asynchronous interface to resources that must be handled synchronously.

**Read-write lock** Allows concurrent read access to an object, but requires exclusive access for write operations.

**Scheduler** Explicitly control when threads may execute single-threaded code.

**Thread pool** A number of threads are created to perform a number of tasks, which are usually organized in a queue. Typically, there are many more tasks than threads. Can be considered a special case of the object pool pattern.

**Thread-specific storage** Static or "global" memory local to a thread.

# Lift
- Locate code quickly
- Identify the code at a glance
- Flattest structure you can keep
- Try to be DRY
