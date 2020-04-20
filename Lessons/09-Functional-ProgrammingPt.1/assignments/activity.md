
## In Class Activity

### Individually

1. Here is an imperative version of a function called `doubleIt` that takes an array of numbers and returns a new array after doubling every item in the initial array:

```swift
func doubleIt(inputArray: Array<Int>) {

    var results = [Int]()

    for num in inputArray {
        results.append(num * 2)
    }
    print(results)
}

doubleIt(inputArray: [1,2,3]) // [2,4,6]
```

**TODO:**

1. Code the declarative (FP) version of `doubleIt`so that it achieves the same result as the code above by using the `map` function instead of the `for loop`

<!--
```swift
func doubleIt(inputArray: Array<Int>) {

    // TODO: Use map here...
    let results = ??
    print(results)
}

doubleIt(inputArray: [1,2,3]) // [2,4,6]
```
-->

2. Given an array of Users which have properties name:String and age:Int:
   - write a `map` function that returns an array of strings consisting of the user’s names

3. Take the initial array of Users from the exercise above and, using `map`, convert it to a Dictionary

4. Given an array of dictionaries containing keys for “name” and “age”:
   - write a `map` function that returns an array of users created from it

*From:* </br>
https://www.weheartswift.com/higher-order-functions-map-filter-reduce-and-more/
