<!-- Run this slideshow via the following command: -->
<!-- reveal-md README.md -w -->


<!-- .slide: class="header" -->

# Creational Patterns Pt.1

## [Slides](https://make-school-courses.github.io/MOB-2.4-Advanced-Architectural-Patterns-in-iOS/Slides/01-Creational-PatternsPt.1/README.html ':ignore')

<!-- > -->

## Why you should know this

__*Design patterns*__ represent time-tested solutions to general software development challenges realized by numerous experienced software engineers through decades of trial and error.

<!-- > -->

Design patterns...

- Create a common language
- Provide tested solutions to common development problems
- Fast-track developer on-boarding
- Allow you to spot similarities between code

<!-- > -->

## Learning Objectives

By the end of this lesson, you should be able to...

1. Explain why design patterns are important in software development
2. Describe:
  - the **Singleton** and **Object Template** patterns
  - the software construction problem each is intended to solve
  - potential use cases for each (when to use them)
3. Assess:
  - the suitability of a given design pattern to solve a given problem
  - the trade offs (pros/cons) inherent in each
4. Implement basic examples of both patterns explored in this class

<!-- > -->


## 3 Types of Design Patterns

There are three main types of design patterns:

- **Structural**
- **Behavioral**
- **Creational**

<!-- > -->

### Creational patterns

Creational patterns are concerned with how objects are created in an application.

They aim to increase an application’s flexibility in instantiating objects in a manner suitable for a given situation.

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

Take 5 minutes to do a quick search on what the Singleton and Object template patterns are.

- Write a small description for each.

<!-- TODO: Insert a diagram? -->

<!-- > -->

## The Singleton Pattern

### The Singleton Pattern

![singleton](singleton.png)

*[Free Code Camp](https://medium.com/free-code-camp/singleton-design-pattern-pros-and-cons-e10f98e23d63)*

The singleton pattern restricts a class to only one, unique instance.

To ensure there is only one instance of your singleton, you must make it impossible for anyone else to make an instance.

<!-- > -->

Swift allows you to do this by marking the initializers as `private`. You can then add a `static` property for the shared instance, which is initialized inside the class.

Apple uses this approach **extensively in iOS** development.

Examples include:

- UserDefaults.standard
- UIApplication.shared
- FileManager.default

...all return a Singleton object.

<!-- > -->

__*Simple Example:*__

This simplified example illustrates the basic structure of a class definition designed to create a single instance of an object:

```swift
// Singleton design pattern
class Singleton {

   static let sharedInstance = Singleton()

   // use a private init to ensure only 1 instance is created
   private init() {
      // do something
   }
}
// Instantiate the Singleton object
let singleton = Singleton.sharedInstance
```

<!-- > -->

#### Pros & Cons

**PROS**
- __*Instance Control*__ — prevents other objects from instantiating their own copies of the Singleton object, ensuring that all objects access the single instance.
- __*Flexibility*__ - The class controls the instantiation process; hence, the class has the flexibility to change the instantiation process.
- __*Ease of Implementation*__ — Can create and use it anywhere and for the lifetime of the app. And you are absolutely sure of the number of instances when you use a Singleton.

<!-- > -->

**CONS**

Singletons are not the answer to every problem. And some developers are critical of Singletons for various reasons, including:

- __*Singletons hinder unit testing:*__ A Singleton might cause issues for writing testable code if the object and the methods associated with it are so tightly coupled that it becomes impossible to test without writing a fully-functional class dedicated to the Singleton.
- __*Singletons create hidden dependencies*__ and carry state around for the lifetime of the application.
- They inherently __*cause code to be tightly coupled.*__

<!-- > -->

## Creating a singleton

Follow [this guide]() to practice with singletons.

<!-- > -->

## Object template

__*The Object Template Pattern*__

- Helps prevent the tight coupling of components
- Also provides a foundation for more advanced patterns

<!-- > -->

In the __*object template pattern,*__ you define a template from which objects are created from a class or struct.

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

![object-template](obj-temp.jpg)

*[Pro Design Patterns in Swift](https://link.springer.com/chapter/10.1007/978-1-4842-0394-1_4)*

<!-- Needs code sample -->

<!-- > -->


## Exploring the template pattern

Follow [this activity]()


<!-- > -->

## After Class

1. **Research** — and __*be ready to discuss*__ in our next class the following:

a) The two design patterns we’ve covered today, paying attention to:

- definition/design
- the specific problem(s) that the pattern is intended to solve
- pros/cons of using it
- use case examples (with code to illustrate them, if possible)

<!-- > -->

b) These concepts:

- Inversion of Control (IoC)
- Tight Coupling...and the benefits of decoupling
- The Singleton Plus design pattern
- Dependency Injection
- the `private` access control level

<!-- > -->

2. **Rework the code** In the Activity above to **optimize maintainability:**

The code snippet you analyzed above presents a simple example of __*Tight Coupling.*__ The functions used to process the items in the products array are *tightly coupled* to the variables in each product tuple.

**TODO:** Applying what you’ve learned today, refactor the code in the snippet above to allow changing the properties on the product in a way that minimizes the need to change the calling code.

<!-- > -->

## Wrap Up

1) Brief summary of today's design Patterns

2) Any questions re: the After Class assignments above

<!-- > -->

## Additional Resources

1. [Software design pattern - wikipedia](https://en.wikipedia.org/wiki/Software_design_pattern)
2. [Design Patterns: Elements of Reusable Object-Oriented Software](https://en.wikipedia.org/wiki/Design_Patterns)
  - An extremely important book in the field of software development. Co-written by the "Gang of Four" (not the British punk rock group of the same name)
3. [Top 5 Design Patterns in Swift for iOS App Development - an article](https://rubygarage.org/blog/swift-design-patterns)
4. [Creational pattern - wikipedia](https://en.wikipedia.org/wiki/Creational_pattern)
5. [What Is a Singleton and How To Create One In Swift - an article](https://cocoacasts.com/what-is-a-singleton-and-how-to-create-one-in-swift)
6. [Swift 2.0 Programming : Design Patterns : The Singleton Pattern - video by funza Academy](https://www.youtube.com/watch?v=3g7zZJWEbX0)
