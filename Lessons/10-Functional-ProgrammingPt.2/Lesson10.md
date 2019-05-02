# Functional Programming (Part 2 of 2)

<!-- INSTRUCTOR NOTES:
1) For Activity 1:
- solution is inline below each exercises
-->

<!-- TODO: review and edit the Min X Min section - this was never validated  -->

## Minute-by-Minute

| **Elapsed** | **Time**  | **Activity**              |
| ----------- | --------- | ------------------------- |
| 0:00        | 0:05      | Objectives                |
| 0:05        | 0:20      | Initial Exercise          |
| 0:25        | 0:20      | Overview                  |
| 0:45        | 0:15      | In Class Activity I       |
| 1:00        | 0:10      | BREAK                     |
| 1:10        | 0:15      | Overview                  |
| 1:25        | 0:25      | In Class Activity II      |
| TOTAL       | 1:50      |                           |


## Learning Objectives (5 min)

By the end of this lesson, you should be able to...

1. Describe **Higher-kinded types (HKTs)** in FP:
- **Functors**
- **Applicative Functors** (aka, Applicatives)
- **Monads**
2. Describe how HKTs map to **Higher-Order Functions (HoFs)** in Swift
- along with software construction problem(s) each is intended to solve
3. Implement basic examples of the Swift HoFs explored in class: `map`, `filter`, `reduce`, `flatMap`, and `compactMap`.
4. Describe **Best Practices** for integrating FP and OOP in Swift.

## Initial Exercise (15 min)

### Part 1 - As a class

- Review progress on course project

### Part 2 - As a class

__*Discussion Topic:*__ Side Effects

**Q:** What examples of side effects can you think of?

**Q:** Are side effects ever desirable?


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


##### Functor Example: Using `map` with Optionals

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

#### Applicatives with Multiple Parameters

Applicative Functors let us perform very powerful operations with a minimum of code.

In Haskell and other pure FP languages, Applicatives are more powerful than Functors because they allow function application with multiple parameters.

Even though this is not currently native to Swift, there are workarounds in Swift avaialable that allow you to create Applicatives which take multiple parameters.

> This topic is beyond the scope of today's lesson; It is recommended that you review Applicatives in this blog for details: </br>
> https://www.mokacoding.com/blog/functor-applicative-monads-in-pictures/


<!-- TODO: Insert image here  -->


#### Monads

Functors apply a function to a wrapped value.

And Applicatives apply a wrapped function to a wrapped value.

**Monads** apply a function that *returns* a wrapped value *to* a wrapped value.

To do this, Monads have a `flatMap` function (modeled after the `liftM` in Haskell).

`flatMap` can be used to flatten one level of a dimension of a sequence or to remove `nil` values in the sequence.

##### Example 1 - Flattening a Nested Array

> This example starts with a nested array of integers. The numbers array consists of an array of 3 arrays,
> that each contain 3 numbers.
> The closure { $0 } simply returns the first argument of the closure, i.e. the individual nested arrays.
> When you call `flatMap(_:)` on the numbers array, you end up with a flattened array of individual numbers.

```Swift
let numbers = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
let result = numbers.flatMap({ $0 })

print(result) // [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

*from:* </br>
https://learnappmaking.com/swift-flatmap-compactmap-how-to/

##### Examples of Monads with Optionals: `compactMap(_:)`

A common use of a Monad in Swift is to filter out `nil` values from flattened arrays.

Since Swift 4.2, this is using the `compactMap(_:)` function.

&mdash; **Example 1** &mdash;

> Here is a simple example which removes `nil` from an array...

```Swift
let paths:[String?] = ["test", nil, "Two"]
let nonOptionals = paths.compactMap{$0}

print(nonOptionals) // ["test", "Two"]
```

*from:* </br>
https://useyourloaf.com/blog/swift-non-nil-values-in-an-array-of-optionals/


&mdash; **Example 2** &mdash;

> For this example, let's first see the results of using the `map` function on a collection with mixed data types.
> The `Int($0)` closure takes an individual string from numbers with $0 and attempts to convert it to an integer with the
> `Int()` initializer, which might return `nil` (since it’s an optional) – so its return type is `Int?`.

```Swift
let numbers = ["5", "42", "nine", "100", "Bob"]
let result = numbers.map({ Int($0) })

print(result) // [Optional(5), Optional(42), nil, Optional(100), nil]

```

> As a result, the return type of the mapping transformation is [Int?] – an array of optional integers:

```Swift
  [Optional(5), Optional(42), nil, Optional(100), nil]
```

> Let's apply the `compactMap(_:)` function to the same array:

```Swift
let numbers = ["5", "42", "nine", "100", "Bob"]
let result = numbers.compactMap({ Int($0) })

