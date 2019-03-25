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

__*Design patterns*__ represent time-tested solutions to general software development challenges realized by numerous experienced software engineers through decades of trial and error.

Design patterns...

- Create a common language
- Provide tested solutions to common development problems
- Fast-track developer on-boarding
- Allow you to spot similarities between code

It’s best for a new developer to have an understanding of what they are before running into them...


## Learning Objectives (5 min)

1. Identify and describe
1. Define
1. Design
1. Implement


## Overview/TT I (20 min)

### 3 Types of Design Patterns

There are three main types of design patterns:
- Structural
- Behavioral
- Creational

Lessons 1 and 2 cover Creational design Patterns

### Creational patterns
Creational patterns are concerned with how objects are created in an application.

They aim to increase an application’s flexibility in instantiating objects in a manner suitable for a given situation.

Creational design patterns include:
- Object Template
- Factory Method
- Abstract Factory
- Builder
- Singleton
- Prototype

*from wikipedia*

<!-- TODO: Insert a diagram? -->


### The Singleton Pattern
The singleton pattern restricts a class to only one, unique instance.

To ensure there is only one instance of your singleton, you must make it impossible for anyone else to make an instance.

Swift allows you to do this by marking the initializers as `private`. You can then add a `static` property for the shared instance, which is initialized inside the class.

**Apple* uses this approach **extensively in iOS** development.

Examples include:
- UserDefaults.standard
- UIApplication.shared
- FileManager.default

...all return a Singleton object.

__*Simple Example:*__

```Swift
// Singleton design pattern
   class DataSource {
       static let sharedInstance = DataSource()

       private init() // use a private init to ensure only 1 instance is created
   }

   // Invocation/usage
   let data = DataSource.sharedInstance
   ```


<!-- for Presenter notes?
- Why learn this?
- Industry examples of usage
- Best practices
- Personal anecdote

-->



## Initial Exercise (15 min)

- Funny comic
- Prime the Pump (e.g. think and jot, think pair share, etc)
- Productivity Tip/Tool
- Review of current event (e.g. tech news relevant to your track/topic)
- Quiz on homework or topic(s) of past class
- Concept Test



## In Class Activity I (30 min)

< student driver exercise here? >

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

__*The Object Template Pattern*__
- Helps prevent the tight coupling of components
- Also provides a foundation for more advanced patterns


## In Class Activity II (optional) (30 min)

## Wrap Up (5 min)

- Continue working on your current tutorial
- Complete reading
- Complete challenges

## Additional Resources

1. Links to additional readings and videos
