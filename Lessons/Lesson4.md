# Behavioral Patterns Pt.2

<!-- INSTRUCTOR NOTES:
1) For the quiz in the Initial Exercise:
- the URL is xxxx
https://docs.google.com/document/d/1giZglDE141ewuj1fGunZhTqCRq0pA11SO-Sta_yYT60/edit

- Answers are listed in a comment in the Initial Exercise section

2) For Activity 1:
- see below Additional Resources

3) for Activity 2:
- see below Additional Resources
-->

## Minute-by-Minute

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

<!-- Quiz:

- location:
https://docs.google.com/document/d/1giZglDE141ewuj1fGunZhTqCRq0pA11SO-Sta_yYT60/edit

- Answers:
Question 1. a) App Delegate (Application object is also acceptable, as some Apple documentation stops there)
Question 1. b) It discards it

Question 2. A, G, B, F, C, E, D
-->

### Part 2 - In Pairs

Grade each other's quizzes, sharing answers, insights, etc.

### Part 3 - As A Class

Review: The After Class coding assignment from previous class.
- One or more students to share progress and implementation details with class.

## Overview/TT I (20 min)

### The Observer Pattern &nbsp;&nbsp;&nbsp;&nbsp;:eyes:

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

__*Note:*__ This is example is a non-functioning "shell" only provided to illustrate key implementation features of the pattern. __*It will not run in a playground.*__

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

##### Example Use Cases
Observer is **often used with MVC** where the view **controller is the observer** and the **model is the subject.** This allows the model to communicate changes back to the view controller without needing to know anything about the view controller’s type. Hence, different view controllers can use and observe changes on a shared model type.

### The Observer Pattern in iOS

There are several examples of the observer pattern in the Cocoa Touch and Cocoa frameworks. The Cocoa Touch implementation of the Observer pattern that most programmers encounter is in the UI frameworks, where user interactions and changes in UI component state are expressed using *events* (which are *a type of Notification*).

Cocoa implements the observer pattern in two ways:
- **Notifications**
- **Key-Value Observing (KVO)**

#### Notifications
Notifications are based on a subscribe-and-publish model that allows an object (the publisher) to send messages to other objects (subscribers/listeners). The publisher never needs to know anything about the subscribers.

Notifications are heavily used by Apple.

*(See lessons in MOB 1.3 for more on iOS Notifications)*

#### Key-Value Observing (KVO)
Objective-C has a feature called **Key-Value Observing (KVO)** that allows one object to receive notifications when the value of another object’s __*property*__ changes.

It is useful for communicating changes between logically separated parts of your app—such as between models and views.

You can use KVO to communicate between Swift objects as long as both of them are derived from `NSObject`, and you use the  `@objc dynamic` keyword when defining the property that will be observed.

__*Note:*__ *KVO is similar to property observers (`willSet` and `didSet`), except KVO is for adding observers outside of the type definition.*

**KVO’s biggest downside:** You’re required to subclass NSObject and use the Objective-C runtime.

#### Apple's KVO Implementation Steps

