# Structural Patterns Pt.1

<!-- INSTRUCTOR NOTES:
1) For the quiz in the Initial Exercise:
- the URL is xxxx
2) For Activity 1:
- xxxx
3) for Activity 2:
- xxx
-->

## Minute-by-Minute

| **Elapsed** | **Time**  | **Activity**              |
| ----------- | --------- | ------------------------- |
| 0:00        | 0:05      | Objectives                |
| 0:05       | 0:15      | Initial Exercise             |
| 0:20       | 0:15      | Overview  I                |
| 0:35       | 0:20      | In Class Activity I       |
| 0:55        | 0:10      | BREAK                     |
| 1:05         | 0:15      | Overview  II                |
| 1:20       | 0:25      | In Class Activity II      |
|1:45       | 0:05    | Wrap Up                     |
| TOTAL       | 1:50    |                          |


## Why you should know this...

<!-- Why Structural
- why these 2 patterns -->


## Learning Objectives (5 min)

By the end of this lesson, you should be able to...

1. Explain why **Structural design patterns** are important in software development
2. Describe:
- the **Adapter** and **Decorator** patterns
- the software construction problem each is intended to solve
- potential use cases for each (when to use them)
3. Assess:
- the suitability of a given design pattern to solve a given problem
- the trade offs (pros/cons) inherent in each
4. Implement basic examples of both patterns explored in this class


## Initial Exercise (15 min)

### Part 1 - Individually


<!-- Quiz location:

TODO: Add quiz answers

-->

### Part 2 - In Pairs

Grade each other's quizzes, sharing answers, insights, etc.

## Overview/TT I (20 min)


### Structural Patterns
Structural design patterns ease design by identifying a simple way to realize relationships between entities.

Examples of Structural patterns include:
- **Adapter**
- Aggregate
- Bridge
- Composite
- **Decorator**  
- Extensibility
- **Facade**
- Flyweight  
- Marker
- **Proxy**

*From: wikipedia*

*For lessons 5 and 6 in this course, we will cover the patterns highlighted in bold text above…*

**Structural Pattern Notes:**
1. MVC is a high-level example of a Structural pattern.
2. Many of the structural patterns have similar implementations but different intents. Best practice: Ensure you select the Structural pattern which best suits your intended purpose.
2. Adapter and Decorator are often each referred to as “wrapper” patterns because they wrap an object and provide a new interface around it. Here are some key differences between the two patterns:
- **Adapter** -- Can be used when the wrapper must respect a particular interface and must support polymorphic behavior.
- **Decorator** makes it possible to add or alter behavior of an interface at run-time.
- **Facade** is used when an easier or simpler interface to an underlying object is desired. *(We will learn more about Facade in next lesson.)*

![example](assets/wikipedia_table.png)

### The Adapter Pattern

Adapter lets classes work together that couldn’t otherwise because of incompatible interfaces.

It is used to provide a link between two elements that otherwise would not fit with each other by wrapping the "adaptee" with a class that supports the interface required by a client.

It decouples the client from the class of the targeted object.

#### Implementation Notes

The key idea in this pattern is to work through a *separate adapter* that adapts the interface of an (already existing) class *without changing it.*

Adapter is typically composed of four main *actors*:

1. **Adaptee** -- Defines an existing interface that needs adapting.
2. **Adapter** -- Adapts/converts the (incompatible) interface of a class (Adaptee) into another interface (Target) that clients require.
3. **Target** -- Defines the domain-specific interface that the Client uses.  
4. **Client** -- Collaborates with objects conforming to the Target interface.

The __*Adapter object*__ does the actual work -- it "wraps" the original object and adds new requirements specified by the Target.

The pattern is implemented correctly when the adapter allows a component to be integrated into the application without requiring modification of the existing application modules or the component.

