What is a Unit Test
===================

I used to feel that a unit was the smallest possible part of a code base (a method, really). But in the past couple of years I've changed my mind. Here's how I define a unit test, as of October 2011:

A unit test is an automated piece of code that invokes a unit of work in the system and then checks a single assumption about the behavior of that unit of work.

A unit of work is a single logical functional use case in the system that can be invoked by some public interface (in most cases). A unit of work can span a single method, a whole class or multiple classes working together to achieve one single logical purpose that can be verified.

Characteristics of good unit tests:
-----------------------------------

-   Able to be fully automated
-   Has full control over all the pieces running (Use mocks or stubs to achieve this isolation when needed)
-   Can be run in any order if part of many other tests
-   Runs in memory (no DB or File access, for example)
-   Consistently returns the same result
-   Runs fast
-   Tests a single logical concept in the system
-   Readable
-   Maintainable
-   Trustworthy (when you see its result, you don't need to debug the code just to be sure)

I consider any test that doesn't live up to all these as an integration test and put it in its own integration tests project.

-   Ray Osherove, the art of Unit Testing

From Pragmatic Unit Testing
===========================

<http://media.pragprog.com/titles/utj/StandaloneSummary.pdf>

General Principles
------------------

✷ Test anything that might break ✷ Test everything that does break ✷ New code is guilty until proven innocent ✷ Write at least as much test code as production code ✷ Run local tests with each compile ✷ Run all tests before check-in to repository

Questions to Ask
----------------

✷ If the code ran correctly, how would I know? ✷ How am I going to test this? ✷ What else can go wrong? ✷ Could this same kind of problem happen anywhere else?

SOLID
=====

Robert C. Martin (Uncle Bob)

S - Single Responsibility Principle
-----------------------------------

An object should do exactly one thing, and should be the only object in the codebase that does that one thing. For instance, take a domain class, say an Invoice. The Invoice class should represent the data structure and business rules of an invoice as used in the system. It should be the only class that represents an invoice in the codebase. This can be further broken down to say that a method should have one purpose and should be the only method in the codebase that meets this need.

By following this principle, you increase the testability of your design by decreasing the number of tests you have to write that test the same functionality on different objects, and you also typically end up with smaller pieces of functionality that are easier to test in isolation.

O - Open/Closed Principle
-------------------------

A class should be open to extension, but closed to change. Once an object exists and works correctly, ideally there should be no need to go back into that object to make changes that add new functionality. Instead, the object should be extended, either by deriving it or by plugging new or different dependency implementations into it, to provide that new functionality. This avoids regression; you can introduce the new functionality when and where it is needed, without changing the behavior of the object as it is already used elsewhere.

By adhering to this principle, you generally increase the code's ability to tolerate "mocks", and you also avoid having to rewrite tests to anticipate new behavior; all existing tests for an object should still work on the un-extended implementation, while new tests for new functionality using the extended implementation should also work.

L - Liskov Substitution Principle
---------------------------------

A class A, dependent upon class B, should be able to use any X:B without knowing the difference. This basically means that anything you use as a dependency should have similar behavior as seen by the dependent class. As a short example, say you have an IWriter interface that exposes Write(string), which is implemented by ConsoleWriter. Now you have to write to a file instead, so you create FileWriter. In doing so, you must make sure that FileWriter can be used the same way ConsoleWriter did (meaning that the only way the dependent can interact with it is by calling Write(string)), and so additional information that FileWriter may need to do that job (like the path and file to write to) must be provided from somewhere else than the dependent.

This is huge for writing testable code, because a design that conforms to the LSP can have a "mocked" object substituted for the real thing at any point without changing expected behavior, allowing for small pieces of code to be tested in isolation with the confidence that the system will then work with the real objects plugged in.

I - Interface Segregation Principle
-----------------------------------

An interface should have as few methods as is feasible to provide the functionality of the role defined by the interface. Simply put, more smaller interfaces are better than fewer larger interfaces. This is because a large interface has more reasons to change, and causes more changes elsewhere in the codebase that may not be necessary.

Adherence to ISP improves testability by reducing the complexity of systems under test and of dependencies of those SUTs. If the object you are testing depends on an interface IDoThreeThings which exposes DoOne(), DoTwo() and DoThree(), you must mock an object that implements all three methods even if the object only uses the DoTwo method. But, if the object depends only on IDoTwo (which exposes only DoTwo), you can more easily mock an object that has that one method.

D - Dependency Inversion Principle
----------------------------------

Concretions and abstractions should never depend on other concretions, but on abstractions. This principle directly enforces the tenet of loose coupling. An object should never have to know what an object IS; it should instead care what an object DOES. So, the use of interfaces and/or abstract base classes is always to be preferred over the use of concrete implementations when defining properties and parameters of an object or method. That allows you to swap one implementation for another without having to change the usage (if you also follow LSP, which goes hand in hand with DIP).

Handy Dandy Acronyms
====================

AAA
---

1.  Arrange
2.  Act
3.  Assert

Right-BICEP
-----------

-   Right: Are the results right?
-   B: are all the boundary conditions correct?
-   I: can you check the inverse relationships?
-   C: can you cross-check results using other means?
-   E: can you force error conditions to happen?
-   P: are performance characteristics within bounds?

CORRECT
-------

-   Conformance - does the value conform to an expected format?
-   Ordering - is the set of values ordered or unordered as appropriate?
-   Range - is the value within reasonable minimum and maximum values?
-   Reference - does the code reference anything external that isn't under direct control of the code itself?
-   Existence - does the value exist (e.g. is not null, non-zero, present in a set)?
-   Cardinality - are there exactly enough values?
-   Time (absolute and relative) - is everything happening in order? At the right time? In time?

A TRIP
------

✷ Automatic ✷ Thorough ✷ Repeatable ✷ Independent ✷ Professional
