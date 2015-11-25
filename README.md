# Swift — Constants and Variables

## Objectives

1. Distinguish instances created with `let` or `var`.
2. Create instances of the basic value types and strings.
3. Overview Swift operators and the new identity operators `===` and `!==`.
4. Use the string literal `""` to create a string instance.
5. Concatenate strings with the overridden addition operator `+`.
6. Interpolate strings with the literal syntax, `\()`.
7. Print instances to the debug console using the `print()` function.

## `let` & `var`

![](https://curriculum-content.s3.amazonaws.com/swift/swift-constants-and-variables/bioshock_bird_and_cage.jpg)  
— Bird and Cage pendant, fan art jewelry for *Bioshock Infinite* by [leagueOfShadows](https://www.etsy.com/listing/128142086/bioshock-infinite-birdcage-necklace?ga_order=most_relevant&ga_search_type=all&ga_view_type=gallery&ga_search_query=bioshock%20cage%20bird&ref=sr_gallery_1)

Swift employs the keywords `let` and `var` for naming instances. The `let` keyword declares an instance as a *constant*, meaning that it cannot be overwritten after it's been created (though its variable properties *can* be altered later). The `var` keyword declares an instance as a *variable*, meaning that it *can* be changed at a later time.

**Objective-C:** *Swift's use of the word "constant" is not a direct translation from Objective-C's "constant", which takes the form of a globally-accessible value. Swift's terminology for "constant" and "variable" is synonymous to Objective-C's use of "immutable" and "mutable".*

The first section of [The Basics chapter](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/TheBasics.html) in Apple's Swift programming guide discusses these keywords in more detail.

### Implicit Typing

When creating instances, the compiler will infer the type of the instance you are creating based upon the instance's initial assignment. The compiler will enforce that future uses of any given instance fall into accordance with the instance's type. Any variables created with `var` can only be reassigned to a value of that same type (i.e. a string value cannot be assigned to an integer instance).

### Value Types

Objective-C programmers are all too familiar with distinguishing primitives from objects. Swift has no such distinction: integers, floats, and booleans are all held as objects. The value types `Int` (integer), `Double` (floating-point), and `Bool` (boolean) are typed implicitly based upon initial assignment:

```swift
let two = 2       // Int
let negSeven = -7 // Int
let twoPointZero = 2.0 // Double
let pi = 3.14159       // Double
let isTrue = True    // Boolean
let isFalse = False  // Boolean
```
**Advanced:** *Unsigned integers are available as* `UInt` *but require explicit-typing to declare, which we'll cover later. Apple discourages widespread use of* `UInt`, *even for values that can only be positive.*

## Operators

Since Swift is a C-family language, the typical C operators are available with their usual behavior and precedence.

A couple of notable distinctions in Swift are that:

1. The assignment operator (`=`) no longer returns a boolean value, which makes it more difficult to accidentally type an assignment operator into an evaluation instead of a comparison operator.

2. Swift includes the normal comparison operators `==` (a.k.a. "double equals") and `!=` ("not equal to") which measure whether or not two instances hold the *same value*, **and** includes two *identity* operators, `===` (a.k.a. "triple equals") and `!==` ("not identical to") which measure whether two instances are the *exact same reference.*

Reference the [Basic Operators chapter](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/BasicOperators.html#//apple_ref/doc/uid/TP40014097-CH6-ID60) of Apple's documentation for detailed information.

## Strings

### The String Literal `""`

In Swift, the string literal uses a pair of double-quotes to encapsulate its text value which can be assigned to an instance declared with either `let` or `var` (among many other uses):

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

Swift allows for custom uses of certain operators, which means that the addition operator (`+`) has been overridden for use with string literals to serve as a "concatenation literal". For programmers with experience using Ruby or Python, this will feel very familiar:

```swift
let message = greeting + flatiron
```

The `message` instance will now hold the awkward string value `"Hello, welcome tothe Flatiron School"`. We can add a space and an ending punctuation by using string literals with more addition operators:

```swift
let message = greeting + " " + flatiron + "."
```
The `message` instance will now hold the string value `"Hello, welcome to the Flatiron School."`. This concatenation literal can mix string instances with string literals without penalty.

### String Interpolation with `"\()"`

Swift also allows string interpolation to be done with a literal syntax as well. In stark contrast to the messy Objective-C syntax of matching format specifiers up with variable names, Swift allows an instance to be passed directly into a string literal with the interpolation syntax `\(instanceName)`.

This means we can create our `message` instance without concatenation by passing the `greeting` and `flatiron` instances directly into a new string literal:

```swift
let message = "\(greeting) \(flatiron)."
```
The `message` instance will hold the same string value as above, `"Hello, welcome to the Flatiron School."`.

Reference the [Strings and Characters chapter](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/StringsAndCharacters.html#//apple_ref/doc/uid/TP40014097-CH7-ID285) of Apple's documentation for more detailed information.

## Printing An Instance to the Debug Console

Swift's `print()` function will send a string representation of any instance to the debug console. It can be sent an instance directly, or be sent a string literal which may or may not include interpolation arguments:

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

**Objective-C:** `NSLog()` *is actually available in Swift, however, it requires more resources to process than using the native* `print()` *function in part because* `print()` *does not prepend the project name and time stamp to the string sent to LLDB.*
