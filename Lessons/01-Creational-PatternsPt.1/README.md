<!-- Run this slideshow via the following command: -->
<!-- reveal-md README.md -w -->


<!-- .slide: class="header" -->

# Intro & Creational Patterns Pt.1

## [Slides](https://make-school-courses.github.io/MOB-2.4-Advanced-Architectural-Patterns-in-iOS/Slides/01-Creational-PatternsPt.1/README.html ':ignore')

<!-- > -->

## Why you should know this

__*Design patterns*__ represent time-tested solutions to general software development challenges realized by numerous experienced software engineers through decades of trial and error.

<!-- v -->

You can see them as templates that you can customize to solve your own problems in your code base.

❌They are not libraries you can import.<br>
✅They are concepts that give you details and cues to implement a solution that works for you.

<!-- > -->

Design patterns...

- Create a common language
- Provide tested solutions to common development problems
- Fast-track developer onboarding
- Allow you to spot similarities between code

<!-- > -->

## Learning Objectives

By the end of this lesson, you should be able to...

1. Explain why design patterns are important in software development
2. Describe:
  - the **Singleton** and **Object Template** patterns
  - the software problem each is intended to solve
  - potential use cases for each
3. Assess:
  - the suitability of a given design pattern to solve a problem
  - the trade offs (pros/cons) inherent in each
4. Implement basic examples of both patterns explored in this class

<!-- > -->

## 3 Types of Design Patterns

According to their purpose, patterns can be categorized into:

- **Creational** - Object creation mechanisms
- **Structural** - How to assemble components into larger systems
- **Behavioral** - Effective distribution of responsibilities and communication

<!-- > -->

### Creational patterns

Creational patterns are concerned with **how objects are created**.

They aim to increase code flexibility when instantiating objects.

<!-- > -->

Creational design patterns include:

- __*Object Template*__
- __*Factory Method*__
- Abstract Factory
- __*Builder*__
- __*Singleton*__
- Prototype

<!-- > -->

### Warm up

Take 3 minutes to write a small description for each pattern based on what you know or what you've heard.

[Link to Jamboard](https://jamboard.google.com/d/1vaQUal9xfJR9joXEMt8YGmONoi6GqOnT8JbF5yfHDEY/edit?usp=sharing)

<!-- > -->

## The Singleton Pattern

<img src="https://refactoring.guru/images/patterns/content/singleton/singleton.png">

The singleton pattern makes sure that a class has only one instance. And that it can be accessed from anywhere in your code.

To ensure there is only one instance of your singleton, you must make it impossible for anyone else to make an instance.

<!-- > -->

## Why singleton?

- Make sure a class has a single instance = control access to a shared resource.
- Give a global access point to the instance

<!-- > -->

Apple uses this approach **extensively in iOS** development.

Examples include:

- UserDefaults.standard
- UIApplication.shared
- FileManager.default

...all return a Singleton object.

<!-- > -->

__*Simple Example:*__

This illustrates the basic structure of a class definition designed to create a single instance of an object:

```swift
// singleton design pattern
class Singleton {

   static let sharedInstance = Singleton()

   // use a private init to ensure only 1 instance is created
   private init() {
      // do something
   }
}
// instantiate the singleton object
let singleton = Singleton.sharedInstance
```

Swift allows you to create singletons by marking the initializers `private`. You can then add a `static` property for the shared instance, which is initialized inside the class.

<!-- > -->

**PROS**

__*Instance Control*__ — prevents other objects from instantiating their own copies of the Singleton object, ensuring that all objects access the single instance.


<!-- v -->

__*Ease of Implementation*__ — Can create and use it anywhere and for the lifetime of the app. And you are absolutely sure of the number of instances when you use a Singleton.

<!-- > -->

**CONS**

Singletons are not the answer to every problem. And some developers are critical of Singletons for various reasons, including:

__*Singletons hinder unit testing:*__ A Singleton might cause issues for writing testable code if the object and the methods associated with it are so tightly coupled that it becomes impossible to test without writing a fully-functional class dedicated to the Singleton.

<!-- v -->

__*Singletons need special treatment with multithreading*__ to avoid having multiple threads creating the object more than once.

<!-- v -->

They inherently __*cause code to be tightly coupled.*__

<!-- > -->

## Creating a singleton

Follow [this guide](https://github.com/Make-School-Courses/MOB-2.4-Advanced-Architectural-Patterns-in-iOS/blob/master/Lessons/01-Creational-PatternsPt.1/assignments/singleton.md) to practice with singletons.

<!-- > -->

## Object Template Pattern

You define a template from which objects are created from a class or struct.

When some component in your app needs a new object created, it calls the runtime by specifying the name of the template to use, along with any initialization values required to configure the object.

<!-- > -->

The __*object template pattern,*__ is composed of **three operations:**

1. A **calling component** asks the runtime to **create** an object and provides the **template name** and required **initialization values.**

2. The **runtime allocates memory** to store the object, **uses the template** to create it, and **initializes** (prepares) **the object for use.**

3. The **runtime returns the created object** to the calling component

<!-- > -->

Because this __*process can be easily repeated*__ as often as desired (within memory limits), a single template can be used to create many, many objects.

**This is essentially OOP as you learned in your CS classes!**

<!-- > -->

## Exploring the template pattern

Follow [this activity](https://github.com/Make-School-Courses/MOB-2.4-Advanced-Architectural-Patterns-in-iOS/blob/master/Lessons/01-Creational-PatternsPt.1/assignments/template.md) to see the benefits of the object template pattern.

<!-- > -->

## After Class

**Review** the following:

The two design patterns covered today, paying attention to:

- definition/design
- the specific problem(s) that the pattern is intended to solve
- pros/cons of using it
- use case examples (with code to illustrate them, if possible)

<!-- > -->

**Research** these concepts:

- Tight Coupling...and the benefits of decoupling
- Dependency Injection
- the `private` access control level

<!-- > -->

**Complete** the sections in the [worksheet](https://docs.google.com/document/d/11jRhbMQfxqDy3SP-Xs_EnWUnuwcwX3QFvNYnRbVvwWo/edit?usp=sharing) for the patterns covered in class.

<!-- > -->

## Additional Resources

- [Software design pattern - wikipedia](https://en.wikipedia.org/wiki/Software_design_pattern)
- [Design Patterns: Elements of Reusable Object-Oriented Software](https://en.wikipedia.org/wiki/Design_Patterns)
- [Top 5 Design Patterns in Swift for iOS App Development - an article](https://rubygarage.org/blog/swift-design-patterns)
- [Creational pattern - wikipedia](https://en.wikipedia.org/wiki/Creational_pattern)
- [What Is a Singleton and How To Create One In Swift - an article](https://cocoacasts.com/what-is-a-singleton-and-how-to-create-one-in-swift)
- [Swift 2.0 Programming : Design Patterns : The Singleton Pattern - video by funza Academy](https://www.youtube.com/watch?v=3g7zZJWEbX0)
- [Free Code Camp](https://medium.com/free-code-camp/singleton-design-pattern-pros-and-cons-e10f98e23d63)
- [Refactoring Guru - Singleton](https://refactoring.guru/design-patterns/singleton)
- Book: Pro Design Patterns in Swift
- [Gang Of Four Cheat Sheet](http://www.blackwasp.co.uk/GangOfFour.aspx)
