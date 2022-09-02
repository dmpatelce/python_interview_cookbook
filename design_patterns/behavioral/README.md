# Behavioral Pattern ##############

Behavioral patterns are about identifying common communication patterns between objects and realizing these patterns. 
Behavioral patterns are Chain of responsibility, Command, Interpreter, Iterator, Mediator, Memento, Null Object, Observer, State, Strategy, Template method, Visitor 

Use Case of Behavioral Design Pattern- 

The template pattern defines the skeleton of an algorithm in an operation deferring some steps to sub-classes. The template method lets subclasses redefine certain steps of an algorithm without changing the algorithm structure. For example, in your project, you want the behavior of the module to be able to extend, such that we can make the module behave in new and different ways as the requirements of the application change, or to meet the needs of new applications. However, no one is allowed to make source code changes to it, i.e you can add but can’t modify the structure in those scenarios a developer can approach template design pattern.

Behavioral pattern is mostly concerned about objects and the responsibility of the object so we can say the behaviour of the object. And the object and its responsibility is loosely coupled so we can easily separated out both.

## Types of Behavioral Pattern

- [Template Pattern](template.md)
- [Observer Pattern](observer.md)