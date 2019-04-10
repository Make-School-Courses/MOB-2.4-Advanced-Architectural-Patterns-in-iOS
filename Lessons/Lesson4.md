# Behavioral Patterns Pt.2

<!-- INSTRUCTOR NOTES:
1) For the quiz in the Initial Exercise:
- the URL is xxxx
2) For Activity 1:
- xxxx
3) for Activity 2:
- xxx
-->

## Minute-by-Minute [OPTIONAL]

| **Elapsed** | **Time**  | **Activity**              |
| ----------- | --------- | ------------------------- |
| 0:00        | 0:05      | Objectives                |
| 0:05       | 0:15      | Initial Exercise             |
| 0:20       | 0:15      | Overview  I                |
| 0:35        | 0:20      | In Class Activity I       |
| 0:55        | 0:10      | BREAK                     |
| 1:05         | 0:15      | Overview  II                |
| 1:20        | 0:25      | In Class Activity II      |
|1:45       | 0:05    | Wrap Up                     |
| TOTAL       | 1:50    |                          |


## Learning Objectives (5 min)

By the end of this lesson, you should be able to...

1. Describe:
- the **Observer** and **Mediator** patterns
- the software construction problem each is intended to solve
- potential use cases for each (when to use them)
3. Assess:
- the suitability of a given design pattern to solve a given problem
- the trade offs (pros/cons) inherent in each
4. Implement basic examples of both patterns explored in this class

## Initial Exercise (15 min)

### Part 1 - Individually

...__*SURPRISE!!!*__ ...__*time for another Quiz!*__

<!-- Quiz location:

-->

### Part 2 - In Pairs

Grade each other's quizzes, sharing answers, insights, etc.

## Overview/TT I (20 min)

### The Observer Pattern &nbsp;&nbsp;&nbsp;&nbsp;:eyes:

#### Description
The **Observer pattern** lets one object observe changes to the __*state*__ of another object without needing to know the implementation of the object observed.

Observer is comprised of __*two main objects:*__ <sup>1</sup>
1. **Subject** — The object under observation.
- The subject object __*allows observer objects to register*__ (and unregister) their interest in receiving updates (notifications) whenever changes are made to the subject, and it __*automatically notifies observers*__ of any state changes.<sup>2</sup>
- Subjects are __*responsible for maintaining a list of their dependents*__ (observers).
2. **Observer(s)** — The object(s) doing the observing.
- It is the responsibility of observers is __*to register (and unregister) themselves on a subject*__ (to get notified of state changes) and __*to update their state*__ (synchronize their state with subject’s state) when they are notified.

This makes subject and observers loosely coupled - subject and observers have no explicit knowledge of each other. Observers can be added and removed independently at run-time.

<sup>1</sup> *This notification-registration interaction is also known as* __*"publish-subscribe."*__

<sup>2</sup> *Another common actor in the Observer pattern is a* __*Client object.*__ *Subject objects often have methods to attach and detach observers to a client object.*

#### Implementation

The key to implementing the Observer pattern is to __*define the interactions*__ between the Subject and Observer objects __*using protocols*__. Subject and Observer protocols should contain methods to:

- Add observers
- Remove observers
- Notify observers

<!-- TODO: add notes on weak properties -->

**Simple Representation of Key Implementation Points**

The example below (in non-functioning pseudocode) illustrates the basic patterns involved in implementing the Observer pattern.

Key highlights:

- At item (2), notice that this `addObserver(_:)` function is set up to accept only a single observer. A better, more real-world design would likely accept a variable number of observers.
- Item (8) shows how the Subject object fulfills it responsibility to maintain a list of its observers.

```Swift
protocol Observable { // 1) Subject protocol
   func addObserver(observer:ObserverObject); // 2) Register
   func removeObserver(observer:ObserverObject); // 3) Unregister
}

protocol Observer: class { // 4)  Observer protocol
   func notify(event: Event)
}

class ObserverObject: Observer { // 5) Observer implementation

   weak var subject = Subject() // 6) Subject property

   func notify(event: Event) {
       // update Observer with changes to Subject
   }
}

class Subject: Observable { // 7) Subject implementation

   // 8) Subject maintains a list of its observers
   private var observerArray = [ObserverObject]()

   func addObserver(observer: ObserverObject) {
       // implement code to add observer
   }

   func removeObserver(observer: ObserverObject) {
       // implement code to remove observer

   }

   func changeSubjectState() {

       // make a change Subject state, then notify observers of change

       notifyObservers()
   }

   func notifyObservers() {
       observer.notify(event: Event)
   }
}
```


#### Problems Addressed





#### Benefits
.
- Why learn this?
- Industry examples of usage
- Best practices
- Personal anecdote


#### Pitfalls
.

#### When to use




-

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

### The Mediator Pattern &nbsp;&nbsp;&nbsp;::mailbox_with_no_mail::

#### Description



#### Implementation



#### Problems Addressed





#### Benefits
.

#### Pitfalls
.

#### When to use


## In Class Activity II (optional) (30 min)

## Wrap Up (5 min)

- Continue working on your current tutorial
- Complete reading
- Complete challenges

## Additional Resources

1. [Slides]()
2. [Observer pattern - wikipedia](https://en.wikipedia.org/wiki/Observer_pattern)
3. [Publish–subscribe pattern  - wikipedia](https://en.wikipedia.org/wiki/Publish–subscribe_pattern)
[]()
[]()
