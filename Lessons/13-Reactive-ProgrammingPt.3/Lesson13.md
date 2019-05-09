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


`combineLatest`

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

`This produces:
❤️ 🍐 🐱
❤️ 🍊 🐱
❤️ 🍊 🐭
❤️ 🍊 🐹
`

<!-- TODO: end: You can create your own - show link  -->

> NOTE: Because the combineLatest variant that takes a collection passes an array of values to the selector function, it requires that all source Observable sequences are of the same type.


<!-- takeUntil
distinctuntilchanged
race
combineLatest
buffertoggle -->



<!-- TODO: get exercises for Operators  -->


## Overview/TT I (20 min)

- Why learn this?
- Industry examples of usage
- Best practices
- Personal anecdote

## In Class Activity I (30 min)

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

## Overview/TT II (optional) (20 min)

## In Class Activity II (optional) (30 min)

## Wrap Up (5 min)

- Continue working on your current tutorial
- Complete reading
- Complete challenges

## Additional Resources

1. Links to additional readings and videos
