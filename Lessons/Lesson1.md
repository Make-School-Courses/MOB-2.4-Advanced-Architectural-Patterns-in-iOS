# Creational Patterns Pt.1

## Minute-by-Minute

| **Elapsed** | **Time**  | **Activity**              |
| ----------- | --------- | ------------------------- |
| 0:00        | 0:05      | Intro                |
| 0:05        | 0:05      | Objectives                |
| 0:10       | 0:20      | Overview #1                 |
| 0:30        | 0:20      | In Class Activity I       |
|0:50        | 0:10      | BREAK                     |
| 1:00       | 0:10      | Overview #2                 |
| 1:10        | 0:30      | In Class Activity II      |
|1:40       | 0:05    | Wrap Up                     |
| TOTAL       | 1:45      |                           |

## Why you should know this or industry application (5 min)

__*Design patterns*__ represent time-tested solutions to general software development challenges realized by numerous experienced software engineers through decades of trial and error.

Design patterns...

- Create a common language
- Provide tested solutions to common development problems
- Fast-track developer on-boarding
- Allow you to spot similarities between code

It’s best for a new developer to have an understanding of what they are before running into them...


## Learning Objectives (5 min)

By the end of this lesson, you should be able to...

1. Explain why design patterns are important in software development
2. Describe:
- the **Singleton** and **Object Template** patterns
- the software construction problem each is intended to solve
- potential use cases for each (when to use them)
3. Assess:
- the suitability of a given design pattern to solve a given problem
- the trade offs (pros/cons) inherent in each


## Overview/TT #1 (20 min)

### 3 Types of Design Patterns

There are three main types of design patterns:
- **Structural**
- **Behavioral**
- **Creational**


### Creational patterns
Creational patterns are concerned with how objects are created in an application.

They aim to increase an application’s flexibility in instantiating objects in a manner suitable for a given situation.

Creational design patterns include:
- __*Object Template*__
- __*Factory Method*__
- Abstract Factory
- __*Builder*__
- __*Singleton*__
- Prototype

*From: wikipedia*

*Lessons 1 and 2 cover the Creational design Patterns highlighted above*

<!-- TODO: Insert a diagram? -->


### The Singleton Pattern
The singleton pattern restricts a class to only one, unique instance.

To ensure there is only one instance of your singleton, you must make it impossible for anyone else to make an instance.

Swift allows you to do this by marking the initializers as `private`. You can then add a `static` property for the shared instance, which is initialized inside the class.

**Apple* uses this approach **extensively in iOS** development.

Examples include:
- UserDefaults.standard
- UIApplication.shared
- FileManager.default

...all return a Singleton object.

__*Simple Example:*__

This simplified example illustrates the basic structure of a class definition designed to create a single instance of an object:

```Swift
// Singleton design pattern
class Singleton {

   static let sharedInstance = Singleton()

   private init() { // use a private init to ensure only 1 instance is created
      // do something
   }
}
// Instantiate the Singleton object
let singleton = Singleton.sharedInstance
   ```

#### Pros & Cons

**PROS**
- __*Instance Control*__ — prevents other objects from instantiating their own copies of the Singleton object, ensuring that all objects access the single instance.
- __*Flexibility*__ - The class controls the instantiation process; hence, the class has the flexibility to change the instantiation process.
- __*Ease of Implementation*__ — Can create and use it anywhere and for the lifetime of the app. And you are absolutely sure of the number of instances when you use a Singleton.

**CONS**
Singletons are not the answer to every problem. And some developers are critical of Singletons for various reasons, including:

- __*Singletons hinder unit testing:*__ A Singleton might cause issues for writing testable code if the object and the methods associated with it are so tightly coupled that it becomes impossible to test without writing a fully-functional class dedicated to the Singleton.
- __*Singletons create hidden dependencies*__ and carry state around for the lifetime of the application.
- They inherently __*cause code to be tightly coupled.__*

## In Class Activity I (20 min)

#### Individually

Let's create a simple example of a Singleton class that designed to create an array to be used as an applications a single, globally-accessible data source.

**Step 1:** Create the Singleton

In a playground, create a Singleton class called `DataSource` with these members:

1. An array that holds a few items:

```Swift
var simpleArray = [“eenie”, “meenie”, “minie”, “moe”]
```

2. A `private init()` function that only contains these two statements:</br>

    `print(“self is:“, self)` </br>
    
    `print("simpleArray is," simpleArray)`  

**Step 2:**  Instantiate the Singleton object

`let data = DataSource.sharedInstance`

Now, __*run*__ the playground...

**Step 3:**  Below your code so far, add and invoke the following `looper()` function

```Swift
func looper(){

  for n in 1...5 {
      _ = DataSource.sharedInstance
      print(“n is:“, n)
  }
}
looper()
```

**Q:** What is surprising or noteworthy about the result of running `looper()`?


   <!--
