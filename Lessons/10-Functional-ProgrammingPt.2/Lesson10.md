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

- **Functors**
- **Applicative Functors** (aka, Applicatives)
- **Monads**

Swift took features and ideas from many other programming languages, including *Haskell,* from which Swift loosely adapted some of Haskell's implementation of FP concepts such as HKTs.

Though HKTs are not currently supported in Swift,<sup>1</sup> Swift simulates HKTs by using Higher-Order Functions that *model* key HKT behaviors.

</br>

> <sup>1</sup> HKTs do not currently have native support in Swift. The standard Swift libraries are tied to base types, and Swift
> does not currently have HKT base types - such as a `Functor` type - to which subordinate types would conform to implement HKTss.
> For more on Swift and HKTs, see this doc from Apple on Generics:
> https://github.com/apple/swift/blob/master/docs/GenericsManifesto.md </br>
> "Higher-kinded types allow one to express the relationship between two different specializations of the same nominal type within a protocol."

</br>



#### Functors revisited

In the last lesson, we defined a **Functor** as a "a map between categories (object collections)."

A Functor can also be thought of as:
- a functional design pattern
- an abstraction of a way to apply a function over some structure which we cannot (or do not want to) alter
- a structure or container that applies *morphisms* or functions to the values it contains, instead of to itself

In other words, a Functor is *any type that implements the `map` function.*

![functor_mapping](assets/functor_mapping.png)

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

**Problem:** When a value is wrapped in a context, you can’t apply a normal function to it.


##### Example 1 - Using `map` with Optionals

**Note:** *Swift Optionals are another item borrowed from Haskell, which has a type called a `Maybe` that is functionally equivalent to the Swift `Optional` type definition.*

In the last lesson, we saw how to use the `map` function with collections (Swift Sequence types).

Because Optionals are also *container types,* we can also use the `map` function with Optionals to guard against `nil` (without unwrapping them).

> You can see how optionals are implemented in the Swift Standard Library by typing "Optional" into any Swift file and ⌘-clicking on it:

<!-- TODO: Validate this is still correct  -->
```Swift
public enum Optional<Wrapped> : ExpressibleByNilLiteral {
    case none
    case some(Wrapped)
}
```
> Thus, an optional is a type of container. It contains optional values of `none` and `some(Wrapped)`, and it can be mapped over just like an array or other Sequence type.

> To illustrate how an Optional behaves under the hood, we can create a function that takes an Optional, adds 1 to it if it is not `nil`, or returns `nil` if the Optional was actually `nil`...

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

> ...but we can also accomplish the same task, and with fewer lines of code, by creating a function that uses `map` to iterate over the Optional and return whichever optional state it finds...

```Swift
func increment(someNumber: Int?) -> Int? {
    return someNumber.map { number in number + 1 }
}

increment(someNumber: 5)   // Some 6
increment(someNumber: nil) // nil
```

> For a similar example using String Optionals, see this post: </br>
> https://www.hackingwithswift.com/example-code/language/how-to-use-map-with-an-optional-value


#### Applicative Functors

Applicative Functors take Functors to the next level. An Applicative lets you put the transformation function inside a container or Functor.

With an Applicative, our values are wrapped in a context, just like Functors. But our functions are wrapped in a context, too.

Suppose we want to have *a function in the Functor* and apply it to values *in another Functor* of the same kind.

For instance, we can extend a Functor by adding an `apply` function that *takes a function* and *applies it to the Functor.*

> Note: In native Swift, there currently is no base type for Applicatives; as a developer,
> you will need to create an `apply` function as needed.


##### Example 1 - Creating `apply` for Array

Unfortunately, Swift does not provide any `apply` function on arrays. To be able to implement Applicative Functors, we need to develop `apply` functions.

> Here is a simple version of an `apply` function that takes only one argument:

```Swift
func apply<T, V>(fn: ([T]) -> V, args: [T]) -> V {
    return fn(args)
}
```

> ...here is how that `apply` function could be used in your code:

```Swift
let numbers = [1, 3, 5]

func incrementValues(a: [Int]) -> [Int] {

    return a.map { $0 + 1 }
}

let applied = apply(fn: incrementValues, args: numbers) // prints: [2, 4, 6]
```

> Just to demonstrate how you could make the above `apply` function available to *all* arrays in a project, here is the same simple example in an extension of the Array class:

```Swift
extension Array {

    func apply<T, V>(fn: ([T]) -> V, args: [T]) -> V {
        return fn(args)
    }
}
```

> Note: this simple example is not ideal for demonstrating the extension of Array with `apply`; try adding `apply` functions to extensions on your own to understand how the Applicatives can add to Swift Sequence types.


##### Example 2 - Creating `apply` for Optionals

Applicative Functors provide us with the ability to operate on not just values, but values in a functorial context &mdash; such as Swift __*Optionals*__ &mdash; without needing to unwrap or map over their contents.

> Examine how the `apply` function in this example handles the Optional without unwrapping it:

```Swift
func add(_ a: Int) -> (Int) -> Int {
    return { b in
        return a + b
    }
}

let value: Optional<Int> = Optional.some(12)
let wrappedFunction: Optional<(Int) -> Int> = Optional.some(add(5))

func apply<T,U>(_ wrappedF: Optional<(T) -> U>, to value: Optional<T>) -> Optional<U> {
    switch (wrappedF, value) {
    case let (.some(f), .some(v)):
        return .some(f(v))
    default:
        return .none
    }
}

apply(wrappedFunction, to: value) // Prints: 17
```

> Again, if you create an `apply` function that you are satisfied should be applied to all Optionals, placing your `apply` function in an extension makes it accessible to any Optional:

```Swift
extension Optional {

    func apply<T,U>(_ wrappedF: Optional<(T) -> U>, to value: Optional<T>) -> Optional<U> {
        switch (wrappedF, value) {
        case let (.some(f), .some(v)):
            return .some(f(v))
        default:
            return .none
        }
    }
}
```

</br>

##### Applicatives with Multiple Parameters

Applicative Functors let us perform very powerful operations with a minimum of code.

In Haskell and other pure FP languages, Applicatives are more powerful than Functors because they allow function application with multiple parameters.

Even though this is not currently native to Swift, there are workarounds in Swift avaialable that allow you to create Applicatives which take multiple parameters.

> This topic is beyond the scope of today's lesson; It is recommended that you review Applicatives in this blog for details: </br>
> https://www.mokacoding.com/blog/functor-applicative-monads-in-pictures/


<!-- TODO: Insert image here  -->


#### Monads

<!-- TODO: Insert image here  -->

##### compactMap

<!-- https://useyourloaf.com/blog/swift-non-nil-values-in-an-array-of-optionals/ -->


let paths:[String?] = ["test", nil, "Two"]

let nonOptionals = paths.compactMap{$0}


You may heard of Monad, it is a typeclass(protocol) based on Functor




#### < recap Functors, etc. >

Functors apply a function to a wrapped value
Applicatives apply a wrapped function to a wrapped value

…a structure intermediate between functors and monads, in that they allow sequencing of functorial computations (unlike plain functors) but without deciding on which computation to perform on the basis of the result of a previous computation (unlike monads).




Applicative Functors are Functors with apply functions.

Applicative functor picks up where functor leaves off.
Functor lifts/upgrades a function making it capable of operating on a single effect.

Applicative functor allows the sequencing of multiple independent effects.

Functor deals with one effect while applicative functor can deal with multiple independent effects. In other words, applicative functor generalizes functor.




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

https://en.wikipedia.org/wiki/Currying
