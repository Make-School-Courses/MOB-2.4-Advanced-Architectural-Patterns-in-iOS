# Functional Programming (Part 2 of 2)

<!-- INSTRUCTOR NOTES:
1) For the QuizLet Game in the Initial Exercise:
- the URL is xxxx
2) For Activity 1:
- xxx
3) for Activity 2:
- xxxx
-->

## Minute-by-Minute

| **Elapsed** | **Time**  | **Activity**              |
| ----------- | --------- | ------------------------- |
| 0:00        | 0:05      | Objectives                |
| 0:05        | 0:20      | Initial Exercise          |
| 0:25        | 0:20      | Overview                  |
| 0:45        | 0:15      | In Class Activity I       |
| 1:00        | 0:10      | BREAK                     |
| 1:10        | 0:20      | Overview                  |
| 1:30        | 0:25      | In Class Activity II      |
| TOTAL       | 1:55      |                           |


## Learning Objectives (5 min)

By the end of this lesson, you should be able to...

1. Describe:
- the **xxxx** design pattern
- the software construction problem(s) it is intended to solve
- potential use cases for it (when to use it; when not to use it)
3. Assess:
- the suitability of a given design pattern to solve a given problem
- the trade offs (pros/cons) inherent in choosing high-level (MVC, MVVM, etc.) design patterns
4. Implement basic examples of MVVM explored in this class


## Initial Exercise (15 min)

- Funny comic
- Prime the Pump (e.g. think and jot, think pair share, etc)
- Productivity Tip/Tool
- Review of current event (e.g. tech news relevant to your track/topic)
- Quiz on homework or topic(s) of past class
- Concept Test

## Overview/TT I (20 min)


### Higher-Order Functions (continued...)

A **Higher-Order Function** is a function that does at least one of the following:
- takes one or more functions as arguments
- returns a function as its result

#### Higher-kinded types

Another concept from Category Theory that Functional Programming languages seek to implement is called **Higher-kinded types (HKT)** or **HKTs.**

HKTs are simply a way to express polymorphism based on a __*type*__ (aka, [Kind](https://en.wikipedia.org/wiki/Kind_(type_theory))) and __*type constructor.*__

Think of HKTs as __*types*__ *that* __*take other types*__ and __*construct new types*__ with them.

In progressive order, HKTs types are:

- **Functors*
- **Applicative Functors** (aka, Applicatives)
- **Monads**

Swift took features and ideas from many other programming languages, including *Haskell,* from which Swift loosely adapted some of Haskell's implementation of FP concepts such as HKTs.

Though HKTs are not currently supported in Swift,<sup>1</sup> Swift simulates HKTs by using Higher-Order Functions that *model* key HKT behaviors.

</br>

> <sup>1</sup> HKTs do not currently have native support in Swift. The standard Swift libraries are tied to base types, and Swift
> does not currently have HKT base types - such as a `Functor` type - to which subordinate types would conform to implement HKTss.
> For more on Swift and HKTs, see this doc from Apple on Generics:
> https://github.com/apple/swift/blob/master/docs/GenericsManifesto.md
> "Higher-kinded types allow one to express the relationship between two different specializations of the same nominal type within a protocol."

</br>



#### Functors revisited

In the last lesson, we defined a **Functor** as a "a map between categories (object collections)."

A Functor can also be thought of as:
- a functional design pattern
- an abstraction of a way to apply a function over or around some structure which we cannot (or do not want to) alter
- a structure or container that applies *morphisms* or functions to the values it contains, instead of to itself

In other words, a Functor is *any type that implements the `map` function.*

Examples of Functors in Swift:
- Dictionaries
- Arrays
- Sets
- Closure types
- Functions
- Optionals

But __*specific programming problem*__ do functors solve?

&mdash; When a value is wrapped in a context, you can’t apply a normal function to it:








The map function can be applied to any container type that wraps a value or multiple values inside itself. Any container that provides the map function becomes the Functor,




OPtionals

An optional is a kind of container.
You can see how optionals are implemented in the Swift Standard Library by typing "Optional" into any Swift file and ⌘-clicking on it. Here's the important part of the definition:

enum Optional<Wrapped> {
    case none
    case some(Wrapped)
}


<!-- https://www.hackingwithswift.com/example-code/language/how-to-use-map-with-an-optional-value -->


func increment(someNumber: Int?) -> Int? {
    if let number = someNumber {
        return number + 1
    } else {
        return nil
    }
}

increment(5)   // Some 6
increment(nil) // nil


func increment(someNumber: Int?) -> Int? {
    return someNumber.map { number in number + 1 }
}

increment(5)   // Some 6
increment(nil) // nil



#### Applicative Functors




#### Monads


##### compactMap

<!-- https://useyourloaf.com/blog/swift-non-nil-values-in-an-array-of-optionals/ -->


let paths:[String?] = ["test", nil, "Two"]

let nonOptionals = paths.compactMap{$0}


You may heard of Monad, it is a typeclass(protocol) based on Functor




#### xxx



## In Class Activity I (30 min)


So far, we have learned that Functors are structures with map functions. Applicative Functors are Functors with apply functions and Monads are Functors with flatMap functions.


<!-- 1) a few examples for recognition
2) coding exercises for reduce, filter, compactMap...and combining map and filter -->


## Overview/TT II (optional) (20 min)



- Best practices



## In Class Activity II (optional) (30 min)

## Wrap Up (5 min)

- Continue working on your current tutorial
- Complete reading
- Complete challenges

## Additional Resources

1. Links to additional readings and videos

higher-kinded types
https://github.com/apple/swift/blob/master/docs/GenericsManifesto.md#higher-kinded-types
https://lists.swift.org/pipermail/swift-evolution/Week-of-Mon-20151214/002736.html


For curious readers, it is recommended to read the Swift Evolution Proposal (https://lists.swift.org/pipermail/swift-evolution/Week-of-Mon-20151214/002736.html) and the Generic manifesto (https://github.com/apple/swift/blob/master/docs/GenericsManifesto.md#higher-kinded-types).


https://www.hackingwithswift.com/example-code/language/what-is-a-monad


https://en.wikipedia.org/wiki/Fold_(higher-order_function)


https://www.mokacoding.com/blog/functor-applicative-monads-in-pictures/
