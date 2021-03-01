<!-- Run this slideshow via the following command: -->
<!-- reveal-md README.md -w -->


<!-- .slide: class="header" -->

# Combine

## [Slides](https://make-school-courses.github.io/MOB-2.4-Advanced-Architectural-Patterns-in-iOS/Slides/Combine-Pt.3/README.html ':ignore')

<!-- > -->

## Learning Objectives

By the end of this lesson, you will be able to:

**Implement**:
- Combine to update UI with UIKit
- Combine to fetch and display data 

<!-- > -->

## @Published

A type that publishes a property marked with an attribute.

```swift
@propertyWrapper struct Published<Value>
```
- Publishing a property with the `@Published` attribute creates a publisher of this type. 
- You access the publisher with the $ operator
- Class constrained

[Docs](https://developer.apple.com/documentation/combine/published)

<!-- v -->

```swift
class Weather {
    @Published var temperature: Double
    init(temperature: Double) {
        self.temperature = temperature
    }
}

let weather = Weather(temperature: 20)
cancellable = weather.$temperature
    .sink() {
        print ("Temperature now: \($0)")
}
weather.temperature = 25
```

<!-- v -->

## Integration with UIKIt

Declarative UI updates from user input.

[Instructions](assignments/Example-1.md)

<!-- > -->

## Integration with Networking

Fetching, transforming and displaying data.

[Instructions](assignments/Example-2.md)

<!-- > -->

## After Class

Combine is a new framework and it will take more reading and practice to get used to it. But you can start using what you already know, little by little. 😉

<!-- > -->

## Additional Resources

- [Using Combine](https://heckj.github.io/swiftui-notes/#coreconcepts-publisher-subscriber)
- [Combine Concepts - Playground](https://github.com/AvdLee/CombineSwiftPlayground)
- Book: Practical Combine by Donny Walls
- Book: Combine - Asynchronous programming with Swift By Shai Mishali, Marin Todorov, Florent Pillet and Scott Gardner

