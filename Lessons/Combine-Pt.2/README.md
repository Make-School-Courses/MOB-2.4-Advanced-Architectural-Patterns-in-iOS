<!-- Run this slideshow via the following command: -->
<!-- reveal-md README.md -w -->


<!-- .slide: class="header" -->

# Combine

## [Slides](https://make-school-courses.github.io/MOB-2.4-Advanced-Architectural-Patterns-in-iOS/Slides/Combine-Pt.2/README.html ':ignore')

<!-- > -->

## Initial Activity

- Discussion on Backpreassure and `Future`.

<!-- > -->

## Learning Objectives

By the end of this lesson, you will be able to:

Describe:
    - Subjects
Implement:
    - Subscriptions with operators
    - Combine in an Xcode project to update UI

<!-- > -->

## Subjects

A special case of publisher that also adhere to the [Subject protocol](https://developer.apple.com/documentation/combine/subject). 

Lets you inject values in a stream by calling a `send` method.

<aside class = "notes">
Subjects can act as a conductor to send values from non-Combine imperative code to Combine subscribers.
</aside>

<!-- > -->

## Built-in Subjects

- [PassthroughSubject](https://heckj.github.io/swiftui-notes/#reference-passthroughsubject)
- [CurrentValueSubject](https://heckj.github.io/swiftui-notes/#reference-currentvaluesubject)

<aside class ="notes">
PassthroughSubject let's you publish new values on demand. They will pass along values and a completion event.

CurrentValueSubject lets you look at the current value of a publisher.
</aside>

<!-- > -->

## Playground Challenge

Blackjack hand dealer

<!-- > -->

## After Class



<!-- > -->

## Additional Resources

- [Using Combine](https://heckj.github.io/swiftui-notes/#coreconcepts-publisher-subscriber)
- Book: Practical Combine by Donny Walls
- Book: Combine - Asynchronous programming with Swift By Shai Mishali, Marin Todorov, Florent Pillet and Scott Gardner
