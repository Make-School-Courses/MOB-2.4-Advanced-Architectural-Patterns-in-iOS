# Coordinators

<!-- INSTRUCTOR NOTES:
1) For the QuizLet Game in the Initial Exercise:
- the URL is xxxx
2) For Activity 1:
- solutions are hidden below Additional Resources
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
- the **Coordinator** design pattern
- the software construction problem(s) it is intended to solve
- potential use cases for it (when to use it; when not to use it)
- how to implement Coordinator in iOS
3. Assess:
- the suitability of a given design pattern to solve a given problem
- the trade offs (pros/cons) inherent in choosing high-level (MVC, MVVM, etc.) design patterns
4. Design and implement basic examples of **Coordinator** explored in this class


## Initial Exercise (15 min)

### As A Class

1. Review After Assignment from Lesson 7
- selected students demo their solutions

## Overview/TT I (20 min)

### The Coordinator Pattern

Similar to how UIViewControllers manage UIViews, Coordinators manage UIViewControllers, taking all of the driving logic (navigation) out of view controllers and moving that logic up one layer &mdash; to a __*Coordinator layer.*__

*So what is a coordinator?*

> A Coordinator is an object that encapsulates a lifecycle that is spread over a collection of view controllers.
>
> A coordinator is an object that bosses one or more view controllers around.

*Source:* [Coordinators Redux](http://khanlou.com/2015/10/coordinators-redux/) Soroush Khanlou<sup>1</sup>




<!-- TODO: explain Application Coordinator pattern
- add footnote to Khanlou popularizing Coordinator for iOS
- insert diagram of coordinator -->



#### Problems Addressed / Benefits




<!-- Massive View Controller Problem

VC Reusability

push


-->

3. **The Pushing Problem**

One of the standard ways to perform navigation on iOS is to use a `UINavigationController` onto which each view controller can either pop or push other view controllers.

Most iOS developers have implemented this type of navigation a hundred or more times:

```Swift
if let vc = storyboard?.instantiateViewController(withIdentifier: "SomeVC") {
    navigationController?.pushViewController(vc, animated: true)
}
```


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




#### Implementation Notes










<!--
To really execute this pattern well, you need one high-level coordinator that directs the whole app (this is sometimes known as the Application Controller pattern). The app delegate holds on to the AppCoordinator. Every coordinator holds an array of its child coordinators. Especially if you have more than one, as in a tab bar app, each navigation controller gets its own coordinator, for directing its behavior and flow. Further child coordinators can be created for specific tasks like signing up or creating content. Each coordinator is spawned by its parent coordinator. As always, use this pattern early in the development process, so they’re useful even in single-step tasks, such as authentication. -->


A solid, basic implementation of coordinators for includes 3 main steps:
1. Design two protocols:
- Coordinator Protocol - To be used by all our coordinators.
- View Controller Creation Protocol - To make view controllers easier to create.
2. Create a __*main coordinator*__ that will control app flow. Start it when our app launches.
3. Present other view controllers.

**The Coordinator Protocol**
All coordinators will conform to this protocol. At bare minimum, it should include:
- A property to store any child coordinators.
- A property to store the navigation controller being used to present view controllers. (Even if you don’t show the navigation bar at the top, using a navigation controller is the easiest way to present view controllers.)
- A `start()` function to make the coordinator take control. This allows us to create a coordinator fully and activate it only when we’re ready.


<!-- TODO: Need to get an example of this  -->

![example](assets/coordinator_types.png)



## In Class Activity I (30 min)

### Individually

**Required Resources:**
1. Download the starter app: [iOS-CoordinatorsActivity1_B](https://github.com/Make-School-Labs/iOS-CoordinatorsActivity1_B)

**Background:**
The `iOS-CoordinatorsActivity1_B` app seeks to implement the Coordinator pattern by:
- Creating two protocols:

&nbsp;&nbsp;&nbsp;&nbsp; - Navigation </br>
&nbsp;&nbsp;&nbsp;&nbsp; - Dynamically instantiating View Controller objects from the Main Storyboard bundle </br>


__*Navigation Protocol*__
```Swift
protocol Coordinator {
    var childCoordinators: [Coordinator] { get set }
    var navigationController: UINavigationController { get set }

    func start()
}
```

__*VC Creation Protocol*__

```Swift
protocol Storyboarded {
    static func instantiate() -> Self
}
```

__*Note that:*__
- the main VC (`ViewController`) is __*not*__ configured as the "Initial View Controller" in the storyboad
- in order to be created dynamically, all VCs are given a `StoryBoard ID`

**- TODO -**
The code in the app is nearly complete. Your job is to:
- analyze the app's structure wrt how it is creating view controllers
- complete any missing code so that the `BuyViewController` and `CreateAccountViewController` are presented using the Coordinator pattern instead of typical iOS navigation process (*see* The Pushing Problem *above*)


> **TIP:** Look for the //TODO: annotations we left in the app for you...


*adapted from:* </br>
https://www.hackingwithswift.com/articles/175/advanced-coordinator-pattern-tutorial-ios


<!-- INSTRUCTOR NOTES: solutions for Activity 1 are hidden below Additional Resources -->


## Overview/TT II (optional) (20 min)

### Coordinator with Other Patterns

#### with MVVM

#### with xxx


### When to Use

Use Coordinators when...

(especially when building apps that have a large amount of screens and destinations that can be reached from multiple places) is to introduce dedicated navigator types.

## In Class Activity II (optional) (30 min)

## After Class

1. Research:
- Data Source Design Pattern

deep linking in ios

2. Follow on exercise to today's Activity 1:

[Advanced coordinators in iOS](https://www.hackingwithswift.com/articles/175/advanced-coordinator-pattern-tutorial-ios)

At minimum, complete these:

- How and when to use child coordinators
- Navigating backwards

Stretch Challenge:
- finish all

3. Continue working on your Course Project...




## Wrap Up (5 min)

- Continue working on your current tutorial
- Complete reading
- Complete challenges

## Additional Resources

1. [Slides]()

[]()
[]()
[Coordinators - video presentation](https://vimeo.com/144116310)
[Coordinators - a slideshare from LinkedIn](https://www.slideshare.net/secret/3jJlEE1weo0RRl)


[8 Patterns to Help You Destroy Massive View Controller - an article](http://khanlou.com/2014/09/8-patterns-to-help-you-destroy-massive-view-controller/)
[NextPrevious What Are Cocoa Bindings? - from Apple ](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CocoaBindings/Concepts/WhatAreBindings.html#//apple_ref/doc/uid/20002372-CJBEJBHH)

[Presentation Model - Martin Fowler](https://martinfowler.com/eaaDev/PresentationModel.html)
[Application Controller - Martin Fowler](https://martinfowler.com/eaaCatalog/applicationController.html)



<sup>1</sup> <!-- TODO:
- add footnote to Khanlou popularizing Coordinator for iOS
-->


<!-- INSTRUCTOR NOTES:  -- SOLUTION TO ACTIVITY 1 --

  PART 1: IN App Delegate:

    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {

        // create the main navigation controller to be used for our app
        let navController = UINavigationController()

        // send that into our coordinator so that it can display view controllers
        //TODO: create a coordinator var
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
