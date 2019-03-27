# Lesson Title

## Minute-by-Minute [OPTIONAL]

| **Elapsed** | **Time**  | **Activity**              |
| ----------- | --------- | ------------------------- |
| 0:00        | 0:05      | Objectives                |
| 0:05        | 0:15      | Overview  I                |
| 0:20        | 0:45      | In Class Activity I       |
| 1:05        | 0:10      | BREAK                     |
| 0:05        | 0:15      | Overview  II                |
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


#### Implementation

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

## Overview/TT II (20 min)

#### Problems Addressed





#### Description

The Builder pattern is a creational design pattern that allows you to create  complex objects — composed of requisite parts — from simple objects.

It differs from other Creational patterns in that it:
- employs a step-by-step approach
- calls for separating the construction of an object from its own class (i.e., An external class controls the construction algorithm).

#### Implementation

*Step-by-Step Approach*
The pattern organizes object construction into a set of steps which must be created in the same order, or by using a specific algorithm, to repeatedly create multiple objects of the same type.

To create an object, you execute a series these steps on a __*builder*__ object — but you are not required to call all steps for *all* objects created. You are allowed to call only those steps required to produced a particular object configuration.

**External Builders**
The Builder pattern suggests that you extract the object construction code out of its own class and move it to separate objects called *builders.*

The construction of the intended object is assigned to builder classes/objects and split into multiple steps.

To create an object, you successively call builder methods on an instance of a builder class, which builds the final object step-by-step and returns it as its final step.

**Typical Steps**
1. In a base builder class or protocol, declare the construction steps common to all intended optional object representations.
2. Declare are concrete builder class for each of the object representations. Implement their specific construction steps, including implementing a function to fetch/return the constructed object, if applicable.
3. Consider creating an additional class — often referred to as a Director — to encapsulate various ways to construct an object using the same builder class.
4. Implement client code (in calling component) to create both the builder and director objects.
- The client should pass the builder object to the director, and the director will use this builder object in all additional construction.
5. Returning the constructed result can be achieved in optional ways. For examples:
- It can be obtained directly from the director,  if all optional intended objects follow the same steps.
- The client can fetch the result from the builder.

#### Example

<!-- Example code -->


#### Benefits




#### When to use (or not to)






## In Class Activity II (optional) (30 min)

## Wrap Up (5 min)

- Continue working on your current tutorial
- Complete reading
- Complete challenges

## Additional Resources

1. Links to additional readings and videos
