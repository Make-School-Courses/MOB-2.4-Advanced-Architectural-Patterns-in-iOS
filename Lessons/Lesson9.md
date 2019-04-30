# Functional Programming (Part 1 of 2)

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
4. Implement basic examples of XXX explored in this class


<!-- 1. Identify and describe
1. Define
1. Design
1. Implement -->

## Initial Exercise (15 min)

Review solutions to last class's After Class assignment:  

- [Advanced coordinators in iOS - a tutorial](https://www.hackingwithswift.com/articles/175/advanced-coordinator-pattern-tutorial-ios)



## Overview/TT I (20 min)

###  Functional Programming

> “Functional programming is a programming paradigm &mdash; a style of building the structure and elements of computer programs &mdash; that treats computation as the evaluation of mathematical
> functions and avoids changing-state and mutable data.”
> – Wikipedia

### Why Learn This?

**Enemy of the State** <sup>1</sup> </br>
iOS and Mac apps rely heavily on __*state*__ to change their presentation and respond to input &mdash; it's hard to imagine writing an app without the use of __*properties*__ and __*variables.*__

However, __*state*__ is a __*huge source of needless complexity,*__ and __*responsible for most of the easily avoidable bugs*__ that users encounter. State management is difficult and error-prone.

In OOP, programs are composed of classes and objects. Statements, when executed, can mutate the state of objects.

Functional Programming (FP) seeks to avoid using mutable states; functions are the fundamental building blocks. In FP, programs are structured by functions.  

Swift is not purely a functional programming language, but it does combine multiple programming paradigms to give you flexibility for app development, and it firmly embraces key attributes of FP:

- **Higher-Order Functions** &mdash; Including map, filter, reduce and compactMap.

- **Value Types** &mdash; Simpler numerics, enums and structs.


### Key Concepts

**State (aka, Mutable State)** &mdash; Refers to a program's stored values at any given time.

**Mutation** &mdash; The act of updating some state in-place.

**Higher-Order Functions** &mdash; a function that does at least one of the following:

takes one or more functions as arguments (i.e. procedural parameters),
returns a function as its result.

**Imperative programming** &mdash; A programming paradigm that uses statements that change a program's state. Consists of commands for the computer to perform and implements algorithms in explicit steps.

- OOP typically follows the Imperative Programming paradigm.

**Declarative programming** &mdash; Focuses on what the program should accomplish without specifying how the program should achieve the result. It seeks to minimize or eliminate *side effects* by describing __*what*__ the program must accomplish rather than describing __*how*__ to accomplish it.

- Functional Programming (FP) is considered a subset of Declarative Programming paradigm.

**Pure Functions** &mdash; A function is pure if it meets two criteria:
	- It always produces the same output if given the same input.
	- It does not produce external side effects (they do not change any data or state outside of themselves)

<!-- TODO: show example of pure function? -->


### Problem(s) Addressed

`Variables` represent data &mdash; or *state.* By definition, since a `variable` can *vary* as your app runs, it fosters *mutable state.*

Imperative_programming &mdash; with mutable state &mdash; can lead to __*unintended consequences*__ of certain side effects.

#### Side Effects

*Side Effects* represent any changes to the state outside of a code block's current scope. Side effects might include:

- Changing the value of a variable
- Writing some data to disk
- Enabling or disabling a button in the User Interface

A function produces side effects if it modifies some variable's value (state) outside of the variable's local environment.

Not all side effects are unwanted. In fact, it is difficult to produce an iOS app without changing the state of some key variables.

However, uncontrolled side effects can cause unintended consequences: As apps grow, mutable state becomes harder to manage (and to test), especially
with concurrency for which mutable state can create dead-locks and race conditions.

<!-- TODO: example here -->


#### Benefits of FP


<!-- Ease the creation, testing, and maintenance  -->

Cleaner code: “variables” are not modified once defined, so we don’t have to follow the change of state to comprehend what a function, a, method, a class, a whole project works.

 It eradicates threading issues like race-conditions and dead-locks
 It leaves state in tact for future use
 It is easy to test

 <!-- concurrency -->






### Imperative vs. Declarative Code Style

##### Example 1

<!-- A simple example in which all the odd numbers are chosen from an array of integers: -->




*from:* </br>
https://medium.com/swift2go/functional-programming-in-swift-an-introduction-253c1f420ca9



### First-Class and Higher-Order Functions

Functions in Swift are first class citizens (or first class values), this means that functions are types, this allows us to treat them as variables, pass them into other functions as arguments, and even allows functions to return other functions.

every language with FP has some version of Map, Filter, Reduce


Higher-order functions can receive other functions as their parameters. Swift provides higher-order functions such as map, filter, and reduce.

Also, in Swift, we can develop our own higher-order functions and DSLs.


### map

The map function is a higher-order function that solves the problem of transforming the elements of an array using a function.



<!-- < TODO: Demo map(()) -->

## In Class Activity I (30 min)

<!-- < TODO: have  students talk about side effects? -->



> First, create a type and an array to hold objects of the type.

```Swift
class MyItem {
    var name: String
    var description: String

    init(name: String, description: String) {
        self.name = name
        self.description = description
    }
}

var myArr = [
    MyItem(name: "Abc", description: "Lorem ipsum 1."),
    MyItem(name: "Def", description: "Lorem ipsum 2."),
    MyItem(name: "Xyz", description: "Lorem ipsum 3.")
]
```

> With __*imperative programming,*__ you tell the compiler what you want to happen, step by step:

```Swift
// Imperative approach
for item in myArr { // step through the array and decide if condition is met
    if item.name == "Def" {
        print("Yes")
    }
}
```

> With __*declarative programming,*__ you write code that describes **what** results are desired, but not the step-by-step commands on **how** to get them:

```Swift
// Declarative approach
if myArr.contains(where: { $0.name == "Def" }) {
    print("yes")
}
```
<!-- < TODO: have them update Example 1 using map() -->



## Overview/TT II (optional) (20 min)

## In Class Activity II (optional) (30 min)

- I do, We do, You do
- Reading & Discussion Questions in small groups
- Draw a picture/diagram
- Complete Challenges solo or in pair
- Q&A about tutorials
- Pair up and code review
- Pair program
- Formative assessment
- Form into groups
- etc (get creative :D)


## Wrap Up (5 min)

- Continue working on your current tutorial
- Complete reading
- Complete challenges

## Additional Resources

1. [Slides]()
2. [Functional programming - wikipedia](https://en.wikipedia.org/wiki/Functional_programming)
3. [Enemy of the State](https://speakerdeck.com/jspahrsummers/enemy-of-the-state?slide=5) <sup>1</sup>
[]()


https://en.wikipedia.org/wiki/Imperative_programming

https://en.wikipedia.org/wiki/Declarative_programming

https://realm.io/news/andy-matuschak-controlling-complexity/


https://en.wikipedia.org/wiki/State_(computer_science)


https://en.wikipedia.org/wiki/Comparison_of_programming_paradigms


deterministic
https://en.wikipedia.org/wiki/Deterministic_system


https://en.wikipedia.org/wiki/Side_effect_(computer_science)#Example


https://en.wikipedia.org/wiki/Higher-order_function