#### Part 2 - As A Class

Discuss...

**Q:** How do you think this pattern works to create a single, global instance?

**Q:** What advantages and disadvantages come to mind?
-->

<!-- FIRST ACTIVITY 1 - retained as fallback:
- View [Swift 2.0 Programming : Design Patterns : The Singleton Pattern](https://www.youtube.com/watch?v=3g7zZJWEbX0) video by the funza Academy (7 mins)

### 2. In Pairs - Discuss

**Q:** What iOS design patterns have you used or are familiar with so far?

**Q:** When have you encountered the Singleton pattern in code you've written or come across so far? (See the list of Apple examples above for ideas.)
- Why do you think a Singleton was chosen for either (a) the Apple examples listed, or (b) code you've used or seen?

### 3. As A Class

- 1 or 2 students to share results of discussion with class...
-->


## Overview/TT #2 (20 min)

__*The Object Template Pattern*__
- Helps prevent the tight coupling of components
- Also provides a foundation for more advanced patterns

In the __*object template pattern,*__ you define a template from which objects are created from a class or struct.

When some component in your app needs a new object created, it calls the runtime by specifying the name of the template to use, along with any initialization values required to configure the object.

The __*object template pattern,*__ is composed of **three operations:**

1. A calling component asks the runtime to **create** an object and provides the **template name** and required **initialization values.**

2. The **runtime allocates memory** to store the object, **uses the template** to create it, and **prepares** (initializes) **the object for use.**

3. The **runtime returns the created object** to the calling component

Because this __*process can be easily repeated*__ as often as desired (within memory limits), a single template can be used to create many, many objects.

<!-- Needs code sample -->

<!-- Needs diagram -->


## In Class Activity II (30 min)

### In Pairs

The following code sets up an array of tuples each representing a specific product:

```Swift
var products = [
   (“Kayak”, “A boat for one person”, 275.0, 10),
   (“Lifejacket”, “Protective and fashionable”, 48.95, 14),
   (“Soccer Ball”, “FIFA-approved size and weight”, 19.5, 32)]

func calculateTax(product:(String, String, Double, Int)) -> Double {
   return product.2 * 0.2;
}

func calculateStockValue(tuples:[(String, String, Double, Int)]) -> Double {
   return tuples.reduce(0, {
       (total, product) -> Double in
       return total + (product.2 * Double(product.3))
   });
}

print(“Sales tax for Kayak: $\(calculateTax(product: products[0]))“)
print(“Total value of stock: $\(calculateStockValue(tuples: products))“)
```

**Q:** If we remove an element from each of the tuples, how will that effect the rest of the code?

**TODOs:**
1. Have one person validate the code by running it in a playground just as it is.
2. For each of the tuples in the array, remove the second element - the element which describes the product - so that your array now looks like this:
```Swift
var products = [
   (“Kayak”, 275.0, 10),
   (“Lifejacket”, 48.95, 14),
   (“Soccer Ball”, 19.5, 32)]
   ```
3. Analyze and discuss with your partner the various places in the code which must now be rewritten to accommodate this change to the product tuples.
- Also discuss what this reveals regarding the impact of tuples on extending and maintaining code.
4. Now, validate your analysis by applying your proposed fixes to the code in the playground (each person should do this separately in their own playground)


## After Class

1. **Research** — and __*be ready to discuss*__ in our next class the following:

a) The two design patterns we’ve covered today, paying rapt attention to:
- definition/design
- the specific problem(s) that the pattern is intended to solve
- pros/cons of using it
- use case examples (with code to illustrate them, if possible)

b) These concepts:
- Inversion of Control (IoC)
- Tight Coupling...and the benefits of decoupling
- The Singleton Plus design pattern
- Dependency Injection
- the `private` access control level

2. **Rework the code** In the Activity above to **optimize maintainability:**

The code snippet you analyzed above presents a simple example of __*Tight Coupling.*__ The functions used to process the items in the products array are *tightly coupled* to the variables in each product tuple.

**TODO:** Applying what you’ve learned today, refactor the code in the snippet above to allow changing the properties on the product in a way that minimizes the need to change the calling code.


## Wrap Up (5 min)

1) Brief summary of today's design Patterns
2) Any questions re: the After Class assignments above


## Additional Resources

1. [Software design pattern - wikipedia](https://en.wikipedia.org/wiki/Software_design_pattern)
2. [Top 5 Design Patterns in Swift for iOS App Development - an article](https://rubygarage.org/blog/swift-design-patterns)
3. [What Is a Singleton and How To Create One In Swift - an article](https://cocoacasts.com/what-is-a-singleton-and-how-to-create-one-in-swift)
4. [Swift 2.0 Programming : Design Patterns : The Singleton Pattern - video by funza Academy](https://www.youtube.com/watch?v=3g7zZJWEbX0)(7 mins)
