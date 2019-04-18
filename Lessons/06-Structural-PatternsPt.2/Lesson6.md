# Structural Patterns Pt.2

<!-- INSTRUCTOR NOTES:
1) No quiz this class -- course project intro instead
2) For Activity 1:
- Solution is embedded below Add'l Resources
3) for Activity 2:
- Solution is embedded below Add'l Resources
-->

## Minute-by-Minute

| **Elapsed** | **Time**  | **Activity**              |
| ----------- | --------- | ------------------------- |
| 0:00        | 0:05      | Objectives                |
| 0:05       | 0:10      | Initial Exercise             |
| 0:15       | 0:25      | Overview  I                |
| 0:40       | 0:25      | In Class Activity I       |
| 1:05       | 0:10      | BREAK                     |
| 1:15         | 0:15      | Overview  II                |
| 1:30       | 0:25      | In Class Activity II      |
|1:55       | 0:05    | Wrap Up                     |
| TOTAL       | 2:00    |    


## Learning Objectives (5 min)

By the end of this lesson, you should be able to...

1. Describe:
- the **Proxy** and **Facade** patterns
- the software construction problem each is intended to solve
- potential use cases for each (when to use them)
3. Assess:
- the suitability of a given design pattern to solve a given problem
- the trade offs (pros/cons) inherent in each
4. Implement basic examples of both patterns explored in this class

## Initial Exercise (10 min)

### As A Class

- Course Project Kickoff


## Overview/TT I (25 min)

#### Proxy

The Proxy design pattern is used to provide a __*surrogate*__ or __*placeholder*__ object, which references an underlying object.

In its most general form, a *proxy* is a class functioning as an interface to something else.

The proxy could interface to anything:
- a network connection to a remote service
- a large object in memory
- a file
- or some other resource that is expensive or impossible to duplicate

 Calling components operate on the proxy, which in turn operates on the underlying resource.

#### Problems Addressed

The Proxy pattern is used to solve three different problems:

1. **Remote Object Problem** - This arises when dealing with resources that are accessed over a network, such as a web page or a RESTful web service.

2. **Expensive**<sup>1</sup> **Operation Problem** - Involves tasks such as making HTTP requests which are classified as *expensive*<sup>1</sup> operations.

3. **Restricted Access Problem** - When you need to restrict access to an object but you don’t have access to the source code or because there is already a dependency on the object type elsewhere in the application, and you cannot afford to let any user perform the operations that the object encapsulates.

*From:
Pro Design Patterns in Swift* - Adam Freeman


#### Benefits
Proxies allow close control over the way underlying resources are accessed, which is useful when you need to intercept and adapt operations.

The *intent* of the pattern is to:
- Control access to some object by providing a surrogate or placeholder (proxy) to it.
- Use an extra level of indirection to support distributed, controlled, or intelligent access.
- Add a wrapper and delegation to protect the real component from undue complexity.

Proxies can also be used to *defer expensive operations* (example, `lazy loading`).

#### Pitfalls

Pitfalls associated with the proxy pattern depend on how it is being implemented:

- For **Remote Object proxies** - Ensure that no unnecessary details of the mechanism used to access the remote object are revealed.
- For proxies used to manage **Expensive Operations** - Avoid exposing details of how the cost of the operation is being mitigated.
- For **Access Restriction proxies** - Take care not to allow calling components to bypass the proxy and access the underlying object directly.

Some general, common themes are:

- Do not allow details of the implementation to leak out of the proxy class into the calling component.
- Avoid allowing instances of the underlying class to be instantiated when a proxy is used to restrict access to an object.

And, if you use the proxy pattern to implement __*reference counting:*__
- Do not use proxies to manage the life cycle of objects.
- Do not use proxies to implement concurrency protections such as locks and semaphores. Let GCD handle this.

##### Proxy in iOS


 - Deferring the Operation
        - lazy loading, lazy initialization


#### When to use

