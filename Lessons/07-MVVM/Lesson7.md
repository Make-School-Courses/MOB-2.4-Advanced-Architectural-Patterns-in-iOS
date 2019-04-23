# MVVM

<!-- INSTRUCTOR NOTES:
1) For the QuizLet Game in the Initial Exercise:
- the URL is https://quizlet.com/_6hmrxi

2) For Activity 1:
- is just diagraming on boards
3) for Activity 2:
- use starter app listed in exercise
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

1. __*Separation of Concerns*__ &mdash; MVVM can create a much clearer separation of concerns between Model, View and Controller providing several advantages:
- It allows developers to break an app into smaller components, which facilitates easier debugging, testing, and code readability.
- Due to the decoupling of UI and business logic, the MVVM design pattern results in more flexible code. 
- MVVM can go a long way to solve the "Massive View Controller" problem by decreasing the code size of View Controllers by delegating some of a VC's tasks to a View Model.

2. __*Testability*__ &mdash; MVVM makes it easy to test the logic behind the views. By moving a ViewController’s business logic into a ViewModel it becomes much easier to create unit tests of the business logic and the View layout code.


### Pitfalls of MVVM

With great power comes great responsibility...

The cost of MVVM can be a bit high as sometimes it is difficult to figure one’s way around binding and other technicalities of MVVM. If you do something wrong, you might spend a lot of time debugging your app.

Noteworthy criticism of the pattern comes from MVVM creator, John Gossman, himself:
- the overhead in implementing MVVM is "overkill" for simple UI operations.
- for larger applications, generalizing the ViewModel becomes more difficult.
- data binding in very large applications can result in considerable memory consumption.

*Source: wikipedia*


### When to Use MVVM

Use MVVM when you need to transform models into another representation for a View, especially in situations which require several model-to-view transformations.

For example, you can use a View Model to configure a table cell, transform a Date into a date-formatted String, a Decimal into a currency-formatted String, or many other useful View transformations.

## In Class Activity I (15 min)

### Individually

**TODO:** Analyze the Playground code below and __*diagram*__ how it implements MVVM.
Emphasize in your diagram:
- how this implementation changes MVC into MVVM, especially which class(es) comprise the View Model
- the relationship between the View Model and the View Controller

**Q:** How does this design free up the View Controller?


**Playground Code:**

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
*Excerpted from:*
https://gist.github.com/BohdanOrlov/bdb64ae4ca83a2fca3af



## Overview/TT II (20 min)


### View Model - A Closer Look

Note that using a **View Model** is actually an example of the __*Mediator pattern.*__

View Models can be thought of as representations of the View Controller which are designed to handle a specific subset of functionality that a VC might otherwise handle (though *not designed to handle* `viewDidLoad()` and other lifecycle functions handled by VCs).

It exposes an interface to the Controller for displaying information about the Model: it *hides* the Model from the Controller.

**View Models** are:
- an abstraction of the view exposing public properties and commands.
- considered more Model than View, because View Models have a close relationship with the Models they consume.
- classes that take objects and transform them into different objects which can be passed into the view controller and displayed on the view.
- especially useful for converting computed properties - such as a Date or a Decimal - into a String or other data type that can be shown in a UILabel or UIView.

**Recommended Practices** </br>
When dealing with the View Model, ensure it is *as "dumb" as possible:*
- Decouple it from the View Controller as much as possible.
- Avoid tight coupling between the View Model layer and web service or data access layers.

If only using a View Model with a single View, it can be good to put all configurations and set up code into the View Model. If you’re using __*more than one view,*__ you might find that putting all the logic in one view model complicates and clutters it. In those cases, creating __*a separate View Model*__ specific to __*each type of View*__ might declutter and simplify the implementation (by further separating concerns).


### Bindings
The View Model provides a set of interfaces, each of which represents a UI component in the View. We can use a technique called __*“binding”*__<sup>1</sup> to *connect UI components to ViewModel interfaces.*

Binding refers to the flow of information between Views and View Models; a View directly binds to properties on the View Model to send and receive updates. If View Model properties change, those changes can be immediately and automatically reflected on the View.