In [Using Key-Value Observing in Swift](https://developer.apple.com/documentation/swift/cocoa_design_patterns/using_key-value_observing_in_swift), Apple outlines KVO implemention in four simple steps:

1. Annotate a Property for Key-Value Observing
2. Define an Observer class
3. Associate the Observer with the Property to Observe
4. Respond to a Property Change

## In Class Activity I (30 min)

**TODO:** Complete and run the partially-implemented playground code below following the steps from Apple's *Using Key-Value Observing in Swift* document listed above.

__*Implementation Notes:*__
1. Your Subject class only needs to have:
- A variable called `counter`, initialized to `0`, and modified with
```Swift
@objc dynamic
```
2. Your Observer class needs this specific `init()`` function:
```Swift
  init(subject:Subject) {
        super.init()
        subject.addObserver(self, forKeyPath: "counter",
                            options: NSKeyValueObservingOptions.new, context: nil)
    }
   ```

**Partially-Implemented Playground Code**
```Swift
import Foundation;

/* Step 1: Create a Subject class and Annotate a Property for Key-Value Observing */

//TODO: Create Subject class...


/* Step 2: Define an Observer class */
class Observer : NSObject {

    //TODO: Add init()

    override func observeValue(forKeyPath keyPath: String?, of object: Any?, change: [NSKeyValueChangeKey : Any]?, context: UnsafeMutableRawPointer?) {

        print("Notification: \(String(describing: keyPath)) = \(String(describing: change?[NSKeyValueChangeKey.newKey]!))");

    }
}
/* Step 3: Associate the Observer with the Property to Observe */
let subject =
let observer =

/* Step 4: Respond to a Property Change */
subject.counter += 11
subject.counter = 99

/* RESULTS - Should print:
Notification: Optional("counter") = Optional(11)
Notification: Optional("counter") = Optional(99)
*/

```
<!-- Instructor Note: Solution to Activity  is below Additional Resources
-->

## Overview/TT II (20 min)

### The Mediator Pattern &nbsp;&nbsp;&nbsp;:mailbox_with_no_mail:

The **Mediator pattern** simplifies peer-to-peer communication between objects by introducing a __*mediator object*__ that acts as a __*communications broker*__ between other objects.

Instead of objects communicating directly - and thus requiring knowledge of each other's implementations (i.e., tight coupling) - __*peer objects send messages*__ to each other via the __*mediator object.*__

Mediator joins together colleagues (peers) who share a single interface.

#### Implementation Notes

Implementing Mediator typically involves some or all of the following components:
1. **Colleague protocol** - Defines methods and properties each colleague must implement.
2. **Colleague objects** — `Peer objects` that want to communicate with each other `implement the colleague protocol`. `Colleague objects` send messages to and receives messages from other colleagues through an associated mediator object.
3. **Mediator protocol** — Defines methods and properties the mediator class must implement.
4. **Mediator object** - `Implements the mediator protocol.` __*Coordinates and controls communication*__ between all colleague objects.
5. **Client object** – Creates colleagues and associates an appropriate mediator object with each.

__*When is the pattern implemented correctly?*__  
 - When each object deals only with the mediator and has no direct knowledge of its peers.


 <!-- TODO: Add examples of protocols and objects from resources
 -->

#### Problem(s) Addressed

Designing groups of interdependent and/or reusable obects which need to communicate with one another can easily result in tight coupling.

#### Benefits

This design pattern __*promotes loose coupling*__ by keeping objects from referring to each other explicitly, and it __*lets you vary their interaction independently.*__

Mediator reduces chaotic dependencies between objects. The pattern restricts direct communications between the objects and forces them to collaborate indirectly, and only through a mediator object.

As a result, the __*components depend only on a single mediator class*__ instead of being coupled to dozens of their colleagues.

#### Pitfalls

- It is important that the mediator object *not* provide peers with access to one another so that they might become interdependent.

- Over time, a mediator object can evolve into a __*God Object.*__ <sup>3</sup>

#### When to use

Use this pattern when...

- __*dealing with a group of objects*__ that need to communicate freely between one another.
- __*designing reusable components,*__ but dependencies between the potentially reusable pieces might result in tight coupling.
- you need one or more __*colleagues to act upon events initiated by another colleague*__ and want this colleague to generate further events which, in turn, further affect other colleagues.

**Do not use** this pattern if you have one object that needs to send notifications to a range of disparate objects — consider using the Observer pattern instead.

__*Example Use Case -*__ The most popular usage of the Mediator pattern in Swift code is facilitating communications between GUI components of an app. *The Mediator objects fits into the* __*Controller*__ *role of MVC.*

<!-- TODO: add related patterns
-->

## In Class Activity II (30 min)

The playground code below is not complete...

When completed, it will loosely emulate a common real-world scenario in which various categories of "peers" communicate across the same system.

The seeks to implement the Mediator pattern by:
- creating Colleague and Mediator protocols
- creating a base implementation class that conforms to the Colleague protocol, and creating classes/objects by extending that base classes
- creating an implementation of a class that conforms to the Mediator protocol to coordinate communication between disparate peer objects
- using a Client object to make message requests, through the mediator, for each type of peer

**TODO:** Your job is to complete the code so that its output will match the output listed in the comment below the code snippet
- __*TIP*__ All of the places where the code is incomplete are neatly marked with "//TODO:" annotation.

```Swift
import UIKit

// Colleague protocol
protocol Receiver {
    associatedtype MessageType
    func receive(message: MessageType)
}

// Mediator protocol {
protocol Sender {
    associatedtype MessageType
    associatedtype ReceiverType: Receiver

    var recipients: [ReceiverType] { get }

    func send(message: MessageType)
}

// Concrete base class implementation of Colleague protocol
class Peer: Receiver {
    var name: String

    init(name: String) {
        self.name = name
    }

    func receive(message: String) {
        print("\(name) received: \(message)")
    }
}

// First Colleague class extending base Peer class
class Programmer: Peer {
    let expertise: String

    init(name: String, expertise: String) {

        //TODO: Complete init()

        super.init(name: name)
    }

    override func receive(message: String) {
        print("\(name) received: \(message) for possible \(expertise) work")
    }
}

// Another Colleague class extending base Peer class
class Recruiter: Peer {

    //TODO: add custom property required

    init(name: String, company: String) {

        //TODO: Complete init()

    }

    //TODO: Create and complete required function override
}

// Concrete implementation of Mediator protocol
final class MessageMediator: Sender {
    internal var recipients: [Peer] = []

    func add(recipient: Peer) {
        recipients.append(recipient)
    }

    func send(message: String) {
        for recipient in recipients {
            recipient.receive(message: message)
        }
    }
}

// Client
class SpamGenerator {
    func spamSpamSpamSpam(message: String, worker: MessageMediator) {
        worker.send(message: message)
    }
}

let messagesMediator = MessageMediator()
let spamGenerator = SpamGenerator()

let programmer0 = Programmer(name: "Hedy Lamar", expertise: "iOS Development")
let programmer1 = Programmer(name: "Michael Faraday", expertise: "Electrical Engineering")
let recruiter1 = Recruiter(name: "Queen Elizabeth I", company: "Apple")

messagesMediator.add(recipient: programmer0)
messagesMediator.add(recipient: programmer1)
messagesMediator.add(recipient: recruiter1)

spamGenerator.spamSpamSpamSpam(message: "I'd Like to Add you to my LinkedIn Network", worker: messagesMediator)

/* When successfully completed, the last line of the code will print:
 Hedy Lamar received: I'd Like to Add you to my LinkedIn Network for possible iOS Development work
 Michael Faraday received: I'd Like to Add you to my LinkedIn Network for possible Electrical Engineering work
 Queen Elizabeth I received: I'd Like to Add you to my LinkedIn Network. I am a recruiter at Apple
 */
```
<!-- Instructor Note: Solution to Activity  is below Additional Resources
-->

## After Class

1. Look up these other Behavioral Patterns:
- Visitor
- Iterator
- Memento
- Strategy
2. Research the following concepts:
- The Lapsed Listener Problem
- `NSKeyValueObserving` and its `addObserver` function
- `NSKeyValueChangeKey`
- `NSKeyValueObservingOptions`
3. **TODO:** Extend the Media Player app you created in the previous class by implementing the following using either the Observer or the Mediator pattern:
- add a notification that, when the video clip is done playing, sends the user this message: "Your media file is done playing — do you want to replay it?"
4. **TODO:** Analyze the following simple implementation of the Observer pattern (KVO).
- For discussion in next class, pay particular attention to the `.observe(_:_)` function, especially the implications of its origin (where does it come from?) and purpose.
```Swift
import UIKit

@objc class Person: NSObject {
    @objc dynamic var name = "Taylor Swift"
}

let taylor = Person()
print(taylor.name)// prints ""Taylor Swift"

taylor.observe(\Person.name, options: .new) { person, change in
    print("I'm now called \(person.name)")
}

taylor.name = "Justin Bieber" // prints "I'm now called Justin Bieber"
```

## Wrap Up (5 min)

- Continue working on your current tutorial
- Complete reading
- Complete challenges

## Additional Resources

1. [Slides]()
2. [Observer pattern - wikipedia](https://en.wikipedia.org/wiki/Observer_pattern)
3. [Publish–subscribe pattern  - wikipedia](https://en.wikipedia.org/wiki/Publish–subscribe_pattern)
4. [Mediator pattern - wikipedia](https://en.wikipedia.org/wiki/Mediator_pattern)
4. [God Object - wikipedia](https://en.wikipedia.org/wiki/God_object) <sup>3</sup>
5. [Using Key-Value Observing in Swift](https://developer.apple.com/documentation/swift/cocoa_design_patterns/using_key-value_observing_in_swift)
6. [Lapsed Listener Problem - wikipedia](https://en.wikipedia.org/wiki/Lapsed_listener_problem)
7. [Design Patterns on iOS using Swift – Part 2/2 - from Ray Wenderlich](https://www.raywenderlich.com/476-design-patterns-on-ios-using-swift-part-2-2)
- Contains descriptions and examples of the Observer pattern in iOS, including both Notifications and KVO, with a simple, excellent KVO example in which a `UIActivityIndicator` is stopped when there is a change to an `image property`.


<!-- TODO: add:
the lapsed listener problem
https://en.wikipedia.org/wiki/Hedy_Lamarr
-->


<!-- Solution to Activity I:
import Foundation

/* Step 1: Create a Subject class and Annotate a Property for Key-Value Observing */
class Subject : NSObject {
    @objc dynamic var counter = 0
}

/* Step 2: Define an Observer class */
class Observer : NSObject {

    init(subject:Subject) {
        super.init()
        subject.addObserver(self, forKeyPath: "counter",
                            options: NSKeyValueObservingOptions.new, context: nil)
    }

    override func observeValue(forKeyPath keyPath: String?, of object: Any?, change: [NSKeyValueChangeKey : Any]?, context: UnsafeMutableRawPointer?) {

        print("Notification: \(String(describing: keyPath)) = \(String(describing: change?[NSKeyValueChangeKey.newKey]!))");

    }
}
/* Step 3: Associate the Observer with the Property to Observe */
let subject = Subject()
let observer = Observer(subject: subject)

/* Step 4: Respond to a Property Change */
subject.counter += 11
subject.counter = 99

-->

<!-- Solution to Activity II:
import UIKit

// Colleague protocol
protocol Receiver {
    associatedtype MessageType
    func receive(message: MessageType)
}

// Mediator protocol {
protocol Sender {
    associatedtype MessageType
    associatedtype ReceiverType: Receiver

    var recipients: [ReceiverType] { get }

    func send(message: MessageType)
}

// Concrete base class implementation of Colleague protocol
class Peer: Receiver {
    var name: String

    init(name: String) {
        self.name = name
    }

    func receive(message: String) {
        print("\(name) received: \(message)")
    }
}

// Colleague class extending base Peer class
class Programmer: Peer {
    let expertise: String

    init(name: String, expertise: String) {
        self.expertise = expertise
        super.init(name: name)
    }

    override func receive(message: String) {
        print("\(name) received: \(message) for possible \(expertise) work")
    }
}

// Colleague class extending base Peer class
class Recruiter: Peer {
    let company: String

    init(name: String, company: String) {
        self.company = company
        super.init(name: name)
    }

    override func receive(message: String) {
        print("\(name) received: \(message). I am a recruiter at \(company)")
    }
}

// Concrete implementation of Mediator protocol
final class MessageMediator: Sender {
    internal var recipients: [Peer] = []

    func add(recipient: Peer) {
        recipients.append(recipient)
    }

    func send(message: String) {
        for recipient in recipients {
            recipient.receive(message: message)
        }
    }
}

// Client
class SpamGenerator {
    func spamSpamSpamSpam(message: String, worker: MessageMediator) {
        worker.send(message: message)
    }
}

let messagesMediator = MessageMediator()
let spamGenerator = SpamGenerator()

let programmer0 = Programmer(name: "Hedy Lamar", expertise: "iOS Development")
let programmer1 = Programmer(name: "Michael Faraday", expertise: "Electrical Engineering")
let recruiter1 = Recruiter(name: "Queen Elizabeth I", company: "Apple")

messagesMediator.add(recipient: programmer0)
messagesMediator.add(recipient: programmer1)
messagesMediator.add(recipient: recruiter1)

spamGenerator.spamSpamSpamSpam(message: "I'd Like to Add you to my LinkedIn Network", worker: messagesMediator)

/* The last line of the code will Print:
Hedy Lamar received: I'd Like to Add you to my LinkedIn Network for possible iOS Development work
Michael Faraday received: I'd Like to Add you to my LinkedIn Network for possible Electrical Engineering work
Queen Elizabeth I received: I'd Like to Add you to my LinkedIn Network. I am a recruiter at Apple
 */
-->
