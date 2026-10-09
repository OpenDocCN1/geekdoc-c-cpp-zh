
and `Pop()` methods as public API.

This example shows four different possible implementations of the `Pop()` method. (Obviously, you will only need one.) The implementation of the `Push()` method is straightforward. But, for `Pop()`, we need to consider an edge case when the stack does not contain any data.

Traditionally, we could have indicated this special situation by returning the `null` value, if T is a reference type, as shown in the first `Pop()` method. This implementation is not as convenient when T is a value type since the type's `default` value might be a valid value for the stack data.

Another way is just to throw an exception. This example implementation is shown in the `PopOrDie()` method. The caller will need to try and catch any possible exceptions. As alluded throughout the earlier parts of this book, the modern trend in C# programming is not to use exceptions, when avoidable. (And, avoid the `null` value, if possible.)

A "better" alternative might be using the `TryXXX` pattern. This is shown in the implementation of the `bool TryPop(out T? tok)` method. We have seen a number of such "Try" methods earlier in the book. We only use the `tok` out parameter value if the method returns `true`.

The `PopSoft()` method essentially follows the same pattern, but it uses a tuple return value instead of using the `out` parameter.

Again, the choice is yours. The C# programming style is changing, and there is no "right" or "wrong" way. It is really a matter of preference at this point.

If you implement a calculator, then you will likely define a "token" type (for numbers and operators) and it is this token type that will be stored in the stack (the `T` type parameter). In the example above, the nullable `T?` type is an artifact of the generic implementation. You will likely use a non-nullable record/struct as a token type, but there is no easy way to specify that as a generic type constraint, as of the current version of C#.

## 30.3. Sample Implementations

We will leave the implementation to the readers. After all, this is a "hands-on" project. ☮ An example program is included in the appendix: Code Listing - Part IV.

No cheating! 🙃☮🙃

There are two implementations. reverse-polish-1 and reverse-polish-2. They are more or less equivalent, but one sample program uses a property `TokType` to distinguish different token types. The other one uses the object types, and the polymorphism, to achieve the same.

One sample code is not necessarily "better" than the other. But, there will be situations where one style is preferred over the other. It will be instructive to compare these two programs.

Not all input sequences are valid expressions in the postfix notation. The sample program, either version, does not do much error handling when it encounters an invalid input expression. It will be a good exercise to think of a good error handling method for this problem.

# Lesson 31. Web To-Do List

## 31.1. Project Idea

Creating a "to do list" app is one of the most popular projects for beginning programmers.

Here’s a list of requirements for this final project:

- 1. Create a Web server app that stores to-do list items in memory.
- 2. Create a CLI client which connects to the server via HTTP.
- 3. The client app supports the following commands:
    - Create a to-do item.
    - List all current to-do items.
    - Delete an item.
    - Update an item.

> There is no more sample code for the remaining final projects. This is the time for you to test your C# skills, and to have fun! 🕊️

![](img/25af69ec45b3c0b589a8dccd0c2a88be_489_0.png)

# Lesson 32. Rubik’s Cube Challenge

## 32.1. Final Final Projects

Here’s one final "very ambitious" project. Or, more like three projects.

*Let’s "solve" Rubik’s cube using computers!!!*

We will try this in three different ways.

![](img/25af69ec45b3c0b589a8dccd0c2a88be_490_0.png)

## 32.2. Random Tries

If we try various moves enough times on a cube, then will it reach the target state? Try a series of random rotations, in an infinite loop, and check if the cube is in the perfectly ordered state.

## 32.3. Optimization

We can use a simple optimization technique to see if it works in solving the Rubik’s cube problem. Based on the arrangement of the tiles, assign a score for each configuration. That is, the more the cube is ordered, the higher score it will have.

Try an optimization technique using this score value.

## 32.4. Rubik’s Cube Algorithm

In fact, a (semi-)deterministic algorithm exists to solve the Rubik’s cube, *Rubik's Cube 3x3 guide* [https://www.rubiks.com/en-uk/rubiks-cube-3x3-guide]. Try implementing this algorithm in C#.

ℹ️ These are not easy projects for beginners, or for anyone. Give them a try. Just remember. The whole point is *having fun*. Good luck! 👍

# Author's Note

# Final Remarks

Congratulations! You made it!

It is not easy to read a technical book like this from beginning to end, regardless of your skill levels. This is a big achievement. Congrats!

As stated, knowledge is familiarity. The more you read, and the more you practice, the better you will become. In any art. Especially, in the art of programming.

Hope you had as much fun reading this book as I did writing it.

# Appendix A: C# Keywords

## C# Language Keywords

**abstract**

The `abstract` modifier can be used with classes and records, and member methods and properties to indicate that the implementation is missing or incomplete.

**as**

The `as` operator is used to perform conversions between compatible reference types. It evaluates to `null` if conversion fails.

**async**

The `async` modifier is used to specify that a method, lambda expression, or anonymous method is asynchronous.

**await**

The `await` operator suspends evaluation of the enclosing `async` method until the asynchronous operation represented by its operand completes.

**base**

The `base` keyword is used to access members of the base class from within a derived class or record.

**break**

The `break` statement terminates the closest enclosing loop or switch statement in which it appears.

**case**

The `switch` statement is a control statement that handles multiple selections by passing control to one of the case statements within its body.

**catch**

The try-catch statement consists of a try block followed by one or more catch clauses, which specify handlers for different exceptions.

**checked**

The checked keyword is used to control the overflow-checking context for integral-type arithmetic operations and conversions.

**class**

The keyword class is used to define a reference type.

**const**

The const keyword is used to declare a compile-time constant.

**continue**

The continue statement passes control to the next iteration of the enclosing iteration statement in which it appears.

**default**

The default keyword can be used as the default label in the switch statement or as the default operator to produce the default value of a type.

**delegate**

A delegate declaration defines a reference type that can be used to encapsulate a method with a specific signature.

**do**

The do statement executes a statement or a block of statements repeatedly until a specified expression evaluates to false.

**dynamic**

An object of type dynamic bypasses static type checking. In most cases, it functions like it has type object.

**else**

The if-else statement selects a statement for execution based on the value of a Boolean expression.

**enum**

The `enum` keyword is used to declare an enumeration, a distinct type consisting of a set of named constants called the enum values.

**event**

The `event` keyword specifies an event.

**explicit**

The `explicit` keyword is used to declare an explicit user-defined type conversion operator.

**extern**

The `extern` modifier is used in a method declaration to indicate that the method is implemented externally.

**finally**

The `finally` block is useful for cleaning up any resources allocated in the `try` block.

**fixed**

Prevents relocation of a variable by the garbage collector.

**for**

The `for` loop executes a statement or a block of statements repeatedly until a specified expression evaluates to false.

**foreach**

The `foreach` statement repeats a group of embedded statements for each element in an array or collection.
