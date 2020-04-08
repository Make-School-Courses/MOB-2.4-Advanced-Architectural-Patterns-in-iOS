<!-- Run this slideshow via the following command: -->
<!-- reveal-md README.md -w -->


<!-- .slide: class="header" -->

# Structural Patterns Pt.1

## [Slides](https://make-school-courses.github.io/MOB-2.4-Advanced-Architectural-Patterns-in-iOS/Slides/05-Structural-PatternsPt.1/README.html ':ignore')

<!-- > -->

<!-- INSTRUCTOR NOTES:
1) For the quiz in the Initial Exercise:
- the URL is https://docs.google.com/document/d/1kz7OpSDh_S2d7KCbUTeYEOR1M9r6-zgkxDhUGdvaDiY/edit
2) For Activity 1:
- Solution is embedded below Addtional Resources
3) for Activity 2:
- Solution is embedded below Addtional Resources
-->

<!-- > -->

## Learning Objectives

By the end of this lesson, you should be able to...

1. Explain why **Structural design patterns** are important in software development
2. Describe:
- the **Adapter** pattern
- the software construction problem each is intended to solve
- potential use cases
3. Assess:
- the suitability of patterns to solve a given problem
- the trade offs (pros/cons)
4. Implement basic examples

<!-- > -->

## Media Player Assignment Review

- Review progress of the media player app for which After Class work was assigned in the last 2 class sessions
- One student to volunteer to present their work (if time permits)


<!-- Quiz location:
https://docs.google.com/document/d/1kz7OpSDh_S2d7KCbUTeYEOR1M9r6-zgkxDhUGdvaDiY/edit
-->

<!-- Quiz answers:

Question 1: D, C, A, B

Question 2: God Object
https://en.wikipedia.org/wiki/God_object

Question 2:  Weak references
https://en.wikipedia.org/wiki/Lapsed_listener_problem

-->

<!-- > -->

## Structural Patterns

Structural design patterns ease design by identifying a simple way to realize relationships between entities.

They can assemble objects and classes into larger structures while keeping these structures flexible and efficient.

<!-- > -->

**Structural Pattern Notes:**

1. MVC is a **high-level** example of a Structural pattern.
2. Many of the structural patterns have similar implementations but different **intents**.
3. Adapter and Decorator are often each referred to as **wrapper** patterns because they wrap an object and provide a new interface around it.

<!--- **Adapter** - Can be used when the wrapper must respect a particular interface and must support polymorphic behavior.
- **Decorator** makes it possible to add or alter behavior of an interface at run-time.
- **Facade** is used when an easier or simpler interface to an underlying object is desired. *(We will learn more about Facade in next lesson.)*
-->

<!-- > -->

### The Adapter Pattern&nbsp;&nbsp;&nbsp;&nbsp;:electric_plug:

![adapter](assets/adapter1.png)