**Best Practices in Swift**
- __*Use Protocols*__ --  The *design* of iOS protocols does not perfectly match the description of the Adapter pattern, though it achieves the *goal* of the pattern: allowing classes with otherwise incompatible interfaces to work together.
- __*Use Class Extensions*__ -- The most elegant way to implement the Adapter pattern is with a Swift extension. Extensions allow you to add functionality to classes that you are unable to modify. This functionality includes adding conformance to a protocol, which is perfectly suited to implementing the Adapter pattern. <sup>1</sup>



A protocol is a language-level (Objective-C) feature that makes it possible to define interfaces that are instances of the Adapter pattern.

#### Simple example

**Problem**
In the following example: A Hobbit object can only `walk()`, but a Guardian object (*code not listed*) must `march()`. But if a Hobbit is promoted to guard the citadel, the Hobbit somehow must now be able to `march()`.

**Solution** Use the Adapter pattern to (1) adapt the Hobbit class to a xxx

```swift
import UIKit

/// Adaptee
class Hobbit {
    func walk() {
        print("Hobbit is walking a few steps")
    }
}

/// Target
protocol GuardianOfTheCitadel {
    func march()
}

/// Adapter
extension Hobbit: GuardianOfTheCitadel {
    func march() {
        walk()
        print("Hobbit realizes he is a few steps behind the formation")
        walk()
    }
}

let hobbit = Hobbit()
hobbit.march()

/* This will print:
 Hobbit is walking a few steps
 Hobbit realizes he is a few steps behind the formation
 Hobbit is walking a few steps
 */
```
*Example above was adapted from this article:*
 https://medium.com/jeremy-codes/adapter-pattern-in-swift-7332e178f112


#### Problems Addressed


The adapter design pattern solves problems like:
How can a class be reused that does not have an interface that a client requires?
How can classes that have incompatible interfaces work together?
How can an alternative interface be provided for a class?


The problem that the adapter pattern solves arises when an existing system needs to integrate a new component that has a similar function but that doesn’t present a common interface and that cannot be modified.

On a smaller scale, incompatible code can be introduced into a project when a third-party component is used or when you depend on the code produced by another development team working on a related project.



#### Benefits


This pattern allows you to integrate components for which you cannot modify the source code into your application. This is a common problem when you use a third-party framework or when you are consuming the output from another project.


#### Pitfalls

Trying to extend the pattern to force integration of a component that does not provide the functionality intended by the API for which it is being adapted.

#### When to use

Classes, modules, and functions can’t always be modified, especially if they’re from a third-party library. Sometimes you have to adapt instead!

Use Adapter...

- when you need to integrate a component that provides similar functionality to other components in the application but that uses an incompatible API.
- during the implementation of third-party classes when there is a mismatch in the interface and it does not tally with the rest of application code.
- when you need to employ various existing subclasses and they are not complying with a specific functionality.

Adapter is also very often used in systems based on some legacy code.

__*Do not use__* the Adapter pattern when you are able to modify the source code of the component that you want to integrate or when it is possible to migrate the data provided by the component directly into your application.


## In Class Activity I (30 min)


## Overview/TT II  (20 min)

#### Description



#### Implementation



#### Problems Addressed





#### Benefits
.
- Why learn this?
- Industry examples of usage
- Best practices
- Personal anecdote

#### Pitfalls
.

#### When to use



You can use an adapter if you want to integrate a third-party library in your code, but it's interface doesn't match with your requirements.

Another use case is when you have to use several existing final classes or structs but they lack some functionality and you want to build a new target interface on top of them. Sometimes it's a good choice to implement an wrapper to handle this messy situation


## In Class Activity II  (30 min)

## Wrap Up (5 min)

- Continue working on your current tutorial
- Complete reading
- Complete challenges

## Additional Resources

1.

[Pro Design Patterns in Swift - a book by Adam Freeman](https://www.amazon.com/Design-Patterns-Swift-Adam-Freeman/dp/148420395X) <sup>1</sup>