Instead of the controller of the MVC pattern, MVVM<sup>2</sup> often employ a *binder,* which automates communication between the View and its bound properties in the View Model.

Most frameworks employ the __*Observer pattern*__ as the underlying binding mechanism.


### MVVM in iOS

MVVM has been gaining traction in the Cocoa and Cocoa Touch communities because of its potential to resolve the Massive-View-Controller problem and to facilitate Unit Testing of presentation logic.

And, although bindings are built in to macOS frameworks, we do not have built-in bindings in iOS. Though less convenient to use than built-in bindings, we can use Key-Value-Observing and Notifications to implement bindings between View properties and View Model behaviors in iOS.


### How to implement it?
The implementation of a View Model is usually straightforward:
- Identify opportunities to free up View Controllers from data formatting or other presentation tasks
- Create a View Model to handle those tasks

Whenever possible, it is recommended to implement a data binding mechanism (KVO, Notifications) to automatically handle data state changes between the View and the View Model.


## In Class Activity II (25 min)

**Required Resources:**
- Internet access to the News API Web Service API: https://newsapi.org
- The [iOS-NewsApp_Starter](https://github.com/Make-School-Labs/iOS-NewsApp_Starter) app, which includes a pre-built table view ready to present the results of a data fetch.

<!--
< for reference >
https://medium.com/@azamsharp/mvvm-in-ios-from-net-perspective-580eb7f4f129 -->


### Part 1 - Refactor the data source (array)

**TODO:** Refactor the `sources` array below into an appropriate construct which implements MVVM.

```Swift
class SourceViewController: UITableViewController {

    //TODO: Using MVVM, refactor this datasource array
    var sources: [SourceItem] = []

    ...
```

### Part 2 - Respond to Data changes

**TODO:** Create a new function which will **add** a new `SourceItem` to the datasource (array) whenever the user clicks on any cell in the table view.
- For the  `name` and `overview` properties, you can hard-code any text you would like; just be sure that it is something simple that you can recognize later.
- Set an observer<sup>3</sup> on the datasource such that, whenever the array changes, data for the table view is reloaded.


<sup>3</sup> *Use either KVO or Notification.*


<!-- Refactor the table cell configuration

You will need to refactor the table cell's configuration in 2 places:

1. In the __*View Controller's*__ `cellForRowAt(_:)` function:

```Swift
override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {

    ...

    //TODO: Using MVVM, refactor cell configuration
     cell.sourceItem = sources[indexPath.row]
     return cell
 }
```

2. In the __*NewsFeedCell's*__ `awakeFromNib()` function:

```Swift
override func awakeFromNib() {

    ...

    //TODO: Using MVVM, refactor cell configuration
    var sourceItem: SourceItem? {
        didSet {
            guard let sourceItem = sourceItem else { return }
            nameLabel.text = sourceItem.name
            overviewLabel.text = sourceItem.overview
        }
    }
```

Part 3 -
(see Part 3 in After Class assignments below) -->


## After Class

1. Research these related concepts:

- Event-Driven Programming
- UI Logic
- Business Logic
- Code-Behind
- Data Binding
- Data Binding and MVVM in iOS </br>
&nbsp;&nbsp;&nbsp;&nbsp; - two-way binding </br>
&nbsp;&nbsp;&nbsp;&nbsp; - one-way binding


2. **TODO:** - Continue working on your Course Project

## Wrap Up (5 min)

- Continue working on your current tutorial
- Complete reading
- Complete challenges

## Additional Resources

1. [Model–view–viewmodel - wikipedia](https://en.wikipedia.org/wiki/Model–view–viewmodel)
2. [Presentation Model and Martin Fowler - an article](https://en.wikipedia.org/wiki/Martin_Fowler_(software_engineer))
3. [UI data binding - wikipedia](https://en.wikipedia.org/wiki/UI_data_binding)
4. [The Problems with MVVM on iOS - an article](http://www.danielhall.io/the-problems-with-mvvm-on-ios)


<sup>1</sup> *UI data binding is a software design pattern to simplify development of GUI applications. It binds UI elements to an application domain model.*

<sup>2</sup> *Model–view–viewmodel is also referred to as model–view–binder, especially in implementations not involving the .NET platform.*
