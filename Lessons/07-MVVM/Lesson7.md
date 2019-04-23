# MVVM

<!-- INSTRUCTOR NOTES:
1) For the QuizLet Game in the Initial Exercise:
- the URL is https://quizlet.com/_6hmrxi

2) For Activity 1:
- xxxx
3) for Activity 2:
- xxx
-->

## Minute-by-Minute

| **Elapsed** | **Time**  | **Activity**              |
| ----------- | --------- | ------------------------- |
| 0:00        | 0:05      | Objectives                |
| 0:05        | 0:20      | Initial Exercise          |
| 0:25        | 0:15      | Overview                  |

| 0:20        | 0:45      | In Class Activity I       |
| 1:05        | 0:10      | BREAK                     |
| 1:15        | 0:45      | In Class Activity II      |
| TOTAL       | 2:00      |                           |


## Learning Objectives (5 min)

By the end of this lesson, you should be able to...

1. Describe:
- the **MVVM** design pattern
- the software construction problem(s) it is intended to solve
- potential use cases for it (when to use it; when not to use it)
3. Assess:
- the suitability of a given design pattern to solve a given problem
- the trade offs (pros/cons) inherent in choosing high-level (MVC, MVVM, etc.) design patterns
4. Implement basic examples of MVVM explored in this class


<!-- 1. Identify and describe
1. Define
1. Design
1. Implement -->

## Initial Exercise (20 min)

### As A Class

#### A QuizLet Game

...test your knowledge of design patterns in Swift!


## Overview/TT I (20 min)


### Model-View-ViewModel

The **MVVM** is a __*Structural*__ design pattern which introduces a *fourth* component to MVC — *the* __*View Model.*__

The idea behind the MVVM pattern is that any **View** *with business logic specific to itself* should be backed by a **View Model** that represents and handles the data for the **View.**

In MVVM, we implement *presentational* business logic - such as converting a Date into a date-formatted String - in the __*ViewModel*__ *instead* of in the View or the Controller.

<!-- TODO: Insert: example code (cell?) and/or diagram here? -->


### A Brief History

MVVM was invented by Microsoft architects Ken Cooper and Ted Peters specifically to simplify event-driven programming of user interfaces.

MVVM was designed to make use of data binding functions in WPF (Windows Presentation Foundation) to better facilitate the separation of view layer development from the rest of the pattern, by removing virtually all GUI code ("code-behind") from the view layer.

*Source: wikipedia*

<!-- TODO: add more detail from notes here -->



### Four Components of MVVM

MVVM is very similar to MVC and compliments it exceptionally well. It can be seen as an extension of MVC's primary intent: separating the View from the Model and utilizing the Controller as a central "manager" between View and Model.

MVVM takes the principle of *Separation of Concerns* one step further &mdash; it adds a __*special layer*__ between the View and the Model (called the `ViewModel` or `View Model`) which __*allows Controllers to delegate data presentation responsibilities to the View Model.*__

Here is how the four major components of MVVM relate to each other (and to MVC):

**View** &mdash; Responsible for displaying visual elements and controls on the screen. Typically, subclasses of `UIView`. </br>
(Same as in MVC)

**Model** &mdash; Objects that hold app data; typically, `structs` or simple `classes`. (Same as in MVC)

**View Controller** &mdash; In MVVM, VCs still set up UIView objects, but *they do not interact with the model.* Instead, the VC uses the View Model as a *mediator* and asks for what it needs in a format that will be ready for presentation. In MVVM, Controllers should have absolutely no business logic.

**View Model** &mdash; Transforms Model data into values that can be displayed on a View. Sits between the View Controller and Model. Can be a `class` or a `struct`,  but it is *typically a class* so that references of the same instance can be passed around in code.


### Problem(s) Addressed

MVVM can be used to solve two related development issues:

