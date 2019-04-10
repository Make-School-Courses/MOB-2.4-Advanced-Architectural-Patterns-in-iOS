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

TODO: Add quiz answersz

-->

### Part 2 - In Pairs

Grade each other's quizzes, sharing answers, insights, etc.

### Part 3 - As A Class

Review After Class coding assignment from previous class. One or more students to share progress and implementation details with class.

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

#### Implementation Notes

The observer pattern is implemented correctly when an object can receive notifications without being tightly coupled to the object that sends them.

The key to implementing the Observer pattern is to __*define the interactions*__ between the Subject and Observer objects __*using protocols*__. Subject and Observer protocols should contain methods to:

- **Add Observers**
- **Remove Observers**
- **Notify Observers**

__*Weak References:*__
Best practice is to keep only weak references to all observers. Otherwise, it’s easy to introduce retain cycles, especially when the owner of an observed object is also an observer itself.

**Simple Representation of Key Implementation Points**

The example below (in non-functioning pseudocode) illustrates the basic patterns involved in implementing the Observer pattern.

__*Key Highlights:*__

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

- A one-to-many dependency between objects should be defined without making the objects tightly coupled.

- It should be possible that when one object changes state an open-ended number of dependent objects are updated automatically.

- A single object should be able to notify an open-ended number of other objects.

#### Benefits

- Observer simplifies application design by allowing objects that provide notifications to do so in a uniform way without needing to know how those notifications are processed and acted on by the recipients (i.e., without being tightly coupled).

- It allows us to define “one-to-many” relationships between many observers receiving updates from the same subject.

- The observer pattern allows large and complex groups of objects to cooperate with one another with few dependencies between them.

##### Why learn this?

The Observer pattern is so widely used that you are likely to have come across it if you have developed an application using a __*modern UI component framework.*__

It plays a key part in the familiar **model–view–controller (MVC)** architectural pattern. It is implemented in numerous programming libraries and systems, __*including almost all GUI toolkits.*__


#### Pitfalls

- **Biggest pitfall:** Allowing objects that send and receive notifications to become interdependent.

- Observer __*can cause memory leaks*__: In basic implementation, it requires explicit registration and unregistration. If Subjects hold strong references to Observer to keep them alive, **retain cycles can occur.** Ensuring Subjects hold **weak references to Observers** whenever possible can prevent this.

#### When to use

Use the Observer pattern whenever you want one object to receive changes made on another object but where the sender (Subject) of the notifications does not depend on the recipient (Observer) to complete its work.

__*Do not use*__ the Observer pattern unless the Subject of the notifications is functionally dependent from the recipients (observers): i.e., the observers could be removed from the application without preventing the subject from performing its work.

##### - Example Use Cases
Observer is **often used with MVC** where the view **controller is the observer** and the **model is the subject.** This allows the model to communicate changes back to the view controller without needing to know anything about the view controller’s type. Hence, different view controllers can use and observe changes on a shared model type.

<!-- TODO: Add notes about iOS and Notifications vs KVO , and we did Notificaions in MOB 1.3
-->


## In Class Activity I (30 min)



## Overview/TT II (optional) (20 min)

### The Mediator Pattern &nbsp;&nbsp;&nbsp;:mailbox_with_no_mail:

#### Description
The **Mediator pattern** simplifies peer-to-peer communication between objects by introducing a __*mediator object*__ that acts as a __*communications broker*__ between other objects.

Instead of objects communicating directly - and thus requiring knowledge of each other's implementations (i.e., tight coupling) - __*peer objects send messages*__ to each other via the __*mediator object.*__

Mediator joins together colleagues (peers) who share a single interface.

#### Implementation Notes

Implementing Mediator typically involves some or all of the following components:
1. **Colleague protocol** - Defines methods and properties each colleague must implement.
2. **Colleague objects** — Peer objects which want to communicate with each other implement the `colleague protocol`. Colleague objects sends message to and receives messages from other colleagues through an associated mediator object.
3. **Mediator protocol** — Defines methods and properties the mediator class must implement.
4. **Mediator object** - Implements the mediator protocol. Coordinates and controls communication between all colleague objects.
5. **Client object** – Creates colleagues and associates an appropriate mediator object with each.

*When is the pattern implemented correctly?*  
 - When each object deals only with the mediator and has no direct knowledge of its peers.

#### Problems Addressed

Mediator promotes loose coupling by keeping objects from referring to each other explicitly, and it lets you vary their interaction independently.

#### Benefits

This design pattern __*promotes loose coupling*__ by keeping objects from referring to each other explicitly, and it __*lets you vary their interaction independently.*__

Mediator reduces chaotic dependencies between objects. The pattern restricts direct communications between the objects and forces them to collaborate indirectly, and only through a mediator object.

As a result, the __*components depend only on a single mediator class*__ instead of being coupled to dozens of their colleagues.

#### Pitfalls

It is important that the mediator *not* provide peers with access to one another so that they might become interdependent.

#### When to use

Use this pattern when:
- dealing with a group of objects that need to communicate freely between one another.
- designing reusable components, but dependencies between the potentially reusable pieces might result in tight coupling.
- you need one or more colleagues to act upon events initiated by another colleague and want this colleague to generate further events which, in turn, further affect other colleagues.

**Do not use** this pattern if you have one object that needs to send notifications to a range of disparate objects — consider using the Observer pattern instead.

__*Example Use Case:*__ The most popular usage of the Mediator pattern in Swift code is facilitating communications between GUI components of an app. *The Mediator objects fits into the Controller role of MVC.*

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

the lapsed listener problem
