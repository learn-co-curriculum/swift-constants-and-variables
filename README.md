# Swift — Constants and Variables

## Objectives

1. Distinguish between uses of `let` and `var`.
2. Create instances of the basic value types and strings.
3. Become familiar with Swift operators and the new identity operators `===` and `!==`.
4. Use string literals to create string instances.
5. Concatenate strings with the addition operator `+`.
6. Interpolate strings with the literal syntax, `\()`.
7. Print values to the debug console using the `print()` function.

## `let` & `var`

Swift employs the keywords `let` and `var` for naming variables. The `let` keyword declares a *constant*, meaning that it cannot be re-assigned after it's been created (though its variable properties *can* be altered later). The `var` keyword declares a new *variable*, meaning that the value it holds *can* be changed at a later time.

**Terminology note:** Things get a little weird here. Names for values are universally called "variables". Even though that term in English implies something that can be changed ("vary-able"), in Swift, describing something as a "constant variable" makes a certain amount of sense. Both `let x = 5` and `var x = 5` make a new variable called `x` which starts with the value `5`. The only difference between the two is that it is illegal to reassign the `let`-declared `x` later. A way around this linguistic conundrum would be to describe things declared with `let` as "constants", and the others as "variables", but that's just not the way developers speak. Just keep in mind that if we describe something as a "variable", we don't necessarily mean it was declared with `var`.

The first section of [The Basics chapter](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/TheBasics.html) in Apple's Swift programming guide discusses these keywords in more detail.

### Implicit Typing

When creating variables, the compiler will infer the type of the variable you are creating based upon the initial assignment. The compiler will enforce that future reassignments of the variable are of the same type. For instance, a variable declared to initially hold a string (say, `var name = "Lou"`) cannot later be assigned a value of any type other than a string (for instance, typing `name = 5` later is a compiler error).

### Value Types

Objective-C programmers are all too familiar with distinguishing primitives from objects. Swift has no such distinction: integers, floats, and booleans are all effectively objects. The types `Int` (integer), `Double` (floating-point), and `Bool` (boolean) are typed implicitly based upon initial assignment:

```swift
let two = 2       // Int
let negSeven = -7 // Int
let twoPointZero = 2.0 // Double
let pi = 3.14159       // Double
let isTrue = True    // Bool
let isFalse = False  // Bool
```
**Advanced:** *Unsigned integers are available as* `UInt` *but require explicit typing to declare, which we'll cover later.*

## Operators

Since Swift is a C-family language, the typical C operators are available with their usual behavior and precedence.

A couple of notable distinctions in Swift are that:

1. The assignment operator (`=`) no longer returns a value, which makes it more difficult to accidentally type an assignment in an `if`-statement when you meant to use `==`.

2. Swift includes the normal comparison operators `==` (a.k.a. "double equals") and `!=` ("not equal to") to determine whether two instances are conceptually equal. Yes, Objective-C developers, you can now type `"a" == "a"` and have it do the right thing! No need to use `isEqualToString:` any more.

3. In the same vein as `==` being useful for objects, many other operators now do handy things. For instance, `+` can be used to concatenate two strings. We'll see that shortly.

3. There are two new *identity* operators in Swift, `===` (a.k.a. "triple equals") and `!==` ("not identical to") which measure whether two variables reference the *exact same object.* You probably won't need to use these, but they're around just in case.

Reference the [Basic Operators chapter](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/BasicOperators.html#//apple_ref/doc/uid/TP40014097-CH6-ID60) of Apple's documentation for detailed information.

## Strings

### String Literals

Swift uses a pair of double-quotes to enclose a literal string (a value of type `String`):

```swift
var greeting = "Welcome to"
let flatiron = "the Flatiron School"
```
Because `greeting` was created as a variable, we can reassign its value later:

```swift
greeting = "Hello, welcome to"
```
However, since the `flatiron` instance was created as a constant, the compiler will warn us if we try to change it later:

```swift
flatiron = "the Main Campus"   // error
```
![](https://curriculum-content.s3.amazonaws.com/swift/swift-constants-and-variables/error_cannot_assign_to_let_constant.png)

### String Concatenation with `+`

Swift allows classes to declare how operators should behave on them. That means, for instance, the addition operator (`+`) can be used to join two strings together. For programmers with experience using Ruby or Python, this will feel very familiar:

```swift
let message = greeting + flatiron
```

The `message` instance will now hold the awkward string value `"Hello, welcome tothe Flatiron School"`. We can add a space and an ending punctuation by using string literals with more addition operators:

```swift
let message = greeting + " " + flatiron + "."
```
The `message` instance will now hold the string value `"Hello, welcome to the Flatiron School."`.

### String Interpolation with `"\()"`

Swift allows string interpolation to be done inside a literal. In stark contrast to the messy Objective-C syntax of matching format specifiers up with variable names, Swift allows a value to be used directly into a string literal with the interpolation syntax `\(value)`.

This means we can create our `message` without concatenation by using the `greeting` and `flatiron` variables directly into a new string literal:

```swift
let message = "\(greeting) \(flatiron)."
```
The `message` instance will hold the same string value as above, `"Hello, welcome to the Flatiron School."`.

Reference the [Strings and Characters chapter](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/StringsAndCharacters.html#//apple_ref/doc/uid/TP40014097-CH7-ID285) of Apple's documentation for more detailed information.

## Printing An Instance to the Debug Console

Swift's `print()` function will send a string representation of any value to the debug console. It can be sent an instance directly, or be sent a string literal which may or may not include interpolation arguments:

```swift
print(message)
print("Hello, world.")
print("\(greeting) the world.")
```
These will print:

```
Hello, welcome to the Flatiron School.
Hello, world.
Hello, welcome to the world.
```

It can also be sent the result of an operation, such as using the addition operator (`+`) to print the concatenation of a string instance with a string literal:

```swift
print(greeting + " the world.")
```
This will print: `Hello, welcome to the world.`

**Note:** *You may see* `println()` *("print line") used in examples online, which is no longer available in Swift 2.0. Originally, the* `print()` *function did not append a newline character so* `println()` *was provided as an alternative which did. Swift 2's* `print()` *function, however, automatically appends a newline so* `println()` *was considered redundant and removed.*

**Objective-C:** `NSLog()` *is still available in Swift. However, it's a little more typing than* `print()` *since you still need to give a format specifier in the first argument. For example:* `NSLog("%@", greeting + " the world.")` *.*

<a href='https://learn.co/lessons/swift-constants-and-variables' data-visibility='hidden'>View this lesson on Learn.co</a>
