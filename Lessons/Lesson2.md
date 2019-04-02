# Creational Patterns Pt.1

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

## Learning Objectives (5 min)

By the end of this lesson, you should be able to...

1. Describe:
- the **Factory Method** and **Builder** patterns
- the software construction problem each is intended to solve
- potential use cases for each (when to use them)
3. Assess:
- the suitability of a given design pattern to solve a given problem
- the trade offs (pros/cons) inherent in each
4. Implement basic examples of both patterns explored in this class


## Initial Exercise (15 min)

### In Pairs

Discuss...

1. What you learned about the impact of tuples on extending and maintaining code.

2. These concepts that you researched after the previous class:
- Inversion of Control (IoC)
- Tight Coupling...and the benefits of decoupling
- The Singleton Plus design pattern

**TIP:** *Feel free to look back at the previous lesson plan and/or to use Internet sources to jog your memory here...*

## Overview/TT I (20 min)

### The Factory Method Pattern

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


#### Benefits
1. Factory Method pattern makes the codebase more flexible to add or remove new types.
2. It is simple to implement.
3. It is often combined with the Singleton and Object Pool patterns.

#### When to use

The goal of this pattern is to encapsulate a **thing** for which optional variations of that thing are needed.

Use it when there is a choice to be made between classes that implement a shared protocol or base class.

This pattern works when a calling component can rely on the existence of only one single base type
- __*do not*__ use it if there is no single common base class or shared protocol.

## In Class Activity I (30 min)

In the code below, all vehicles are to be created using the `CarFactory` protocol's `create()` function.

But only the code for creating the Truck object has been completed.

**TODO:** Complete the code for creating the **SportsCar** and **SUV** obects following the basic guidelines of the Factory Method pattern introduced above. Validate creation of each object by running it's `drive()` function.

```Swift
// factory protocol
protocol CarFactory {
    func create() -> Car
}

class Car {
    func drive() {
        print("driving a car")
    }
}

class Truck: Car {
    override func drive() {
        print("driving a truck")
    }
}

class SportsCar: Car {
   // missing function

}

class SUV: Car {
    override func drive() {
        print("I’d rather be driving!")
    }
}

/// concrete factory
class TruckFactory: CarFactory {
    func create() -> Car {
        return Truck()
    }
}

let truckFactory = TruckFactory()
let truck = truckFactory.create()
truck.drive() // prints "driving a truck"

let sportsCarFactory = SportsCarFactory()


let suvFactory = SUVFactory()
```


## Overview/TT II (20 min)

#### Description

The Builder pattern is a creational design pattern that allows you to create  complex objects — composed of requisite parts — from simple objects.

It differs from other Creational patterns in that it:
- employs a step-by-step approach
- calls for separating the construction of an object from its own class (i.e., An external class controls the construction algorithm).

#### Implementation

**Step-by-Step Approach**
The pattern organizes object construction into a set of steps which must be created in the same order, or by using a specific algorithm, to repeatedly create multiple objects of the same type.

To create an object, you execute a series these steps on a __*builder*__ object — but you are not required to call all steps for *all* objects created. You are allowed to call only those steps required to produced a particular object configuration.

**External Builders**
The Builder pattern suggests that you extract the object construction code out of its own class and move it to separate objects called *builders.*

The construction of the intended object is assigned to builder classes/objects and split into multiple steps.

To create an object, you successively call builder methods on an instance of a builder class, which builds the final object step-by-step and returns it as its final step.

**Typical Steps**
1. In a base builder class or protocol, declare the construction steps common to all intended optional object representations.
2. Declare a concrete builder class for each of the object representations. Implement their specific construction steps, including implementing a function to fetch/return the constructed object, if applicable.
3. Consider creating an additional class — often referred to as a Director — to encapsulate various ways to construct an object using the same builder class.
4. Implement client code (in calling component) to create both the builder and director objects.
- The client should pass the builder object to the director, and the director will use this builder object in all additional construction.
5. Returning the constructed result can be achieved in optional ways. For examples:
- It can be obtained directly from the director,  if all optional intended objects follow the same steps.
- The client can fetch the result from the builder.

#### Example

