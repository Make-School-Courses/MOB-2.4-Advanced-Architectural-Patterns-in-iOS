# Reactive Programming (Part 3 of 3)

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



<!--

#### Hot & Cold** Observables
<!-- Hot and cold observables  -->


<!-- TODO: insert the standard comparison chart -->


### Operators

<!-- TODO: list the 4 types -->

<!-- TODO: pick a couple and show examples...esp. those that the class was confused by -->
<!-- TODO: retry()? -->


1. `combineLatest`

Combines up to 8 source Observable sequences into a single new Observable sequence and will begin emitting from the combined Observable sequence the latest elements of each source Observable sequence &mdash; once all source sequences have emitted at least one element &mdash; and also when any of the source Observable sequences emits a new element.

There is also a variant of combineLatest that takes an Array (or any other collection of Observable sequences):

```Swift
  example("Array.combineLatest") {
      let disposeBag = DisposeBag()

      let stringObservable = Observable.just("❤️")
      let fruitObservable = Observable.from(["🍎", "🍐", "🍊"])
      let animalObservable = Observable.of("🐶", "🐱", "🐭", "🐹")

      Observable.combineLatest([stringObservable, fruitObservable, animalObservable]) {
              "\($0[0]) \($0[1]) \($0[2])"
          }
          .subscribe(onNext: { print($0) })
          .disposed(by: disposeBag)
  }
```

> NOTE: Because the combineLatest variant that takes a collection passes an array of values to the selector function, it requires that all source Observable sequences are of the same type.

**Q:** What is the output of the `print()` function? Why?

<!-- SOLUTION:
This produces:
❤️ 🍐 🐱
❤️ 🍊 🐱
❤️ 🍊 🐭
❤️ 🍊 🐹 -->


<!-- TODO: end: You can create your own - show link  -->




<!-- takeUntil
distinctuntilchanged
race
combineLatest
buffertoggle -->



<!-- TODO: get exercises for Operators  -->


## Overview/TT I (20 min)

### Rx and UI / Table Views

In Wikipedia's definition of [Reactive programming](https://en.wikipedia.org/wiki/Reactive_programming), these 2 overall benefits standout:
- Rx has been proposed as a way to simplify the creation of interactive user interfaces and near-real-time system animation.
- In MVC architecture, Rx can facilitate changes in an underlying __*model*__ that are reflected automatically in an associated __*view.*__

Why is this important in iOS?

&mdash; Because there is an increasingly high demand for smooth UI transitions, pixel-perfect apps, and fewer steps to populate UI widgets with user data.

And Rx lets you create amazing UI behavior without managing the state complexity of variable interactions, and with fewer lines of code.

Two critical ways that Rx let you handle data changes to the UI properly are by using:
- **Bindings**
- **Reactive Data Sources**

#### Bindings

**Binding** &mdash; A means of keeping `model` and `view` values *synchronized* without you having to write a lot of “glue code.” It allows you to establish a mediated connection between a view and a piece of data, “binding” them such that a change in one is reflected in the other. <sup>x</sup>

Binding is one of key ways that Rx enables building apps in a *declarative* way. It creates a connected relationship between two entities.

Think of those entities as:
- A "producer," which produces the value
- A "consumer," which processes the values from the producer

> Notes:
> - It is required that the `consumer` conforms to the `ObserverType` protocol.
> - A `consumer` cannot return a value.


<!-- TODO: insert diagram -->


##### The `bind(to:)` Function
The primary method for binding an observable to another entity is the `bind(to:)` function.


<!-- TODO: add other uses of bind(to:), see reference ...examples, "background tasks" -->

__*Example 1*__

> When you bind an observable subscription to the `text` property, the property returns a new observer which executes its block parameter when each
> value is emitted. In other words: any time it receives a new value, it runs the code `label.text = text`

```swift
Observable.combineLatest(firstName.rx.text, lastName.rx.text) { $0 + " " + $1 }
    .map { "Greetings, \($0)" }
    .bind(to: greetingLabel.rx.text)
```

__*Example 2*__

> This also works with `UITableView`s and `UICollectionView`s. Here, you call `bindTo(_:)` to associate the `viewModel` observable with the code that should get executed for each row in the table view.

```swift
viewModel
    .rows
    .bind(to: resultsTableView.rx.items(cellIdentifier: "WikipediaSearchCell", cellType: WikipediaSearchCell.self)) { (_, viewModel, cell) in
        cell.title = viewModel.title
        cell.url = viewModel.url
    }
    .disposed(by: disposeBag)
```

*Source:* </br>
* `Why.md` in Documentation section of RxSwift library.*




<!-- ### data sources

Writing table and collection view data sources is tedious. There is a large number of delegate methods that need to be implemented for the simplest case possible.  -->


## In Class Activity I (30 min)

- I do, We do, You do
-

## Overview/TT II (optional) (20 min)

## In Class Activity II (optional) (30 min)

## Wrap Up (5 min)

- Continue working on your current tutorial
- Complete reading
- Complete challenges

## Additional Resources

1. Links to additional readings and videos

https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CocoaBindings/Concepts/WhatAreBindings.html  <sup>x</sup>

https://github.com/RxSwiftCommunity/RxDataSources