1. **"MVC: Massive View Controller"** &mdash; In MVC, where do you put functionality that does not belong neatly in either the View or the Model?

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; For expediency, iOS developers are too often tempted to use View Controllers as a "catch-all" component </br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; for such code, which results in bloated View Controllers.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; __*Example*__ </br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Data formatting is a common task. Imagine your app needs data &mdash; dates, currency, etc. &mdash; *formatted* </br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *differently* for various user locales. The data is stored in the Model layer, and the View displays the </br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; formatted data &mdash; *but which component should be responsible for formatting the data?*
</br>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Implementing MVVM, the View Model could handle data formatting, freeing up the View Controller </br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; to do its primary job: Responding to `viewDidLoad()` and other View lifecycle events, handling </br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; View callbacks through IBActions, and so on.

2. **Tight Coupling Between MVC Components** &mdash; In the following code snippet, assume that each reusable cell will be populated with data from separate user records when the `configureWithUser(_:)` function is executed:


```Swift
    var userCell = tableView.dequeueReusableCellWithIdentifier("identifier") as UserCell
    userCell.configureWithUser(user)
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- In this design, the cell (the View) is configured directly with the Model, violating MVC guidelines. </br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- You could refactor it by configuring the cell from the Controller, which might follow MVC, but will </br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; increase the size of the Controller.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Such a problem might not be evident until you implement Unit Testing. Because the __*Controller is*__ </br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; __*tightly coupled with the View,*__ it becomes __*difficult to test*__ due to the added complexity of </br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; mocking up views and their life cycles and keeping them all in sync with the Model.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; With MVVM, the business logic required to supply presentation data to the View can be separated from </br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; View layout code.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; When the View Model knows nothing about View layout, testing each - separately or together - is much easier.


### Benefits

1. __*Separation of Concerns*__ &mdash; MVVM can create a much clearer separation of concerns between Model, View and Controller providing several advantages: </br>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- It allows developers to break an app into smaller components, which facilitates easier debugging, testing, and code readability. </br>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- Due to the decoupling of UI and business logic, the MVVM design pattern results in more flexible code. </br>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- MVVM can go a long way to solve the "Massive View Controller" problem by decreasing the code size of View Controllers by delegating some of a VC's tasks to a View Model.

2. __*Testability*__ &mdash; MVVM makes it easy to test the logic behind the views. By moving a ViewController’s business logic into a ViewModel it becomes much easier to create unit tests of the business logic and the View layout code.


### Pitfalls


A criticism of the pattern comes from MVVM creator John Gossman himself,[12] who points out that the overhead in implementing MVVM is "overkill" for simple UI operations. He says that for larger applications, generalizing the ViewModel becomes more difficult. Moreover, he illustrates that data binding in very large applications can result in considerable memory consumption.

However, the cost of MVVM can be a bit high as sometimes it is difficult to figure one’s way around binding and other technicalities of MVVM.

There is one bitter truth about reactive frameworks: the great power comes with the great responsibility. It’s really easy to mess up things when you go reactive. In other words, if you do something wrong, you might spend a lot of time debugging the app, so just take a look at this call stack.

MVVM works well if your app requires many model-to-view transformations. However, not every object will neatly fit into the categories of model, view or view model. Instead, you should use MVVM in combination with other design patterns.
Furthermore, MVVM may not be very useful when you first create your application. MVC may be a better starting point.

It’s
okay to introduce MVVM later in an app’s lifetime when you really need it.



### When to Use



Use this pattern when you need to transform models into another representation for a view. For example, you can use a view model to transform a Date into a date-formatted String, a Decimal into a currency-formatted String, or many other useful transformations.


especially in situations which require several model-to-view transformations.



## In Class Activity I (15 min)

### Individually

<!-- TODO:
1) Does this need a BEFORE example?
- see original URL

2) needs explanatory text/instructions:

**TODO:** Diagram
 -->



```Swift

import UIKit
import PlaygroundSupport

struct Person { // Model
    let firstName: String
    let lastName: String
}

protocol GreetingViewModelProtocol: class {
    var greeting: String? { get }
    var greetingDidChange: ((GreetingViewModelProtocol) -> ())? { get set }
    init(person: Person)
    func showGreeting()
}

class GreetingViewModel : GreetingViewModelProtocol {
    let person: Person

