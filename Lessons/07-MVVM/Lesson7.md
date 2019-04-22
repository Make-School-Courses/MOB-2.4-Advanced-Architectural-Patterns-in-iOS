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

MVVM is very similar to MVC and compliments it exceptionally well. It can be seen as an extension of MVC's primary intent: separating the View from the Model and utilizing the Controller as a central "manager" between View and Model.

MVVM takes the principle of *Separation of Concerns* one step further &mdash; it adds a special layer between the View and the Model (called the ViewModel or View Model) which allows Controllers to delegate data presentation responsibilities to the View Model.

Here is how the four major components of MVVM relate to each other (and to MVC):

**View** &mdash; Responsible for displaying visual elements and controls on the screen. Subclasses of UIView, typically. </br>
(Same as in MVC)

**Model** &mdash; Objects that hold app data; typically structs of simple classes. (Same as in MVC)

**View Controller** &mdash; In MVVM, VCs still set up UI views, but they do not interact with the model. Instead, the VC uses the View Model as a *mediator* and asks for what it needs in a format that will be ready for presentation. In MVVM, VCs should have absolutely no business logic.

**View Model** &mdash; Transform Model data into values that can be displayed on a View. Sits between the View Controller and Model. Can be a class or struct,  but it is typically a class so that references of the same instance can be passed around in code.

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
