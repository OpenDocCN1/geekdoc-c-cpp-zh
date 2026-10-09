
expression.

```C
bool IsLeapYear(int year) {
    if ((year % 4 == 0 && year % 100 != 0) || year % 400 == 0) {
        return true;
    } else {
        return false;
    }
}
```

You can easily convince yourself that these two implementations behave exactly the same way for all eight different conditions. (true/false for 3 boolean expressions yields 8. $2 * 2 * 2 = 8.$) Hence the two methods are equivalent for all possible value of the input, year.

The Boolean $\&\&$ operator has a higher "precedence" than the $||$ operator in C#. Hence the the parentheses around the $\&\&$ expression can be omitted.

That’s the method `LeapYear3.IsLeapYear()` presented earlier. One can further "simplify" this method using the expression body syntax

```C
bool IsLeapYear(int year) => year % 4 == 0 && year % 100 != 0 || year % 400 == 0;
```

The whole method definition is now reduced to essentially just *one line!*

*Which style would you generally prefer?*

## 6.2. Code Reading - Check If the Given Year is a Leap Year

The operator precedence rule determines which parts of an expression get evaluated first. For example, 2 + 3 * 4 is evaluated to 2 + (3 * 4), which is 14. This is because the multiplication operator (*) has a higher "precedence" than the addition operator (+). The explicit use of the parentheses can change the evaluation order. For instance, (2 + 3) * 4 is evaluated to 20.

![](img/25af69ec45b3c0b589a8dccd0c2a88be_122_0.png)

The unary operators (e.g., - in front of a number) have the highest precedence. You can refer to the C# language reference for the complete list of the binary operator precedence rules, if necessary. But, you do not have to memorize these precedence rules. When in doubt, use the parentheses to make your intentions clear (e.g., to the human readers), rather than relying on some (possibly obscure) precedence rules.

Note that multiple binary operators may have the same precedence. In that case, operators of the same precedence associate from left to right. For example, 6.0 / 2.0 * 3.0 is the same as (6.0 / 2.0) * 3.0, which evaluates to 9.0.

Before we end this lesson, there are a few more things that we will need to review.

First of all, a C# program is a collection of custom type definitions (other than the top-level statement exception). For example, the sample program of this lesson included the LeapYear1, LeapYear2, and LeapYear3 classes as well as the IsLeapYear delegate.

As we will see throughout this book, a type can be defined with C# constructs like class, struct, record, enum, interface, and delegate.

Technically speaking, a static class (which cannot be instantiated) does not define a type. But, syntactically, it also belongs to these top-level elements that comprise a C# program.

## 6.2. Code Reading - Check If the Given Year is a Leap Year

As stated, the *namespaces* are only used to reduce the chance of name collision across different C# programs, and they do not play a role in the structure of a C# program.

The basic unit of the (physical) organization in .NET is an "assembly". If you compile your C# program for .NET 5, for instance, then it will be made to an assembly, an executable assembly in particular. Libraries are also built into assemblies (with .dll extension).

An executable or library program can use the code from other library assemblies. Code reuse and sharing happens across the assemblies. .NET provides a way to control who can access what, across different assemblies, as well as within the same assembly.

C# has a number of "access modifiers". For the top-level types that are not included in the definitions of other types, there are two kinds of access modifiers, *public* and *internal*.

The *public* types are accessible from other assemblies. The *internal* types are only accessible within the same assembly.

By default, if we do not specify an access modifier, the top-level types are considered *internal*. In our example, all three classes and the delegate are all internal, meaning that they are not meant to be shared with other programs/assemblies.

If we wanted to share the implementation of `LeapYear1`, for instance, so that other programmers could use our code, then we could have declared it as *public*:

```
public static class LeapYear1 {
    // ...
}
```

Again, namespaces do not play any role in this regards. The namespace names are simply part of the names that we are exporting. That is, the full name of LeapYear1 is Example.LeapYear1.

For the nested types (e.g., the types that are defined in another type), and for the members of a type (e.g., properties and methods), e.g., the LeapYear1() static method, the access control in C# is much more complicated. In fact, C# has several different access modifiers with different behaviors.

In this lesson, we used the internal access modifier for all three static methods, LeapYear1.IsleapYear(), LeapYear2.IsleapYear(), and LeapYear3.IsleapYear(). Internal methods can be accessed by anybody within the same program (or, assembly).

If we want to share IsleapYear(), then we would need to declare it as public as well, not just the IsleapYear class.

The default access level for the member methods, as in this case, is private. The private members can be accessed only within the definition/implementation of that type. If we omitted internal in the declarations of the three static methods, IsleapYear(), then they would not have been accessible from our "main program".

## Summary

A delegate in C# is a type, and it is used to represent a group of methods, (static methods or instance methods), that have the same certain function signature.

The delegate instances can be used just like any other objects, and they can be "called" as if they are methods.

Various access modifiers like public and internal can be used to control the access levels for your types and their members.

## 6.3. Exercises

In addition, we looked at the use of the `foreach` loop (over an array) in this lesson.

We primarily use `delegates` in the context of the functional style programming. We do not discuss another (important) use case of delegates, namely, "events", in this book. Events are mostly used in the "event driven programming styles" (obviously 🙂). If you do GUI programming, for instance, then you will end up using events more. We will leave it to the readers to find out what the event driven programming is, and what `events` are in C#.

1. Create a new program to accept a value of `year` as a user input. Write your own `IsLeapYear()` method without referring to the sample code. Test your program with a few `year` values, and verify that your program works as expected.
2. Create a new program to take a value of `year` as a command line argument. Do the same tests as the previous exercise.

# Author's Note

# Don't Be a Parrot

It is not uncommon to see a beginning programmer copy code from a book to a computer. Or, copy the code found on the Web to his/her computer.

Often they type the code, not even just copy and paste, and they claim that they *learn better* by actually typing.

There is no evidence for that. If anything, that will be a very inefficient way to learn programming. While an imitation is an important part of learning a new language, or a new skill, in the spirit of "listen and repeat", mindless imitations would not enhance your speaking or writing skills very much.

The author made a conscious decision not to release the sample code of this book. For one thing, it has little value. But, there are other reasons as well. In his opinion, the downloadable code samples do more harm than good.

Often the learning students download a code sample and run it on their computers. And, they think that that's the end of it. *It works. Now, let's move on.*

In doing so, however, they have learned very little. On the contrary, they only ended up with the false sense that they were able to "write" the same code because they compiled the code and ran it. Or, because they even "typed" the code.

Obviously, they did not *write* the code.

Although the author has asserted that this book is "for reading", if you are inclined to try out some sample code in this book, then here's a suggestion.

1. Learn the main points of the lesson.