    var greeting: String? {
        didSet {
            self.greetingDidChange?(self)
        }
    }

    var greetingDidChange: ((GreetingViewModelProtocol) -> ())?

    required init(person: Person) {
        self.person = person
    }

    func showGreeting() {
        self.greeting = "Hello " + self.person.firstName + " " + self.person.lastName
    }
}

class GreetingViewController : UIViewController {
    var viewModel: GreetingViewModelProtocol? {
        didSet {
            self.viewModel?.greetingDidChange = { [unowned self] viewModel in
                self.greetingLabel.text = viewModel.greeting
            }
        }
    }
    var showGreetingButton: UIButton!
    var greetingLabel: UILabel!

    override func viewDidLoad() {
        super.viewDidLoad()

        self.view.frame = CGRect(x: 0, y: 0, width: 320, height: 480)

        self.setupUIElements()
        self.layout()
    }

    func setGreeting(greeting: String) {
        self.greetingLabel.text = greeting
    }

    func setupUIElements() {
        self.title = "Test"

        self._setupButton()
        self._setupLabel()
    }

    private func _setupButton() {
        self.showGreetingButton = UIButton()
        self.showGreetingButton.setTitle("Click me", for: .normal)
        self.showGreetingButton.setTitle("You badass", for: .highlighted)
        self.showGreetingButton.setTitleColor(UIColor.white, for: .normal)
        self.showGreetingButton.setTitleColor(UIColor.red, for: .highlighted)
        self.showGreetingButton.translatesAutoresizingMaskIntoConstraints = false
        self.showGreetingButton.addTarget(self, action: #selector(didTapButton(sender:)), for: .touchUpInside)
        self.view.addSubview(self.showGreetingButton)
    }

    private func _setupLabel() {
        self.greetingLabel = UILabel()
        self.greetingLabel.textColor = UIColor.white
        self.greetingLabel.textAlignment = .center
        self.greetingLabel.translatesAutoresizingMaskIntoConstraints = false

        self.view.addSubview(self.greetingLabel)
    }

    func layout() {
        self._layoutButton()
        self._layoutLabel()

        self.view.layoutIfNeeded()
    }

    private func _layoutButton() {
        // layout button at the center of the screen
        let cs1 = NSLayoutConstraint(item: self.showGreetingButton, attribute: .centerX, relatedBy: .equal, toItem: self.view, attribute: .centerX, multiplier: 1.0, constant: 1.0)
        let cs2 = NSLayoutConstraint(item: self.showGreetingButton, attribute: .centerY, relatedBy: .equal, toItem: self.view, attribute: .centerY, multiplier: 1.0, constant: 1.0)

        self.view.addConstraints([cs1, cs2])
    }

    private func _layoutLabel() {
        // layout label at the center, bottom of the screen
        let cs1 = NSLayoutConstraint(item: self.greetingLabel, attribute: .centerX, relatedBy: .equal, toItem: self.view, attribute: .centerX, multiplier: 1.0, constant: 1.0)
        let cs2 = NSLayoutConstraint(item: self.greetingLabel, attribute: .bottom, relatedBy: .equal, toItem: self.view, attribute: .bottom, multiplier: 1.0, constant: -10)
        let cs3 = NSLayoutConstraint(item: self.greetingLabel, attribute: .width, relatedBy: .equal, toItem: self.view, attribute: .width, multiplier: 0.70, constant: 0)

        self.view.addConstraints([cs1, cs2, cs3])
    }

    @objc func didTapButton(sender: UIButton) {
        guard let vm = self.viewModel else { return }

        vm.showGreeting()
    }
}

// Assembling of MVVM
let model = Person(firstName: "Nikola", lastName: "Tesla")
let view = GreetingViewController()
let viewModel = GreetingViewModel(person: model)
view.viewModel = viewModel

PlaygroundPage.current.liveView = view.view

```

<!-- TODO: Attribute this to URL...with MIT License? -->


## Overview/TT II (20 min)


### View Model - A Closer Look


but also the Mediator, represented as the View Model.


View models are classes that take objects and transform them into different objects, which can be passed into the view controller and displayed on the view. They’re especially useful for converting computed properties such as Date or Decimal into a String or something else that actually can be shown in a UILabel or UIView.
a view model abstracts or hides the model from the controller. The view model exposes an interface to the controller for displaying information about the model. The controller does not have direct access to the model.
The view model exposes an interface to the controller for displaying information about the model. The controller does not have direct access to the model.

If you’re only using the view model with one view, it can be good to put all the configurations into the view model. However, if you’re using more than one view, you might find that putting all the logic in the view model clutters it. Having the configure code separated into each view may be simpler.


View model
The view model is an abstraction of the view exposing public properties and commands. Instead of the controller of the MVC pattern, or the presenter of the MVP pattern, MVVM has a binder, which automates communication between the view and its bound properties in the view model. The view model has been described as a state of the data in the model.[7]
The main difference between the view model and the Presenter in the MVP pattern, is that the presenter has a reference to a view whereas the view model does not. Instead, a view directly binds to properties on the view model to send and receive updates. To function efficiently, this requires a binding technology or generating boilerplate code to do the binding.[6]

View Model: The view model is basically a representation of the view controller. If the view controller has a label, the view model should have a property to supply it with the text in string form. It triggers all calls, and sends and receives data. When dealing with the view model, you should ensure it is as dumb as possible. This means that you should decouple it from the view controller as much as possible. We should ensure that we do not inject instances of the view controller to the view model. The view model should be completely independent of all the view controller.
The View Model can be thought of as a representation of the view controller. (VC’s specific functionality, designed for specific functionality — not ViewDid Load, etc.)


So what is the View Model in the iOS reality? It is basically UIKit independent representation of your View and its state.

The View Model invokes changes in the Model and updates itself with the updated Model, and since we have a binding between the View and the View Model, the first is updated accordingly.


Your view model should be as dumb as possible. It should not contain networking code or data access code. When you start performing networking operations inside view model you are adding tight coupling between the view model layer and the web services layer.

Networking and data access operations should be isolated from the view models and should be part of separate classes or even separate framework/library. Depending on your application, networking and data access operations can be passed into the view controller constructor as dependency injections.


That is, the ViewModel provides a set of interfaces, each of which represents a UI component in the View. We use a technique called “binding” to connect UI components to ViewModel interfaces. So, in MVVM, we don’t touch the View directly, we deal with business logic in the ViewModel and thus the View changes itself accordingly. We write presentational things such as converting Date to String in the ViewModel instead of the View.



Because view models have a close relationship with the models they consume, they're considered more model than view.


### Bindings


<sup>1</sup> *note:
Model–view–viewmodel is also referred to as model–view–binder, especially in implementations not involving the .NET platform. ZK (a web application framework written in Java) and KnockoutJS (a JavaScript library) use model–view–binder*


### How to implement it?


The implementation of a view model is usually straightforward. All it does is translate data from the model to values the view(s) can display. The controller is no longer responsible for this ungrateful task.


The view model of MVVM is a value converter,[1] meaning the view model is responsible for exposing (converting) the data objects from the model in such a way that objects are easily managed and presented. In this respect, the view model is more model than view, and handles most if not all of the view's display logic.[1] The view model may implement a mediator pattern, organizing access to the back-end logic around the set of use cases supported by the view.


<!-- TODO: implement the Components
implment or refactor to View Model
add binding
-->



### MVVM in iOS

MVVM has been gaining traction in the Cocoa community. It's commonly referred to as the Model-View- ViewModel pattern, MVVM for short.
The origins of the MVVM pattern lead back to Microsoft and it continues to be used in modern Windows development.


## In Class Activity II (30 min)



## After Class

1. Research these related concepts:

- xxxx

<!-- Binding and MVVM in ios -->


2. **TODO:** - Continue working on your Course Project

## Wrap Up (5 min)

- Continue working on your current tutorial
- Complete reading
- Complete challenges

## Additional Resources

1. Links to additional readings and videos
