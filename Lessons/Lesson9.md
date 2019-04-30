# Functional Programming (Part 1 of 2)

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
- the **xxxx** design pattern
- the software construction problem(s) it is intended to solve
- potential use cases for it (when to use it; when not to use it)
3. Assess:
- the suitability of a given design pattern to solve a given problem
- the trade offs (pros/cons) inherent in choosing high-level (MVC, MVVM, etc.) design patterns
4. Implement basic examples of XXX explored in this class


<!-- 1. Identify and describe
1. Define
1. Design
1. Implement -->

## Initial Exercise (15 min)

xxxx


## Overview/TT I (20 min)

###  Functional Programming

> “Functional programming is a programming paradigm &mdash; a style of building the structure and elements of computer programs &mdash; that treats computation as the evaluation of mathematical
> functions and avoids changing-state and mutable data.”
> – Wikipedia

### Why Learn This?

**Enemy of the State** <sup>1</sup> </br>
iOS and Mac apps rely heavily on __*state*__ to change their presentation and respond to input &mdash; it's hard to imagine writing an app without the use of __*properties*__ and __*variables.*__

However, __*state*__ is a __*huge source of needless complexity,*__ and __*responsible for most of the easily avoidable bugs*__ that users encounter.


### Imperative vs. Declarative Code Style

**State** &mdash; Refers to a program's stored values at any given time

**Mutation** &mdash; The act of updating some state in-place

#### Imperative

 > Imperative programming is a programming paradigm that uses statements that change a program's state.
 > ...an imperative program consists of commands for the computer to perform. Imperative programming focuses on describing how a program operates.
 > ...(it) implements algorithms in explicit steps.
 > – Wikipedia


<!-- TODO: show simple example in swift  -->

#### Declarative

Declarative (programming style)...focuses on what the program should accomplish without specifying how the program should achieve the result.

Many languages that apply this style attempt to minimize or eliminate side effects by describing what the program must accomplish in terms of the problem domain, rather than describe how to accomplish it as a sequence of the programming language primitives[2] (the how being left up to the language's implementation).
 > – Wikipedia

<!-- TODO: expand on  simple example in swift above with Declarative version -->


##### Example 1

```Swift
class MyItem {

    var name: String
    var description: String

    init(name: String, description: String) {
        self.name = name
        self.description = description
    }
}

var myArr = [
    MyItem(name: "Abc", description: "Lorem ipsum 1."),
    MyItem(name: "Def", description: "Lorem ipsum 2."),
    MyItem(name: "Xyz", description: "Lorem ipsum 3.")
]
```

```Swift
// Imperative approach
for item in myArr {
    if item.name == "Def" {
        print("Yes")
    }
}
```


```Swift
// Declarative approach
if myArr.contains(where: { $0.name == "Def" }) {
    print("yes")
}
```

##### Example 2


```Swift
//Imperative Approach
var numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

for i in 0..<numbers.count {
    let timesTen = numbers[i] * 10
    numbers[i] = timesTen
}

print(numbers) //[10, 20, 30, 40, 50, 60, 70, 80, 90, 100]
```


```Swift
//Functional Approach
let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

extension Array where Element == Int {

    func timesTen() -> [Int] {
        var output = [Int]()

        for num in self {
            output.append(num * 10)
        }
        return output
    }

}

let result = numbers.timesTen()

print(numbers) //[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
print(result) //[10, 20, 30, 40, 50, 60, 70, 80, 90, 100]
```

*from:* </br>
https://medium.com/swift2go/functional-programming-in-swift-an-introduction-253c1f420ca9


## In Class Activity I (30 min)



## Overview/TT II (optional) (20 min)

## In Class Activity II (optional) (30 min)

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


## Wrap Up (5 min)

- Continue working on your current tutorial
- Complete reading
- Complete challenges

## Additional Resources

1. [Slides]()
2. [Functional programming - wikipedia](https://en.wikipedia.org/wiki/Functional_programming)
3. [Enemy of the State](https://speakerdeck.com/jspahrsummers/enemy-of-the-state?slide=5) <sup>1</sup>
[]()


https://en.wikipedia.org/wiki/Imperative_programming

https://en.wikipedia.org/wiki/Declarative_programming

https://realm.io/news/andy-matuschak-controlling-complexity/


https://en.wikipedia.org/wiki/State_(computer_science)


https://en.wikipedia.org/wiki/Comparison_of_programming_paradigms
