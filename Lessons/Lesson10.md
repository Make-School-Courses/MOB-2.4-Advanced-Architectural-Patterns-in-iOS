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

The map function can be applied to any *container type* that wraps a value or multiple values inside itself. Any container that provides the map function becomes the Functor.

<!-- TODO: Insert image here  -->

Examples of Functors in Swift:
- Dictionaries
- Arrays
- Sets
- Closure types
- Functions
- Optionals

But...__*what specific programming problem*__ do functors solve?

&mdash; When a value is wrapped in a context, you can’t apply a normal function to it.


##### Example 1 - Using `map` with Optionals

<!-- TODO: note that Optionals are actually the Swift equivalent of Maybe in Haskell  -->

> You can see how optionals are implemented in the Swift Standard Library by typing "Optional" into any Swift file and ⌘-clicking on it:

<!-- TODO: Validate this is still correct  -->
```Swift
enum Optional<Wrapped> {
    case none
    case some(Wrapped)
}
```
> Thus, an optional is a type of container.

<!-- TODO: explain what this is doing... -->
```Swift
func increment(someNumber: Int?) -> Int? {
    if let number = someNumber {
        return number + 1
    } else {
        return nil
    }
}

increment(someNumber: 5)   // Some 6
increment(someNumber: nil) // nil
```

<!-- TODO: explain what this is doing... -->

```Swift
func increment(someNumber: Int?) -> Int? {
    return someNumber.map { number in number + 1 }
}

increment(someNumber: 5)   // Some 6
increment(someNumber: nil) // nil
```

<!-- https://www.hackingwithswift.com/example-code/language/how-to-use-map-with-an-optional-value -->



##### Example 1 - Using `map` with Sequence types





#### Applicative Functors

Applicative Functors let us perform some very powerful operations with a minimum of code.


…a structure intermediate between functors and monads, in that they allow sequencing of functorial computations (unlike plain functors) but without deciding on which computation to perform on the basis of the result of a previous computation (unlike monads).

An Applicative Functor is a Functor equipped with a function that takes a value to an instance of a Functor containing that value. Applicative Functors provide us with the ability to operate on not just values, but values in a functorial context, such as optionals, without needing to unwrap or map over their contents.

An Applicative Functor is a Functor equipped with a function that takes a value to an instance of a Functor containing that value. Applicative Functors provide us with the ability to operate on not just values, but values in a functorial context, such as optionals, without needing to unwrap or map over their contents.


Applicative functor picks up where functor leaves off. Functor lifts/upgrades a function making it capable of operating on a single effect. Applicative functor allows the sequencing of multiple independent effects. Functor deals with one effect while applicative functor can deal with multiple independent effects. In other words, applicative functor generalizes functor.


An applicative lets you put the transformation function inside a container.

Applicative Functors enable us to put a function inside a container or Functor.


Suppose we want to have a function in the Functor and apply it to values in another Functor of the same kind. For instance,we can extend a Functor by adding an apply function that takes a function and applies it to the Functor.


So, Applicative Functors are Functors with apply functions.

Functors apply a function to a wrapped value:
Applicatives apply a wrapped function to a wrapped value:


<!-- TODO: mentioned that there is no Applicative correlative in Swift -- you have to create it -->


apply is a function that applies a function to a list of arguments.

Nayebi, Dr. Fatih. Swift Functional Programming - Second Edition: Ease the creation, testing, and maintenance of Swift codes . Packt Publishing. Kindle Edition.


Unfortunately, Swift does not provide any apply method on arrays. To be able to implement Applicative Functors, we need to develop the apply function. The following code presents a simple version of the apply function with only one argument: func apply<T, V>(fn: ([T]) -> V, args: [T]) -> V {
    return fn(args)
}  The apply function takes a function and an array of any type and applies the function to the first element of the array. Let's test this function as follows:

let numbers = [1, 3, 5]
 func incrementValues(a: [Int]) -> [Int] {

   return a.map { $0 + 1 }
   }
    let applied

   Nayebi, Dr. Fatih. Swift Functional Programming - Second Edition: Ease the creation, testing, and maintenance of Swift codes . Packt Publishing. Kindle Edition.



Applicatives take it to the next level. With an applicative, our values are wrapped in a context, just like Functors:

But our functions are wrapped in a context too!


Note: the original article now shows how Applicatives are more powerful than Functors in that they allow function application with multiple parameters. Again this is not feasible in vanilla Swift, but we can work around it by defining the function we want to handle in a curried way.


<!-- TODO: Insert image here  -->


#### Monads

<!-- TODO: Insert image here  -->

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
