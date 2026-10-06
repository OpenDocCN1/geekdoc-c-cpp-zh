nonalpabet characters in the variable name and eventually improve the readability of your code.
Examples are shown in Listing 1-5.

# LISTING 1-5 Defining a variable

```
// variable with a space
let `my variable` = 4

// variable using a keyword
let `let` = 4

// apostrophe (\') in a variable name
let mySon's = "Feb 1, 2010"
let x' = 3

// include # in the variable name
let `F#` = "this is an F# program."
```

# Flow Control

To write F# applications in an imperative style, you need to know how to define flow-control statements. F# supports several types of flow control to accomplish this, the *for* loop, *while* loop, and *if* expression. These statements segment the program into different scopes. C# uses {} to segment code into scopes, while F# does not use these items. Instead, F# uses the space indent to identify program scopes. This section discusses these three statements in detail.

> Note Visual Studio can automatically convert the Tab key to space. If you edit F# code in another editor that does not support this conversion, you might have to do it manually.

# for Loop

There are two forms of the *for* loop: *for...to/downto* and *for...in*. The *for...to/downto* expression is used to iterate from a start value inclusively to or down to an end value inclusively. It is similar to the *for* statement in C#.

*FOR...IN* is used to iterate over matches of a pattern in an enumerable collection—for example, a range expression, sequence, list, array, or other construct that supports enumeration. It is like *foreach* in C#. Looking at the C# code that began this chapter, you can use two for options (as shown in Listing 1-6) to accomplish the loop of code for each number between 0 and 100. The first approach uses *FOR...TO*, and the second approach uses *for...in*.