print(result) // [5, 42, 100]
```

> `compactMap(_:)` automatically removes `nil` elements from the returned array, and the return type of the `compactMap(_:)` function is a non-optional array:

```Swift
[5, 42, 100]
```

*from:* </br>
https://learnappmaking.com/swift-flatmap-compactmap-how-to/



</br>

<!-- Monads are any type of *container* you can call `flatMap` on.

In Swift, you can define `flatMap` for a type, the type can be called a Monad.

Arrays and Optionals are examples of Monads.

You can also define `flatMap` for other types, such as functions, tuples, reactive cocoa signals, the Result type, and many more... -->


<!-- TODO: Insert image here  -->

<!--

#### < recap Functors, etc. >

Functors apply a function to a wrapped value
Applicatives apply a wrapped function to a wrapped value

…a structure intermediate between functors and monads, in that they allow sequencing of functorial computations (unlike plain functors) but without deciding on which computation to perform on the basis of the result of a previous computation (unlike monads).



Applicative Functors are Functors with apply functions.

Applicative functor picks up where functor leaves off.
Functor lifts/upgrades a function making it capable of operating on a single effect.

Applicative functor allows the sequencing of multiple independent effects.

Functor deals with one effect while applicative functor can deal with multiple independent effects. In other words, applicative functor generalizes functor. -->



<!-- TODO: add reduce and filter  
#### Reduce function

#### Filter function
-->


## In Class Activity I (30 min)

<!-- So far, we have learned that:
- Functors are structures with `map` functions.
- Applicative Functors are Functors with `apply` functions
- Monads are Functors with `flatMap` (and `compactMap`) functions -->

**Exercise 1:** The output for the following code snippet is `[Optional(1), Optional(2), nil, nil, Optional(5)]`, which is not the desired output.

**TODO:** Rework this code so that it only prints the string equivalents of the the integers as `[1, 2, 5]`

```Swift
let possibleNumbers = ["1", "2", "three", "///4///", "5"]
let mapped: [Int?] = possibleNumbers.map { str in Int(str) }

print(mapped)
```

<!-- SOLUTION to Exercise 1:
let compactMapped: [Int] = possibleNumbers.compactMap { str in Int(str) }
// [1, 2, 5]
-->

**Exercise 2:** Using the `reduce` function, complete the code below so that the output is `6.667`

__*Remember:*__ The function `reduce` takes two arguments, an initial value and a closure.

For initial value, use: `0.0` </br>
Closure expression: `{ $0 + ($1 / Double(values.count)) }`

```Swift
let values = [7.0, 3.0, 10.0]
let avg:Double = // TODO: reduce values array to the average of all its elements

print(avg)
```
<!-- SOLUTION to Exercise 2:
let values = [7.0, 3.0, 10.0]
let avg:Double = values.reduce(0.0) { $0 + ($1 / Double(values.count)) }
print(avg)
// Output: 6.667
-->

**Exercise 3:** For the `values` array below, return only the even numbers in a new array. The output of that new `even` array should be `[14, 22]`

```Swift
let values = [11, 13, 14, 17, 21, 33, 22]
  // TODO: return only even numbers here

print(even)
// Output: [14, 22]
```
<!-- SOLUTION to Exercise 3:
let values = [11, 13, 14, 17, 21, 33, 22]
let even = values.filter { $0 % 2 == 0 }

print(even)
// Output: [14, 22]
-->


**Exercise 4:** You’re working with 4 groups of giraffes, and want to create one single group of giraffes that are taller than a certain height.

**TODO:** Complete by findining all the integers in the `giraffes` (nested) array that are greater than 10 and return them in one single, flat (non-nested) array:

```Swift
let giraffes = [[5, 6, 9], [11, 2, 13, 20], [1, 13, 7, 8, 2]]
let tallest = giraffes.flatMap({ // TODO: Insert closure syntax here })

print(tallest) // [11, 13, 20, 13]
```
<!-- SOLUTION to Exercise 4:
let giraffes = [[5, 6, 9], [11, 2, 13, 20], [1, 13, 7, 8, 2]]
let tallest = giraffes.flatMap({ $0.filter({ $0 > 10 }) })

print(tallest) // [11, 13, 20, 13]
```

*from:* </br>
https://learnappmaking.com/map-reduce-filter-swift-programming/#filter


<!-- 1) a few examples for recognition
2) coding exercises for reduce, filter, compactMap...and combining map and filter -->


## Overview/TT II (10 min)

### FP and Swift

In the last lesson, we noted how Swift was designed to combine multiple programming paradigms to provide flexibility in app development, including embracing the two key attributes of FP: Higher-Order Functions and Value Types, and using Optionals and functions (instead of methods).

Since we've covered how HoFs in Swift emulate HKTs in FP, let's delve into the importance of Swift `value types` as an expression of Functional Programming...

#### Value Types

Value Types - numbers, enums, and structs - are excellent at avoiding side effects because they are copied on assignment.

This means that value types always have only one "owner," which makes them safer, especially in multithreaded applications, and they make code easier to read, understand, reuse, and test.

They typically provide performance gains, as well.

<!-- TODO: show example of struct or enum replacing class instances -->

#### FP in Swift: Best Practices

1. **Follow The Concepts**

Your functions should have a clear input and a clear output with no global side effects such as mutating objects.

So, use the Swift equivalents of FP Functors, Monads, etc.: Higher-Order Functions like `map`, `filterMap`, etc.

2. **Avoid Mutable State**

