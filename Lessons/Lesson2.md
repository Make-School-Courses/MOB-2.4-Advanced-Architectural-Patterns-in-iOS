# Lesson Title

## Minute-by-Minute [OPTIONAL]

| **Elapsed** | **Time**  | **Activity**              |
| ----------- | --------- | ------------------------- |
| 0:00        | 0:05      | Objectives                |
| 0:05        | 0:15      | Overview                  |
| 0:20        | 0:45      | In Class Activity I       |
| 1:05        | 0:10      | BREAK                     |
| 1:15        | 0:45      | In Class Activity II      |
| TOTAL       | 2:00      |                           |

## Why you should know this or industry application (optional) (5 min)

Explain why students should care to learn the material presented in this class.

## Learning Objectives (5 min)

1. Identify and describe
1. Define
1. Design
1. Implement

## Initial Exercise (15 min)

- Funny comic
- Prime the Pump (e.g. think and jot, think pair share, etc)
- Productivity Tip/Tool
- Review of current event (e.g. tech news relevant to your track/topic)
- Quiz on homework or topic(s) of past class
- Concept Test

## Overview/TT I (20 min)

### The Factory Patterns

#### Problems Addressed
How do you create objects without needing to specify the exact class of the object to be created?

How can an object be created so that subclasses can redefine which class to instantiate?

How can a class defer instantiation to subclasses?

By using the Factory Method pattern!

#### Description
Factory Method is a Creational Pattern that is used to create objects without needing to specify the exact class of the object to be created.

Instead of using a constructor, it creates objects by calling a specialized method accessible to calling components.

Factory Method implementation is:

- either specified in an interface or protocol and implemented by child classes
- or implemented in a base class and optionally overridden by derived classes

Once implemented, the Factory Method will have all logic required to select a specifically desired class to instantiate, but it only exposes the protocol or base class to the calling component.

The Factory Method pattern is executed in **three operations:**

1. A function in some calling component calls the factory method supplying it with the arguments required to select the  implementation class desired.
2. The factory method executes using the passed-in arguments to create an instance of the desired class.
3. Once the instance of the desired class is created, the factory method returns to the calling component a reference to the newly-created object of the desired class.

#### Example

<!-- Example code -->


#### Benefits
1. Factory Method pattern makes the codebase more flexible to add or remove new types.
2. It is simple to implement.
3. It is often combined with the singleton and object pool patterns.

#### When to use (or not to)

The goal of this pattern is to encapsulate a thing for which optional variations of that thing are needed.

Use it when there is a choice to be made between classes that implement a shared protocol or base class.

This pattern works when a calling component can rely on the existence of only one single base type; do not use it if there is no single common base class or shared protocol.

<!--
- Why learn this?

- Industry examples of usage
- Best practices
- Personal anecdote
-->



## In Class Activity I (30 min)

- I do, We do, You do
- Reading & Discussion Questions in small groups
- Draw a picture/diagram
- Complete Challenges solo or in pair
- Q&A about tutorials
- Pair up and code review
- Pair program
- Formative assessment
- Form into groups
- etc (get creative :D)

## Overview/TT II (optional) (20 min)

## In Class Activity II (optional) (30 min)

## Wrap Up (5 min)

- Continue working on your current tutorial
- Complete reading
- Complete challenges

## Additional Resources

1. Links to additional readings and videos
