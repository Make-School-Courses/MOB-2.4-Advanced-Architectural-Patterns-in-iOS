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

1. Identify and describe
1. Define
1. Design
1. Implement

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


### Four Components of MVVM

#### View:
- Responsible for displaying visual elements and controls on the screen. Subclasses of UIView, typically. </br>
(Same as in MVC)

#### Model:
- (Typically) structs or simple classes that hold app data. </br>
(Same as in MVC)


#### View Controller:
- The view controller sets up UI views. It does not interact with the model at all. It instead goes through the view model, and asks for what it needs in a format ready for display. It should have absolutely no business logic.


**View Model** --- The view model is basically a representation of the view controller. If the view controller has a label, the view model should have a property to supply it with the text in string form. It triggers all calls, and sends and receives data. When dealing with the view model, you should ensure it is as dumb as possible. This means that you should decouple it from the view controller as much as possible. We should ensure that we do not inject instances of the view controller to the view model. The view model should be completely independent of all the view controller.


It can be a class or struct but is generally a class so that references of the same instance can be passed around in your code. The ViewModel sits between the view controller and Model.

View models transform model information into values that can be displayed on a view. They’re usually classes, so they can be passed around as references.

### The ViewModel

but also the Mediator, represented as the View Model.



### Problem(s) Solved





## In Class Activity I (30 min)



## Overview/TT II (20 min)


### The View Model



### Bindings



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
