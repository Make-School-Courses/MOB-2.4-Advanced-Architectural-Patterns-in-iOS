# Behavioral Patterns Pt.2

<!-- INSTRUCTOR NOTES:
1) For the quiz in the Initial Exercise:
- the URL is xxxx
2) For Activity 1:
- xxxx
3) for Activity 2:
- xxx
-->

## Minute-by-Minute [OPTIONAL]

| **Elapsed** | **Time**  | **Activity**              |
| ----------- | --------- | ------------------------- |
| 0:00        | 0:05      | Objectives                |
| 0:05       | 0:15      | Initial Exercise             |
| 0:20       | 0:15      | Overview  I                |
| 0:35        | 0:20      | In Class Activity I       |
| 0:55        | 0:10      | BREAK                     |
| 1:05         | 0:15      | Overview  II                |
| 1:20        | 0:25      | In Class Activity II      |
|1:45       | 0:05    | Wrap Up                     |
| TOTAL       | 1:50    |                          |

## Why you should know this or industry application (optional) (5 min)

Explain why students should care to learn the material presented in this class.

## Learning Objectives (5 min)

By the end of this lesson, you should be able to...

1. Describe:
- the **Observer** and **Visitor** patterns
- the software construction problem each is intended to solve
- potential use cases for each (when to use them)
3. Assess:
- the suitability of a given design pattern to solve a given problem
- the trade offs (pros/cons) inherent in each
4. Implement basic examples of both patterns explored in this class

## Initial Exercise (15 min)

### Part 1 - Individually

...__*SURPRISE!!!*__ ...__*time for another Quiz!*__

<!-- Quiz location:

-->

### Part 2 - In Pairs

Grade each other's quizzes, sharing answers, insights, etc.

## Overview/TT I (20 min)

### The Observer Pattern &nbsp;&nbsp;&nbsp;&nbsp;:eyes:

The **Observer pattern** lets one object observe changes to the __*state*__ of another object without needing to know the implementation of the object observed.

Observer is comprised of __*two main objects:*__ <sup>1</sup>
1. **Subject** — The object under observation.
- The subject object __*allows observer objects to register*__ (and unregister) their interest in receiving updates (notifications) whenever changes are made to the subject, and it __*automatically notifies observers*__ of any state changes.<sup>2</sup>
- Subjects are __*responsible for maintaining a list of their dependents*__ (observers).
2. **Observer(s)** — The object(s) doing the observing.
- It is the responsibility of observers is __*to register (and unregister) themselves on a subject*__ (to get notified of state changes) and __*to update their state*__ (synchronize their state with subject’s state) when they are notified.

This makes subject and observers loosely coupled - subject and observers have no explicit knowledge of each other. Observers can be added and removed independently at run-time.

<sup>1</sup> *This notification-registration interaction is also known as* __*"publish-subscribe."*__

<sup>2</sup> *Another common actor in the Observer pattern is a* __*Client object.*__ *Subject objects often have methods to attach and detach observers to a client object.*






- Why learn this?
- Industry examples of usage
- Best practices
- Personal anecdote

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

### The Visitor Pattern &nbsp;&nbsp;&nbsp;:alien:


## In Class Activity II (optional) (30 min)

## Wrap Up (5 min)

- Continue working on your current tutorial
- Complete reading
- Complete challenges

## Additional Resources

1. [Slides]()
2. [Observer pattern - wikipedia](https://en.wikipedia.org/wiki/Observer_pattern)
3. [Publish–subscribe pattern  - wikipedia](https://en.wikipedia.org/wiki/Publish–subscribe_pattern)
[]()
[]()
