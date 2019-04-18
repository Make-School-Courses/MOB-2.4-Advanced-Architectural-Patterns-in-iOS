# Structural Patterns Pt.2

<!-- INSTRUCTOR NOTES:
1) For the quiz in the Initial Exercise:
- the URL is xxxx
2) For Activity 1:
- Solution is xxxx
3) for Activity 2:
- Solution is xxx
-->

## Minute-by-Minute

| **Elapsed** | **Time**  | **Activity**              |
| ----------- | --------- | ------------------------- |
| 0:00        | 0:05      | Objectives                |
| 0:05       | 0:20      | Initial Exercise             |
| 0:25       | 0:15      | Overview  I                |
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

## Initial Exercise (15 min)

### Part 1 - Individually

<!-- Quiz location:

TODO: Add quiz answersz

-->

## Overview/TT I (20 min)

#### Proxy


#### Implementation Notes



#### Problems Addressed





#### Benefits


#### Pitfalls


#### When to use

## In Class Activity I (30 min)



## Overview/TT II (optional) (20 min)

#### Facade

The Facade pattern is used to define a simplified interface to a more complex subsystem: a library, a framework, or a complex system of classes.




#### Problems Addressed





#### Benefits


#### Pitfalls
.

#### When to use


#### Implementation Notes

This core component of this pattern a single class - a __*facade class*__ - which provides simplified methods required by client and which delegates calls to methods of existing system classes.

The facade class is a *wrapper* that contains a set of members that are easily understood and simple to use. Members access the subsystem on behalf of the facade client, hiding the implementation details of the subsystem.

This minimize dependencies on a subsystem by offloading work to the Facade object.

To implement `Facade`:
1. **Identify target system(s)** whose functionality you seek to simplify.
2. **Define a Facade object** which provides simple methods to interact with the system and allows clients to use the facade instead of needing to interact with multiple classes in the system. The Facade object could also perform additional functionality before or after forwarding a request/interaction with the target system.

The façade pattern is implemented when common tasks can be performed without calling components having any dependency on the underlying objects or their supporting data types.

In addition, consider whether additional Facades would add value: You may decide to implement more than one facade to provide subsets of functionality for different purposes.

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



## In Class Activity II (optional) (30 min)

## Wrap Up (5 min)

- Continue working on your current tutorial
- Complete reading
- Complete challenges

## Additional Resources

1. Links to additional readings and videos
