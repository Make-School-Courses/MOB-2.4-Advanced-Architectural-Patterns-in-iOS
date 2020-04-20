<!-- Run this slideshow via the following command: -->
<!-- reveal-md README.md -w -->


<!-- .slide: class="header" -->

# Coordinators

## [Slides](https://make-school-courses.github.io/MOB-2.4-Advanced-Architectural-Patterns-in-iOS/Slides/08-Coordinators/README.html ':ignore')

<!-- > -->

## Learning Objectives

By the end of this lesson, you should be able to...

1. Describe:
- the **Coordinator** design pattern
- the software construction problem(s) it is intended to solve
- potential use cases for it (when to use it; when not to use it)
- how to implement Coordinator in iOS
3. Assess:
- the suitability of a given design pattern to solve a given problem
- the trade offs (pros/cons)
4. Design and implement basic examples of **Coordinator** explored in this class

<!-- > -->

## Initial Exercise

### As A Class

1. Review assignment from last class
- students demo their solutions

<!-- > -->

### The Coordinator Pattern

The idea behind the Coordinator pattern is the creation of a separate entity &mdash; __*a Coordinator object*__ &mdash; which is responsible for the application’s *flow.*

*So what is a coordinator?*

>
> A **coordinator** is an object that bosses one or more view controllers around.
>
> A **coordinator** is an object that encapsulates a lifecycle that is spread over a collection of view controllers.
>


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *Source:* [Coordinators Redux](http://khanlou.com/2015/10/coordinators-redux/) &mdash; Soroush Khanlou


<!-- > -->

Similar to how UIViewControllers manage UIViews, Coordinators can manage UIViewControllers taking all of the driving logic (navigation) out of view controllers and moving it up one level &mdash; to a __*Coordinator layer.*__


![example](assets/coordinator_diagram.png)

*Source:* </br>
https://medium.com/@saad.eloulladi/ios-coordinator-pattern-in-swift-39a15aa3b01b

<!-- > -->

### Problems Addressed

1. **The Pushing Problem**

One of the standard ways to perform navigation on iOS is to use a `UINavigationController` onto which each view controller can either pop or push other view controllers.

```Swift
if let vc = storyboard?.instantiateViewController(withIdentifier: "SomeVC") {
    navigationController?.pushViewController(vc, animated: true)
}
```

<!-- > -->

When the view controllers themselves must decide the next view controller to push onto `self.navigationController`, the View controllers are too tightly coupled.

As an app grows, this approach becomes difficult to deal with: The codebase will be hard to change and maintain, and view controllers are almost impossible to reuse.

<!-- > -->

What if...
- you need to be able to navigate to the same view controller from multiple places?
- you want to implement something like deep linking from outside your app?

<!--
```Swift
class ImageListViewController: UITableViewController {
    override func tableView(_ tableView: UITableView,
                            didSelectRowAt indexPath: IndexPath) {
        let image = images[indexPath.row]
        let detailVC = ImageDetailViewController(image: image)
        navigationController?.pushViewController(detailVC, animated: true)
    }
}
```

```Swift
class MyViewController : UIViewController {

    // ...
    @IBAction func didTap(_ button: Any) {

        let newViewController = NextViewController()
        self.navigationController?.pushViewController(viewController, animated: true)
    }
}
``` -->

<!-- > -->

2. **Massive View Controller Problem** &mdash; (see previous lesson for description and example)

3. **Reusability** &mdash; with standard MVC, View Controllers are nearly impossible to reuse, especially if overloaded with non-VC tasks.

4. **Tight Coupling** &mdash; an inflexible design in which every controller needs to know details about other controllers inhibits an app's growth.

<!-- > -->

5. **Deep Linking Issues** &mdash; *(see Coordinators and Deep Linking section)*

6. **Testing** &mdash; if you want to generate different views or a different flow in response to user choices (A/B testing) or to handle layout variations, standard MVC implementations of VCs make it extremely difficult to test those scenarios.  

<!-- > -->

### Implementation Notes

A solid, basic implementation of coordinators includes 3 main steps:
1. Design two protocols:
- __*Coordinator Protocol*__ - To be used by all our coordinators.
- __*View Controller Creation Protocol*__ - To facilitate view controller creation.
2. Create a __*main coordinator*__ that will control app flow. Start it when your app launches.
3. Create/present view controllers.

<!-- > -->

**About the Coordinator Protocol**

All coordinators will conform to this protocol. At bare minimum, it should include:
- A property to store any **child coordinators**. Coordinator responsibility is to **handle navigation flow**: the same way that UINavigationController keeps reference of its stack, Coordinators do the same with their children. (optional)
- A property to store the **navigation controller** being used to present view controllers. (Even if you don’t show the navigation bar at the top, using a navigation controller is the easiest way to present view controllers.)
- A `start()` function to make the coordinator take control. This allows us to create a coordinator fully and activate it only when we’re ready.

<!-- > -->


#### Example:

1. Coordinator protocol created

```Swift
protocol Coordinator {
    func start()
    var navigationController: UINavigationController { get set }
    var childCoordinators : [Coordinator] { get set } //not always
}
```

<!-- > -->

2. For building the user flow, a concrete implementation of the protocol is created:

```Swift
class BaseCoordinator: Coordinator {

    var navigationController: UINavigationController
    private var someViewController: UIViewController?

    init(navigationController: UINavigationController) {
        self.navigationController = navigationController
    }

    func start() {
        someViewController = ViewController()        
        navigationController.pushViewController(someViewController, animated: true)
    }
}

```

<!-- > -->

3. All view controllers targeted for participation in the coordinated navigation approach must:
- Have a `BaseCoordinator` property for access to its properties and functions

```Swift
class ViewController: UIViewController {

    var coordinator: BaseCoordinator?
     ...
}
```

<!-- > -->

5. If staring from the AppDelegate:

```swift
let navController = UINavigationController()
coordinator = BaseCoordinator(navigationController: navController)
coordinator?.start()

window = UIWindow(frame: UIScreen.main.bounds)
window?.rootViewController = navController
window?.makeKeyAndVisible()
```

<!-- > -->

##Practicing a simple approach

Follow [these instructions]() to create a flow using coordinators.

<!-- > -->

## Benefits

They can have huge impact on cleaning the code base and on making view controllers more loosely coupled from each other.

The pattern can be adopted for only part of an app or used across the entire application.

<!-- > -->

Coordinators create a well defined way to deal with navigation in which view controllers are:
1. Isolated from each other (do not need to know about each other)
2. Reusable in different contexts
3. Lightweight, less "massive," and focused on their key responsibilities

<!-- > -->

## Pitfalls

The downside of the Coordinator pattern:

1. **Back Button Issue** &mdash; When the user navigates back, developers must ensure that the right coordinator is released. Solutions for this might come with potential loss of built-in framework features.

2. **Overkill** &mdash; The pattern could well take too much work for very simple apps. Many extra classes will need to be created upfront.

<!-- > -->

## When to Use

Coordinators are especially useful for complex apps with a large number of destinations screens that can be reached (presented) from multiple places.


<!-- > -->

## AppCoordinator

Creating an app-wide `AppCoordinator` is the most common implementation of Coordinators for navigation flow.

This requires one high-level coordinator instantiated in the `AppDelegate` that directs navigation for the whole app (also known as the *Application Controller pattern*

<!-- > -->

The `AppCoordinator` holds an array of child coordinators, who in turn might hold an array of their own child coordinators.

This is especially useful in a TabBar app: each TabBar scene's navigation controller could get its own coordinator for directing its own behavior and flow. And each coordinator can be spawned by its parent coordinator.

<!-- > -->

![example](assets/coordinator_types2.png)

*Source:* </br>
https://www.scoop.it/topic/swift-by-jerometonnelier/p/4097595680/2018/05/11/the-c-in-mvvm-c-mihael-y-cholakov

<!-- > -->

### Coordinator and Deep Linking

A **deep link** is any link that directs a user past the home page of a website or app to content inside of it:
- for example, linking directly to a product instead of the home page.

<!-- > -->

**iOS and Deep Linking**
For many kinds of apps we not only want to make it easy to navigate within our own app, but also to enable other apps and websites to deep link into ours.

A common way to do this on iOS is to define a URL scheme that other apps can then use to link directly into a specific screen or feature of an app.

<!-- > -->

__*The Obstacle*__

To support deep linking in an iOS app, you might need to open specific views in the app, regardless of the navigation history or navigation design.

With standard MVC and its potential to tightly-couple View Controllers, it is very difficult to implement deep linking.

<!-- > -->

__*The Solution*__

Using Coordinators and navigator objects, implementing URL and deep linking support becomes a lot easier because it allows for dedicated navigation points in which URL handling logic can be injected.

*from:*
https://medium.com/@abhimuralidharan/universal-links-in-ios-79c4ee038272

<!-- this needs some example TODO: research this more -->

<!-- > -->

### Coordinator &mdash; with Other Patterns

Coordinator is an easy pattern to implement with other complementary patterns.

For examples:
1. __*Coordinator with MVVM*__
- MVVM results in thinner VCs, more easily testable code, and data formatting logic that is decoupled from VCs.
- Adding navigation flow coordinators further decouples VCs

<!-- > -->

2. __*Coordinator with Factory*__
- Combines more flexible navigation with the ability to create objects (even View Controllers) on demand and to dynamically customized specifications.

<!-- > -->

## In Class Activity

Download [this starter code](https://github.com/alfianlosari/MovieCoordinator-Starter-Project)

It is the starting point of [this tutorial](https://medium.com/swift2go/refactoring-ios-app-with-coordinator-pattern-for-navigation-alfian-losari-50081bfa7a4a)

Your task is to refactor the code to use the coordinator pattern.

Modify the Coordinator protocol to be like this:

```swift
protocol Coordinator {
    func start()
    var navigationController: UINavigationController { get set }
}
```

<!-- > -->

### Stretch Challenges

This exercise follows on today's Activity 1...

**Resources Required** Your completed app from Activity 1

**TODO:** In the tutorial below, complete these sections:

- "How and when to use child coordinators"
- "Navigating backwards"
- "Passing data between view controllers"

[Advanced coordinators in iOS - a tutorial](https://www.hackingwithswift.com/articles/175/advanced-coordinator-pattern-tutorial-ios)

<!-- > -->

## After Class

1. Research:

- Application Coordinator Pattern
- Router (with Coordinators)
- Data Source Design Pattern
- Deep Linking (specific to iOS)
- `Universal Link`
- State Machine
- MVP

<!-- > -->

## Additional Resources

1. [Slides](https://docs.google.com/presentation/d/1Ny2GlorCMgeJdkNo7AZg3m_SH4FwBLyFnrbh9Twqk4o/edit#slide=id.g50e0c2788f_27_8)
2. [The Coordinator - an aricle ](http://khanlou.com/2015/01/the-coordinator/), by Soroush Khanlou, <sup>1</sup> who popularized the pattern for iOS development.
3. [Coordinators - video presentation](https://vimeo.com/144116310)
4. [Coordinators - a slideshare from LinkedIn](https://www.slideshare.net/secret/3jJlEE1weo0RRl)
5. [8 Patterns to Help You Destroy Massive View Controller - an article](http://khanlou.com/2014/09/8-patterns-to-help-you-destroy-massive-view-controller/)

<!-- > -->

6. [NextPrevious What Are Cocoa Bindings? - from Apple ](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CocoaBindings/Concepts/WhatAreBindings.html#//apple_ref/doc/uid/20002372-CJBEJBHH)
7. [Application Controller - Martin Fowler](https://martinfowler.com/eaaCatalog/applicationController.html) <sup>2</sup>
8. [Presentation Model - Martin Fowler](https://martinfowler.com/eaaDev/PresentationModel.html)
9. [Universal Links - Apple Devloper](https://developer.apple.com/ios/universal-links/)
10. [Universal links in iOS - an article](https://medium.com/@abhimuralidharan/universal-links-in-ios-79c4ee038272)



<!-- INSTRUCTOR NOTES:  SOLUTION TO ACTIVITY 1

      PART 1: IN App Delegate:

        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {

            // create the main navigation controller to be used for our app
            let navController = UINavigationController()

            // send that into our coordinator so that it can display view controllers
    //TODO: pass the navController var into the coordinator property
            coordinator = MainCoordinator(navigationController: navController)

            // tell the coordinator to take over control
            coordinator?.start()

            // create a basic UIWindow and activate it
            window = UIWindow(frame: UIScreen.main.bounds)
            window?.rootViewController = navController
            window?.makeKeyAndVisible()

            return true
        }


        PART 2: in MainCoordinator:

        //TODO: Create functions to instantiate other VCs
        func buySubscription() {
            let vc = BuyViewController.instantiate()
            vc.coordinator = self
            navigationController.pushViewController(vc, animated: true)
        }

        func createAccount() {
            let vc = CreateAccountViewController.instantiate()
            vc.coordinator = self
            navigationController.pushViewController(vc, animated: true)
        }

        -->
