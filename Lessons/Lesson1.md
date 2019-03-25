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
- **Structural**
- **Behavioral**
- **Creational**


### Creational patterns
Creational patterns are concerned with how objects are created in an application.

They aim to increase an application’s flexibility in instantiating objects in a manner suitable for a given situation.

Creational design patterns include:
- __*Object Template*__
- __*Factory Method*__
- Abstract Factory
- __*Builder*__
- __*Singleton*__
- Prototype

*from wikipedia*

*Lessons 1 and 2 cover the Creational design Patterns highlighted above*

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

#### Pros & Cons

**PROS**
- __*Instance Control*__ — prevents other objects from instantiating their own copies of the Singleton object, ensuring that all objects access the single instance.
- __*Flexibility*__ - The class controls the instantiation process; hence, the class has the flexibility to change the instantiation process.
- __*Ease of Implementation*__ — Can create and use it anywhere and for the lifetime of the app. And you are absolutely sure of the number of instances when you use a Singleton.

**CONS**
Singletons are not the answer to every problem. And some developers are critical of Singletons for various reasons, including:

- __*Singletons hinder unit testing:*__ A Singleton might cause issues for writing testable code if the object and the methods associated with it are so tightly coupled that it becomes impossible to test without writing a fully-functional class dedicated to the Singleton.
- __*Singletons create hidden dependencies*__ and carry state around for the lifetime of the application.
- They inherently __*cause code to be tightly coupled.__*



<!-- for Presenter notes?
- Why learn this?
- Industry examples of usage
- Best practices
- Personal anecdote

-->



## Initial Exercise (15 min)

### 1. As A Class

- View [Swift 2.0 Programming : Design Patterns : The Singleton Pattern](https://www.youtube.com/watch?v=3g7zZJWEbX0) video by the funza Academy (7 mins)

### 2. In Pairs - Discuss

**Q:** What iOS design patterns have you used or are familiar with so far?

**Q:** When have you encountered the Singleton pattern in code you've written or come across so far? (See the list of Apple examples above for ideas.)
- Why do you think a Singleton was chosen for either (a) the Apple examples listed, or (b) code you've used or seen?

### 3. As A Class

- 1 or 2 students to share results of discussion with class...


<!--
- Funny comic
- Prime the Pump (e.g. think and jot, think pair share, etc)
- Productivity Tip/Tool
- Review of current event (e.g. tech news relevant to your track/topic)
- Quiz on homework or topic(s) of past class
- Concept Test
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