```Swift
// Builder Pattern example
class WidgetFactory {
   var parts: String = “”
}

class Builder {
   let widgetFactory = WidgetFactory()
   var part = 0
   func buildPart() {
       part += 1
       widgetFactory.parts = widgetFactory.parts + ” adding part #\(part)”
   }

   func getResult() -> WidgetFactory{
       return widgetFactory
   }
}

   class Director {
       let builder = Builder()
       func construct() -> WidgetFactory {
           for _ in 1...5 {
               builder.buildPart()
           }
           return builder.getResult()
       }
}
let director = Director()
let widget = director.construct()
print(widget.parts) // prints: adding part #1 adding part #2 adding part #3 adding part #4 adding part #5
```


#### Benefits
This pattern allows you to produce different types and representations of an object using the same construction code.

Builder can use one of the other patterns — including Singleton or Bridge — to provide the logic that decides which object gets built.

Builder is one of the top design patterns used in iOS development (along with Singleton and Factory Method)

#### When to use (problems addressed)

Use the Builder pattern when…
- you need to compose complex objects
- you want to avoid having a constructor with too many parameters (difficult to work with)
- your code needs different versions of a specific object

**iOS Example**
What if you want to create a view controller which creates a custom view based on the user’s selection of key criteria such as:

- Region
- Gender
- Age
- Personal Interests
- etc.

...and then present a *different* view based on each of the choices the user selects?

Builder facilitates this architecture nicely!


## In Class Activity II (optional) (30 min)

### Part 1

The code below uses the Builder pattern (with a Director) to standardize the creation of three types of bicycles.

The implementation for the Kids bike is already complete.

Your job is to complete the code so that the remaining two bicycle types can also be created.

```swift
import UIKit

enum BicycleSize: String {
   case small
   case medium
   case large
}

enum BicycleType : String {
   case kids
   case standard
   case mountain
}

struct Bicycle
{
   public let type: BicycleType
   public let color: UIColor
   public let size: BicycleSize
}

extension Bicycle: CustomStringConvertible {
   public var description: String {
       return type.rawValue + ” bicycle”
   }
}

// Builder Protocol
protocol BikeBuilder {
   var type: BicycleType { get set }
   var color: UIColor { get set }
   var size: BicycleSize { get set }

   func construct() -> Bicycle
}

// MARK: - Builder
class BicycleBuilder: BikeBuilder {

   var type: BicycleType = .standard
   var color: UIColor = .gray
   var size: BicycleSize = .medium

   func construct() -> Bicycle {
       return Bicycle(type: type, color: color, size: size)
   }
}

// MARK: - Director
public class BikeAssembler {

   // Build a kids bike
   func createKidsBike() -> Bicycle {
       let builder = BicycleBuilder()
       builder.type = .kids
       builder.size = .small
       return builder.construct()
   }

   // TODO: 1) build the Mountain bike

   // TODO: 2) the Standard bike

}

let bikeAssembler = BikeAssembler()
let kids = bikeAssembler.createKidsBike()
print(kids.description)
```

### Part 2

Create a `Single View App` project.
- On the main screen, provide 4 buttons, each of a different color and another button that will create a detail view
- Applying the Builder pattern, generate the detail view based on the color the user selects (i.e., set the color of the detail view to the color selected by the UserDefaults

### Part 3 - Stretch goal



## After Class

Also known as __*A Virtual Constructor,*__ the Factory Method pattern is closely related to the *Abstract Factory pattern* and can also be considered a specialization of the *Template Method pattern.*

**TODO:**

1. Research these patterns with an eye toward examining how they relate to either the Builder or Factory Method patterns:
- Virtual Constructor
- Abstract Factory Pattern
- Template Method Pattern
- Object Pool Pattern
- Bridge Pattern

2. Using the Builder pattern, create a simple Single View App with the constructs necessary to build a pizza -  including 4 toppings - when the user presses a button (no UI presentation needed; log results are fine for now)


## Wrap Up (5 min)

1) Brief review of today's design patterns
2) Any questions re: the After Class assignments above


## Additional Resources

1. [Factory Method Pattern - wikipedia](https://en.wikipedia.org/wiki/Factory_method_pattern)
2. Builder Design Pattern:</br>
[Article 1](https://en.wikipedia.org/wiki/Builder_pattern)</br>
[Article 2](https://www.geeksforgeeks.org/builder-design-pattern/)