[*Refactoring Guru*](https://refactoring.guru/design-patterns/adapter)

<!-- > -->

![adapter](assets/adapter2.png)

[*Refactoring Guru*](https://refactoring.guru/design-patterns/adapter)

<!-- > -->

**Adapter lets classes work together that couldn’t otherwise because of incompatible interfaces.**

Provides a link between two elements that otherwise would not fit with each other by wrapping the **adaptee** with a class that supports the interface required by a client.

It decouples the client from the class of the targeted object.

<!-- > -->

#### Implementation Notes

The key idea in this pattern is to work through a *separate adapter* that adapts the interface of an (already existing) class **without changing it.**

<!-- > -->

Adapter is typically composed of four main *actors*:

1. **Adaptee** - Defines an existing interface that needs adapting.
2. **Adapter** - Adapts/converts the incompatible interface of a class (Adaptee) into another interface that clients require.

<!-- > -->

3. **Target** - Defines the domain-specific interface that the Client uses.  
4. **Client** - Collaborates with objects conforming to the Target interface.

<!-- > -->

The __*Adapter object*__ does the actual work - it "wraps" the original object and adds new requirements specified by the Target.

The pattern is implemented correctly when the adapter allows a component to be integrated into the application **without requiring modification** of the existing application modules or the component.

<!-- > -->

**Best Practices in Swift**

__*Use Protocols*__ -  The *design* of iOS protocols does not perfectly match the description of the Adapter pattern, though it achieves the *goal* of the pattern: allowing classes with otherwise incompatible interfaces to work together.

<!-- > -->

__*Use Class Extensions*__ - The most elegant way to implement the Adapter pattern is with a Swift extension.

Extensions allow you to add functionality to classes that you are unable to modify.

This functionality includes adding conformance to a protocol, which is perfectly suited to implementing the Adapter pattern.

<!-- > -->

### Example

**The Problem**

In the following example: A Hobbit object can only `walk()`, but a Guardian object (__*code not listed*__) must `march()`. What if a Hobbit is promoted to guard the citadel?

Then the Hobbit must somehow be able to `march()` just as a Guardian object does.

<!-- > -->

**The Solution**

Use the Adapter pattern to adapt the Hobbit class to conform to the behaviors required of a Guardian.

<!-- > -->

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

*[adapted example]( https://medium.com/jeremy-codes/adapter-pattern-in-swift-7332e178f112)*

<!-- > -->

## Add On To This Example

**TODO:** Assume we have another `protocol` for a `Warrior` who has an `attack` function.

How would we adapt a `Hobbit` to be a `Warrior`, where their `attack` function has them walk, swing a sword, then march?

<!-- > -->

### Problems Addressed

The Adapter pattern solves problems like:

- *How can a class be reused that does not have an interface that a client requires?*
- *How can classes that have incompatible interfaces work together?*
- *How can an alternative interface be provided for a class?*

<!-- > -->

Problems that Adapter solves arise when **an existing system** needs to integrate a **new component** that has a **similar function** but that doesn’t present a common interface and that cannot be modified.

<!-- > -->

Another key use of Adapter arises *when you do not have access to the original source code.* Incompatible code can be introduced into a project when:

- a __*third-party component*__ is used
- or when you depend on the code produced by another development team working on a related project.

<!-- > -->

| **Pros** | **Cons**  |
| ----------- | --------- |
| Integrate components when you can't modify source code    | Code complexity increases      |
| Single Responsibility Principle    | Forcing non intended integrations      |
| New functionality without breaking code   |      |

<!-- > -->

### When to use

Classes, modules, and functions can’t always be modified, especially if they’re from a third-party library. Sometimes you have to adapt instead!

<!-- > -->

Use Adapter...

- when you need to integrate a component that provides similar functionality to other components in the application but that uses an incompatible API.
- during the implementation of third-party classes when there is a mismatch in the interface and it does not tally with the rest of application code.

Adapter is also very often used in systems based on some legacy code.

<!-- > -->

### When not to use

__*Do not use__* the Adapter pattern when you are able to modify the source code of the component that you want to integrate

<!-- > -->

## In Class Activity

Complete [this activity](assignments/adapter.md) to learn how to implement the pattern.

<!-- > -->

## Jigsaw Activity

Now it's your turn to pick a pattern belonging to the Structural category to explain how it works and the main categories we always for each pattern.

Make sure to include a working coding example and prepare Slides to give a small 15 min presentation. Make a copy of [this template](https://docs.google.com/presentation/d/10oYlj86pBim3ZGBt5PSkJEQjIMuDDBFnwT74j4SJsd0/edit?usp=sharing) for it.

Resources [here](/06-Structural-PatternsPt.2/README.md)

<!-- > -->

## After Class

1. Look up these other Structural patterns:

- Aggregate
- Extensibility
- Flyweight
- Marker

2. Research the following concepts:

- The pros and cons of `Class Adapter` vs. `Object Adapter`
- The `Single Responsibility Principle`
- The principle of `Composition Over Inheritance`


3. **TODO:** Extend the Media Player app you created and improved in previous classes by implementing the following using either the Adapter or the Decorator pattern:

- Add functionality so that the user can skip to the `Next` or `Previous` video clip

__*Note*__ *- This will require that you have a collection of at several video clips.*


## Additional Resources

2. [Adapter pattern - wikipedia](https://en.wikipedia.org/wiki/Adapter_pattern)
3. [Decorator pattern - wikipedia](https://en.wikipedia.org/wiki/Decorator_pattern)
4. [CocoaDesignPatterns - Apple docs](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CocoaFundamentals/CocoaDesignPatterns/CocoaDesignPatterns.html)
5. [Swift adapter design pattern - an article](https://theswiftdev.com/2018/07/30/swift-adapter-design-pattern/)
6. [Pro Design Patterns in Swift - a book by Adam Freeman](https://www.amazon.com/Design-Patterns-Swift-Adam-Freeman/dp/148420395X) <sup>1</sup>
7. [Single responsibility principle - wikipedia](https://en.wikipedia.org/wiki/Single_responsibility_principle)
8. [Open–closed principle - wikipedia](https://en.wikipedia.org/wiki/Open–closed_principle)
9. [Combinatorial explosion - wikipedia](https://en.wikipedia.org/wiki/Combinatorial_explosion)
10. [Composition over inheritance - wikipedia](https://en.wikipedia.org/wiki/Composition_over_inheritance)
11. [Difference between object adapter pattern and class adapter pattern - stackoverflow](https://stackoverflow.com/questions/9978477/difference-between-object-adapter-pattern-and-class-adapter-pattern)


<!-- SOLUTION FOR ACTIVITY 1:

import UIKit

// Target protocol 1
protocol Player {
    func play(audioType: String, fileName: String)
}

// Target protocol 2
protocol Pause {
    func pause(fileName: String)
}

// Adaptee 1
class AudioPlayer {
    func playAudio(fileName: String) {
        print("Now Playing: ", fileName)
    }
}

// Adaptee 2
class VideoPlayer {
    func playVideo(fileName: String) {
        print("Now Playing: ", fileName)
    }
}

// Adapter (class)
class MyPlayer: Player {

    let videoPlayer = VideoPlayer()
    let audioPlayer = AudioPlayer()

    func play(audioType: String, fileName: String) {
        if (audioType == ".mp4"){
            videoPlayer.playVideo(fileName: fileName);
        }else if(audioType == ".aac"){
            audioPlayer.playAudio(fileName: fileName);
        }
    }
}

// Adapter (class extension)
extension MyPlayer: Pause {
    func pause(fileName: String) {
        print(fileName, " is now paused...")
    }
}

// Usage
let myPlayer = MyPlayer()
myPlayer.play(audioType: ".aac", fileName: "Titanium.aac")
myPlayer.play(audioType: ".mp4", fileName: "Cat_riding_a_roomba.mp4")


myPlayer.pause(fileName: "Cat_riding_a_roomba.mp4")
-->



<!-- SOLUTION FOR ACTIVITY 2:

import UIKit

// Abstract Core Component
protocol PizzaBase {
    func getPrice() -> Double
}

// Concrete Core Component
class PlainPizza: PizzaBase {

    var myPrice: Double = 1.0

    func getPrice() -> Double {
        return self.myPrice
    }
}

// Concrete Core Component
class Margherita: PizzaBase {

    var price: Double = 6.99

    func getPrice() -> Double {
        return self.price
    }
}

// Concrete Core Component
class Gourmet: PizzaBase {

    var price: Double = 7.49

    func getPrice() -> Double {
        return self.price
    }
}

// Decorator (base) class
class ToppingsDecorator: PizzaBase {

    private let pizza: PizzaBase

    required init(pizzaToDecorate: PizzaBase) {
        self.pizza = pizzaToDecorate
    }

    func getPrice() -> Double {
        return pizza.getPrice()
    }
}

// Decorator class (extended)
class ExtraCheeseTopping: ToppingsDecorator {

    override func getPrice() -> Double {
        return super.getPrice() + 1.0
    }
}

// Decorator class (extended)
class MushroomTopping: ToppingsDecorator {

    override func getPrice() -> Double {
        return super.getPrice() + 1.49
    }
}

// Decorator class (extended)
class JalapenoTopping: ToppingsDecorator {

    override func getPrice() -> Double {
        return super.getPrice() + 1.19
    }
}

/// Client-code for Margherita
//let pizza: PizzaBase = Margherita()
//print("Plain Margherita: ", pizza.getPrice())

/// Client-code for Gourmet
let pizza: PizzaBase = Gourmet()
print("Plain Gourmet: ", pizza.getPrice())

let moreCheese: ExtraCheeseTopping = ExtraCheeseTopping(pizzaToDecorate: pizza)
print("moreCheese: ", moreCheese.getPrice())

let evenMoreCheese: ExtraCheeseTopping = ExtraCheeseTopping(pizzaToDecorate: moreCheese)
print("evenMoreCheese: ", evenMoreCheese.getPrice())

let mushrooms: MushroomTopping = MushroomTopping(pizzaToDecorate: evenMoreCheese)
print("mushrooms: ", mushrooms.getPrice())

let withPeppers: JalapenoTopping = JalapenoTopping(pizzaToDecorate: mushrooms)
print("withPeppers: ", withPeppers.getPrice())


/* OUTPUT:

 1) For Client-code for Margherita, should print:

 Plain Margherita:  6.99
 moreCheese:  7.99
 evenMoreCheese:  8.99
 mushrooms:  10.48
 withPeppers:  11.67

 1) For Client-code for Gourmet, should print:

 Plain Gourmet:  7.49
 moreCheese:  8.49
 evenMoreCheese:  9.49
 mushrooms:  10.98
 withPeppers:  12.17

/*

-->
