<!-- Run this slideshow via the following command: -->
<!-- reveal-md README.md -w -->


<!-- .slide: class="header" -->

# Combine

## [Slides](https://make-school-courses.github.io/MOB-2.4-Advanced-Architectural-Patterns-in-iOS/Slides/Combine-Pt.1/README.html ':ignore')

<!-- > -->

▶️ Watch this before the lesson:

[Combine - Video introduction](https://developer.apple.com/videos/play/wwdc2019/722/)

<!-- > -->

## Learning Objectives

By the end of this lesson, you will be able to:

Describe:
  - Reactive programming
  - Marble diagrams
  - Combine as a framework and it's main components
  - Basic operators
  - Lifecycle of a stream

<!-- > -->

## Reactive Programming

Reactive Programming can be thought of as the practice of programming with **asynchronous** data streams, or __*event streams.*__

<!-- > -->

### Event Streams

An event stream is a **sequence of events** happening over time.

An **asynchronous data stream** is a stream of data where values are *emitted*, one after another, with a delay between them, and without blocking program flow to wait for results.

And because the stream is asynchronous, the data emitted can appear anywhere in time.

<!-- > -->

### Modeling Event Streams with Marble Diagrams

The common way of modeling asynchronous streams is to place the emitted values on a time axis in what is called a **Marble Diagram**

These are interactive diagrams that show how operators work with sequences over time.

<!-- > -->

Here, our diagram shows a simple description of a hypothetical event stream, with events represented by colored bubbles drawn at intermittent time intervals:

![Marble_diagram_breakdown](assets/Marble_diagram.png) </br>

<!-- > -->

In a Marble Diagram, the left-to-right arrow represents time, and the numbered circles represent elements of a sequence, which are just values plotted on the timeline.

In the last diagram, pay particular attention to these symbols:
- The **Error** symbol
- The **Event Stream Complete** symbol  

<!-- > -->

## Combine

A framework that provides a declarative Swift API for processing values over time.

These values can represent many kinds of asynchronous events.

[Docs](https://developer.apple.com/documentation/combine)

<!-- > -->

## Core Concepts

- [Publisher](https://developer.apple.com/documentation/combine/publisher) and [Subscriber](https://developer.apple.com/documentation/combine/subscriber)

- Operators

- [Subjects](https://developer.apple.com/documentation/combine/subject)

<!-- > -->

## Publisher

- Described as a protocol
- **Provides data when available and upon request**
- A publisher that has not had any subscription requests will not provide any data
- Has two associated types: one for **Output** and one for **Failure**
- Value types

<!-- > -->

## Subscriber

- Responsible for **requesting data and accepting the data** (and possible failures) provided by a publisher
- Has two associated types: one for **Input** and one for **Failure**
- Reference types (usually act and mutate state upon receipt of values)

<!-- > -->

<img src="https://heckj.github.io/swiftui-notes/images/diagrams/input_output.svg">

Publishers and subscribers are meant to be connected, and make up the core of Combine.

<aside class="notes">
When you connect a subscriber to a publisher, both types must match: Output to Input, and Failure to Failure.
</aside>

<!-- > -->

## Operator

- An object that acts both like a subscriber and a publisher
- Classes that adopt both the Subscriber protocol and Publisher protocol
- They support subscribing to a publisher, and sending results to any subscribers
- Can be chained to process, transform data

<!-- > -->

<img src="https://heckj.github.io/swiftui-notes/images/diagrams/pipeline.svg">

<!-- > -->

```swift
let _ = Just(8)
    .map { value -> String in
        // do something with the incoming value here
        return "\(value) as a string"
    }
    .sink { receivedValue in
        // sink is the subscriber and terminates the pipeline
        print("The end result was \(receivedValue)")
    }
```

## In Class Activity

Instructions [here]()


<!-- > -->

## After Class


<!-- > -->

## Additional Resources

- [Using Combine](https://heckj.github.io/swiftui-notes/#coreconcepts-publisher-subscriber)
- Book: Practical Combine by Donny Walls
