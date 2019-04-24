# Coordinators

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


A Coordinator is an object that encapsulates a lifecycle that is spread over a collection of view controllers.

So what is a coordinator? A coordinator is an object that bosses one or more view controllers around. Taking all of the driving logic out of your view controllers, and moving that stuff one layer up is gonna make your life a lot more awesome.

*Source:*
Soroush Khanlou [Coordinators Redux](http://khanlou.com/2015/10/coordinators-redux/)


<!-- - Why learn this?
- Industry examples of usage
- Best practices
- Personal anecdote -->



#### Implementation Notes

![example](assets/coordinator_types.png)







To really execute this pattern well, you need one high-level coordinator that directs the whole app (this is sometimes known as the Application Controller pattern). The app delegate holds on to the AppCoordinator. Every coordinator holds an array of its child coordinators. Especially if you have more than one, as in a tab bar app, each navigation controller gets its own coordinator, for directing its behavior and flow. Further child coordinators can be created for specific tasks like signing up or creating content. Each coordinator is spawned by its parent coordinator. As always, use this pattern early in the development process, so they’re useful even in single-step tasks, such as authentication.


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

## After Class

- Data Source Design Pattern

deep linking in ios


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