The proxy pattern can be used whenever an object is required to represent some other resource. The resource can be something abstract, such as a web page, or something local to the application, such as another object.

Proxies are used in three main situations mentioned:

- to define an interface to a remote resource
- to manage the execution of expensive operations
- to restrict access to the methods and properties of other objects

Implementing proxy can be complex and labor intensive. If you need a solution that does *not* involve intercepting and adapting operations of another object, consider using one of the other Structural patterns instead.

#### Implementation Notes

The *proxy class* provides the same public interface as the underlying *subject class,* adding a level of __*indirection*__ *by accepting requests from a client object* and passing these to the real subject object as needed.

But implementation of the proxy pattern varies based on the kind of problem that it is being used to solve.

1. **Solving the Remote Object Problem** - Use a **Remote Proxy**, where a local object is a proxy for (represents) a remote object, and calling a method on the local object causes the corresponding method to be invoked on the remote object.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; The proxy object hides the details of how the remote resource is accessed and only presents its data.</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; It consolidates requests to the remote resource in a single application class. It allows implementation changes</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; to itself or the remote object without requiring changes to the calling client code.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; __*Examples:*__ </br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - HTTP requests to a remote web service</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - Any scenario involving a *distributed system,* such as an ATM (the ATM must communicate </br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  transactions with the bank's central computing system).

2. **Solving the Expensive Operation Problem** - A **Virtual Proxy** is used for loading objects on demand. It provides a simplified version of a complex or heavy object. Only when the detail of the object is required is the main object actually populated, providing a form of lazy initialization.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; A Virtual Proxy can be used to minimize the cost of expensive operations by decoupling the operation from </br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; its use, which can often be combined or at least deferred until the cost of performing the operation is lower.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; __*Examples:*__ </br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - A file management utility may use an object for each file visible on the screen. When obtaining the file list, </br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; the file name, size and other easy-to-retrieve information would be held in proxy objects. Only when </br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; the actual file is viewed (requested) would the real object be created and populated with the </br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; full contents of the file, as these are slower to access and require more memory. </br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - A very large image object can be represented using a virtual proxy object (with thumbnail and </br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; other image metadata), only loading the real object "on demand" the real image is requested by the user.

3. **Solving the Restricted Access Problem** - By using a **Protection Proxy**, which might be used to control access to a resource based on access rights. The proxy is defined as a wrapper around an object, adding additional logic to enforce some kind of restriction on its use (which presents a different implementation path from the other proxy types).

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; A Protection Proxy object usually conforms to a common protocol shared with the wrapped object, </br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; which means that proxy objects can be used as seamless replacements without having to </br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modify calling clients.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; The proxy intercepts requests to access the properties and methods of the underlying object and will  </br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; pass them on only if an access control policy has been satisfied.

The Proxy pattern is implemented correctly when the proxy object can be used to perform operations on the resource it represents.

Note, too, that proxies can reveal as much or as little of their implementation detail as they choose.

#### Protection Proxy Example

For this simple example, assume that the `HAL9000` object has its own access control/authentication mechanism and that you do not want client classes to access that mechanism directly.

Instead, the `CurrentComputer` class acts as a Protection Proxy intercepting and handling the client's request for access to the `HAL9000` object.

```Swift
//Protection Proxy protocol
protocol DoorOperator {
    func open(doors: String) -> String
}

//Restricted Access Object
class HAL9000 : DoorOperator {
    func open(doors: String) -> String {
        return ("HAL9000: Affirmative, Dave. I read you. Opened \(doors).")
    }
}

//Protection Proxy object
class CurrentComputer : DoorOperator {
    private var computer: HAL9000!

    func authenticate(password: String) -> Bool {

        guard password == "pass" else {
            return false;
        }

        computer = HAL9000()

        return true
    }

    func open(doors: String) -> String {

        guard computer != nil else {
            return "Access Denied. I'm afraid I can't do that."
        }

        return computer.open(doors: doors)
    }
}

//Client
let computer = CurrentComputer()
let podBay = "Pod Bay Doors"

computer.open(doors: podBay) // Result: "Access Denied. I'm afraid I can't do that."
computer.authenticate(password: "pass")
computer.open(doors: podBay) // Result: "HAL9000: Affirmative, Dave. I read you. Opened Pod Bay Doors."
```

*From this series of Swift design pattern articles:* </br>
 https://github.com/ochococo/Design-Patterns-In-Swift
 <!-- under GNU License -->

## In Class Activity I (30 min)

In this exercise, you are going to create an `Image` protocol and concrete classes implementing it:
- `ProxyImage` is a a proxy class created to reduce the memory footprint created when loading the image.
- Loading the image will up to the `RealImage` object.

Your "client" will use `ProxyImage` to get an `Image` object to load and display, as needs.

```Swift
import UIKit

//Step 1 - Create a protocol (interface)

    //TODO: Create Image protocol, with a display() function

//Step 2 - Create concrete classes implementing the same protocol
class RealImage: Image {

    var fileName: String

    init (fileName: String) {
        self.fileName = fileName
        loadFromDisk(fileName: fileName)
    }

    func display() {
        print("Displaying", fileName)
    }

      //TODO: Create loadFromDisk function that will accept fileName and prints "Loading" along with the fileName

}

class ProxyImage: Image {

    //TODO: Create vars needed

    init (fileName: String) {
        self.fileName = fileName
    }

    func display() {
        if realImage != nil {
            print("realImage already loaded")
        } else {
            print("Load realImage")

            //TODO: If realImage var is nil, create/load a new RealImage object, and pass it to realImage var
        }
        realImage!.display()
    }
}

//Step 3 - Client uses ProxyImage object to load the image through the RealImage class, but only when needed
let image: ProxyImage = ProxyImage(fileName: "test_10mb.jpg")
image.display()
print("") // Add line break for separation in output
image.display()

/* Output should be:

 Load realImage
 Loading test_10mb.jpg
 Displaying test_10mb.jpg

 realImage already loaded
 Displaying test_10mb.jpg
 */
```

*Adapted from this Java example:* </br>
https://www.tutorialspoint.com/design_pattern/proxy_pattern.htm

## Overview/TT II (optional) (20 min)

#### Facade

The Facade pattern is used to define a simplified interface to a more complex subsystem: a library, a framework, or a complex system of classes.

The primary purpose of the Facade pattern is to hide the complexity of a system, class or API and provide all of its functionality behind a simple interface.

The __*central actor*__ in this pattern is an __*object that serves as a front-facing interface*__ that masks more complex underlying, structural code.

#### Problems Addressed

Clients that access a complex subsystem directly refer to, and depend on, many different objects having different interfaces (tight coupling), which makes the clients hard to implement, change, test, and reuse.

#### Benefits

Facade can make a complex subsystem easier to use.

A facade can:
- improve readability and usability of a software library by masking interaction with more complex components behind a single, simplified API
- provide a context-specific interface to more generic functionality
- serve as a launching point for a broader refactoring of monolithic or tightly-coupled systems

#### Pitfalls

The primary pitfall when implementing the façade pattern is to leak details of, or create tight dependency to, the underlying objects. This means that the calling components are still dependent on the underlying classes or supporting types and will require modification when they change.

Also steer clear of creating a “god” facade, which might need to know too many details about every class in your app.


#### When to use

Facade is often used when a system is very complex, or it is difficult to understand because it has a large number of interdependent classes, or because its source code is unavailable.

Use Facade when:
- you want to provide a simple or unified interface to a complex subsystem.
- you need to decompose a subsystem into separate layers.

The facade pattern is ideal when working with a large number of interdependent classes, or with classes that require the use of multiple methods, particularly when they are complicated to use or difficult to understand.

Facade is __*particularly useful*__ when wrapping __*poorly designed subsystems*__ but cannot be refactored because the __*source code is unavailable*__ or the existing interface is too widely used.

#### Implementation Notes

This **core component** of this pattern a single class - __*the facade class*__ - which provides simplified methods required by client and which delegates calls to methods of existing system classes.

The facade class is a *wrapper* that contains a set of members that are easily understood and simple to use. Members access the subsystem on behalf of the facade client, hiding the implementation details of the subsystem.

This minimize dependencies on a subsystem by offloading work to the Facade object, which provides a single, simplified interface to the more general facilities of the subsystem.


**To implement** Facade:
1. **Identify target system(s)** whose functionality you seek to simplify.
2. **Define a Facade object** which provides simple methods to interact with the system and allows clients to use the facade instead of needing to interact with multiple classes in the system. The Facade object could also perform additional functionality before or after forwarding a request/interaction with the target system.

The façade pattern is implemented correctly when common tasks can be performed without the calling components having any dependency on the underlying objects or their supporting data types.

In addition, consider whether additional Facades would add value: You may decide to implement more than one facade to provide subsets of functionality for different purposes.

For example, if you notice a facade has functionality that some classes use and other functionality that other classes use, consider splitting it into two or more facades.
</br>

##### - Simplified Example -

In this example, three simple classes - `SubSystemOne`, `SubSystemTwo`, and `SubSystemThree` - represent three separate systems, each potentially with its own set of functions and/or properties.

Though these are classes, each one could be a separate collection of related classes, as in an API.

```Swift
///Subsystem 1
class SubSystemOne {

    func performActionOne()
    {
        // Do something cool...
        print("printing on line \(#line) in function \(#function)")
    }
}

///Subsystem 2
class SubSystemTwo {

    func performActionTwo()
    {
        // Do something else cool...
        print("printing on line \(#line) in function \(#function)")
    }
}

///Subsystem 3
class SubSystemThree {

    func performActionThree(item: String)
    {
        // Do something even more cool...
        print("printing on line \(#line) in function \(#function), with \(item) passed as the arg")
    }
}
```

Note that after *wrapping* each of the three "subsystems," the Facade class can choose which behaviors of a given subsystem are to be exercised. The Facade class can also aggregate similar subsystem functions into a single function, simplifying the executions of several functions.

```Swift

///Facade class
class Facade {
    let subSystemOne = SubSystemOne()
    let subSystemTwo = SubSystemTwo()
    let subSystemThree = SubSystemThree()

    func performActionA() {

        print("printing on line \(#line) in function \(#function) from Facade class")

        subSystemOne.performActionOne()
        subSystemTwo.performActionTwo()
    }

    func performActionB() {

        print("printing on line \(#line) in function \(#function) from Facade class")

        subSystemOne.performActionOne()
        subSystemThree.performActionThree(item: "Thing")
    }
}

///Client
let facade = Facade()
facade.performActionA()
facade.performActionB()

/* This will print:

 printing on line 41 in function performActionA() from Facade class
 printing on line 9 in function performActionOne()
 printing on line 19 in function performActionTwo()
 printing on line 49 in function performActionB() from Facade class
 printing on line 9 in function performActionOne()
 printing on line 29 in function performActionThree(item:), with Thing passed as the arg
 */
```

##### - An iOS-Specific Example -

The Facade pattern is commonly used in apps written in Swift. It’s especially handy when working with complex libraries and APIs.

In this example, the "system" being wrapped by the *facade* is the `UserDefaults` system built into iOS.

Try this in a playground.

**Q:** *Can you see how much simpler it is to set and get values from UserDefaults using this facade pattern?*

```Swift
import UIKit

// Facade class
final class Defaults {

    private let defaults: UserDefaults

    init(defaults: UserDefaults = .standard) {
        self.defaults = defaults
    }

    subscript(key: String) -> String? {
        get {
            return defaults.string(forKey: key)
        }

        set {
            defaults.set(newValue, forKey: key)
        }
    }
}

// Client
let storage = Defaults()

// Store
storage["Bishop"] = "Disconnect me. I’d rather be nothing"

// Read
storage["Bishop"]
```

*From:*
https://github.com/ochococo/Design-Patterns-In-Swift/blob/master/source/structural/facade.swift



## In Class Activity II (15 min)

The `HotelBooker` and `FlightBooker` classes in the code below represent separate systems. Your customer, a travel agency, would really like to be able to book both airline flights and hotel accommodations in one simple procedure.

**TODO:** Using the Facade pattern, create a class that will unify the calls to these two disparate interfaces for your customer's app.

```Swift
import UIKit

///Subsystem 1
class HotelBooker {

    func book() {
        print("Hotel booked successfully")
    }
}

///Subsystem 2
class FlightBooker {

    func book() {
        print("Flight booked successfully")
    }
}

///Facade

    //TODO: Create a facade class that wraps both systems and invokes each of their separate book() functions

/// Client
let travelFacade = TravelFacade()
travelFacade.getFlightsAndHotels()


/* This prints:
Hotel booked successfully
Flight booked successfully
*/
```


## After Class

1. Look up these other Structural patterns:

- xxx

2. Research the following concepts:

- xxx

3. **TODO:**

<!-- get started with project  -->

<!-- Extend the Media Player app you created and improved in previous classes by implementing the following using either the Adapter or the Decorator pattern:

- Add functionality so that the user can skip to the `Next` or `Previous` video clip -->

__*Note*__ *- This will require that you have a collection of at several video clips.*


## Wrap Up (5 min)

- Continue working on your current tutorial
- Complete reading
- Complete challenges

## Additional Resources

1. [Slides](https://docs.google.com/presentation/d/1IFSv5SJR7c-Y1MMKmLcSPvIQ_pMrEBX_TOkiXkl4i94/edit?usp=sharing)


<sup>1</sup> The term *expensive* is used to refer to any aspect of an operation that should be minimized, including:
- the amount  of computation required
- the memory needed,
- the load on the device battery,
- the bandwidth consumed,
- and the elapsed time that the user has to wait.


<!-- SOLUTION TO ACTIVITY 1:
import UIKit

//Step 1 - Create a protocol (interface)
protocol Image {
    func display()
}

//Step 2 - Create concrete classes implementing the same protocol
class RealImage: Image {

    var fileName: String

    init (fileName: String) {
        self.fileName = fileName
        loadFromDisk(fileName: fileName)
    }

    func display() {
        print("Displaying", fileName)
    }

    func loadFromDisk(fileName: String) {
        print("Loading", fileName)
    }
}

class ProxyImage: Image {

    var realImage: RealImage?
    var fileName: String

    init (fileName: String) {
        self.fileName = fileName
    }

    func display() {
        if realImage != nil {
            print("realImage already loaded")
        } else {
            print("Load realImage")
            realImage = RealImage(fileName: fileName)
        }
        realImage!.display()
    }
}

//Step 3 - Client uses ProxyImage object to load the image through the RealImage class, but only when needed
let image: ProxyImage = ProxyImage(fileName: "test_10mb.jpg")
image.display()
print("") // Add line break for separation in output
image.display()


/* Output should be:

 Load realImage
 Loading test_10mb.jpg
 Displaying test_10mb.jpg

 realImage already loaded
 Displaying test_10mb.jpg
 */

-->


<!-- SOLUTION TO ACTIVITY 2:

import UIKit

///Subsystem 1
class HotelBooker {

    func book() {
        print("Hotel booked successfully")
    }
}

///Subsystem 2
class FlightBooker {

    func book() {
        print("Flight booked successfully")
    }
}

///Facade
class TravelFacade {

    private let hotelBooker = HotelBooker()
    private let flightBooker = FlightBooker()

    init() {

    }
    func getFlightsAndHotels() {
        hotelBooker.book()
        flightBooker.book()
    }
}

/// Client
let travelFacade = TravelFacade()
travelFacade.getFlightsAndHotels()


/* This prints:
Hotel booked successfully
Flight booked successfully
*/
  -->