Use `lets` instead of `vars` when dealing with data. Functional code is less prone to bugs and easier to understand than imperative code.

`Enums` are especially powerful in Swift because cases can have associated values. This kind of type (known as a `sum` type) are common in functional languages.

Using `value types` (structs) and `protocols` instead of classes helps you avoid mutable state. This can lead not only to much safer and easier to maintain code, but also to performance gains in computationally intensive parts of the program.

Consider creating a struct when one or more of these apply:
- the object's primary purpose is to encapsulate a few relatively simple data values
- encapsulated values will be copied rather than referenced when you assign or pass around an instance
- Any properties stored by the struct are themselves value types
- the object does not need to inherit properties or behavior from another existing type

3. **Readability First**

Readability takes priority over complexity and cleverness.

Complicated things can be broken down into smaller, simpler things: break code down into smaller, pure functions, which can be used several times throughout the project.

4. **Don’t fight the iOS Frameworks**

Swift is not a purely functional programming language and we always need to deal with Cocoa Touch frameworks that are mostly designed according to OOP principles.

Achieving a goal of no global side effects is not possible a great deal of the time due to how the Cocoa Touch frameworks are set up.

You also have to use UIViewControllers and UIViews for the UI Layer. There are ways to isolate your logic into nice immutable components to help with the mutability of these, but fighting the frameworks and overcomplicating your code to an unrecognizable, unreadable state is not the preferred practice.

Instead, get the best out of Swift functional programming by looking for opportunities to combine FP with OOP whenever possible.


## In Class Activity II (30 min)

Despite the emphasis on OOP constructs in the Cocoa Touch frameworks, especially in UIKit, it is still possible to apply FP principles to Views and View Controllers.

**Exercise 1:** As a Class: Quickly review the following:

> You have probably used __*higher-order functions*__ without really thinking about it as many of the methods in Cocoa Touch
> utilise them to a great extent. You just need to look at `UIViewController`, `URLSession`, or `UIView` to find common
> examples of *methods that take closures as arguments.*

```swift
viewController.present(anotherViewController, animated: true) {
  /* This is a closure */
}

UIView.animate(withDuration: 3) {
  /* This is a closure */
}
```
*Excerpted from:* </br>
https://www.varvet.com/blog/higher-order-functions-in-swift/


**Exercise 2:** As a Class: Examine and discuss the way that this post uses FP concepts (`apply` functions, HoFs, etc.) to dynamically style view controllers:

https://medium.com/@akbsteam/functional-swift-6-view-styling-1efc4588d1ce

> The post contains a playground, which can also be found here:
[View_Styling_Exercise.playground](View_Styling_Exercise.playground)



## After Class

1. Research (for light familiarity):

- Category Theory
- Arity and Variable Arity
- Morphism
- Kind
&nbsp;&nbsp;&nbsp; - and Type Constructor
- the “~=“ operator
- Functional Programming:
&nbsp;&nbsp;&nbsp; - Currying
&nbsp;&nbsp;&nbsp; - Partial Functions
&nbsp;&nbsp;&nbsp; - Eager vs Lazy Evaluation
&nbsp;&nbsp;&nbsp; - Recursion
&nbsp;&nbsp;&nbsp; - Endofunctor
- Futures, Promises, and Promise Frameworks
- Other Swift HoFs:
&nbsp;&nbsp;&nbsp; - sorted
&nbsp;&nbsp;&nbsp; - zip

2.  Study the "Traversing view hierarchy" section of the post below:

**TODO:** Create a single view app &mdash; or, better yet, use a more complex existing project such as your Course Project &mdash; and in that app, apply and experiment with the following extensions from the posted article:

- the `reduce` function
- the `flatmap` function

[Practical functional programming in Swift - an article](https://jakubturek.com/practical-functional-programming-in-swift/)

3. Continue working on your Course Project


## Wrap Up (5 min)

- Continue working on your Course Project...
- Complete reading
- Complete challenges/assignments

## Additional Resources

1. [Slides](https://docs.google.com/presentation/d/14kWg6CYB0HbqMwRE7TU6kmAzCykjg2uLcOKR4ADBjik/edit#slide=id.g591f3aad1c_0_227)
2. [Swift Functors, Applicatives, and Monads in Pictures - an article](https://www.mokacoding.com/blog/functor-applicative-monads-in-pictures/)
3. [What is a Mondad? - article](https://www.hackingwithswift.com/example-code/language/what-is-a-monad)
4. [Fold - wikipedia](https://en.wikipedia.org/wiki/Fold_(higher-order_function))
5. [Lots of Videos on FP in Swift](http://2014.funswiftconf.com)
6. For curious readers, it is recommended to read the [Swift Evolution Proposal](https://lists.swift.org/pipermail/swift-evolution/Week-of-Mon-20151214/002736.html) and the **Higher-kinded types** section of the [Generic manifesto](https://github.com/apple/swift/blob/master/docs/GenericsManifesto.md#higher-kinded-types).


<!--
Misc secondary posts:
(https://blog.codinghorror.com/code-smells/)
https://academy.realm.io/posts/andy-matuschak-controlling-complexity/


https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html
 -->
