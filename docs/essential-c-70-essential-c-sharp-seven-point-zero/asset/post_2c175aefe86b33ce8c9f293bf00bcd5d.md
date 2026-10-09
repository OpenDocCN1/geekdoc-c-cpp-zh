
```csharp
Console.WriteLine("Throw exception");
throw new Exception("Arbitrary exception");
Console.WriteLine("End executing");
}
catch (FormatException exception)
{
Console.WriteLine("A FormatException was thrown");
}
catch (Exception exception)
{
Console.WriteLine($"Unexpected error: { exception.Message }");
}
catch
{
Console.WriteLine("Unexpected error!");
}
}
Console.WriteLine("Shutting down...");
}
```

### OUTPUT 5.15

```text
Begin executing
Throw exception...
Unexpected error: Arbitrary exception
Shutting down...
```

As the arrows in Listing 5.26 depict, throwing an exception causes execution to jump from where the exception is thrown into the first catch block within the stack that is compatible with the thrown exception type. 6 In this case, the second catch block handles the exception and writes out an error message. In Listing 5.26, there is no finally block, so execution falls through to the System.Console.WriteLine() statement following the try/catch block.

To throw an exception, it is necessary to have an instance of an exception. Listing 5.26 creates an instance using the keyword `new` followed by the type of the exception. Most exception types allow a message to be generated as part of throwing the exception, so that when the exception occurs, the message can be retrieved.

> 6. Technically it could be caught by a compatible catch filter as well.

Sometimes a catch block will trap an exception but be unable to handle it appropriately or fully. In these circumstances, a catch block can rethrow the exception using the **throw** statement without specifying any exception, as shown in Listing 5.27.

### LISTING 5.27: Rethrowing an Exception

```csharp
...
catch (Exception exception)
{
    Console.WriteLine(
        $@"Rethrowing unexpected error: {
            exception.Message }");
    throw;
}
...
```

In Listing 5.27, the **throw** statement is “empty” rather than specifying that the exception referred to by the exception variable is to be thrown. This illustrates a subtle difference: **throw;** preserves the *call stack* information in the exception, whereas **throw exception;** replaces that information with the current call stack information. For debugging purposes, it is usually better to know the original call stack.

### Guidelines

- **DO** prefer using an empty throw when catching and rethrowing an exception so as to preserve the call stack.
- **DO** report execution failures by throwing exceptions rather than returning error codes.
- **DO NOT** have public members that return exceptions as return values or an out parameter. Throw exceptions to indicate errors; do not use them as return values to indicate errors.

### Avoid Using Exception Handling to Deal with Expected Situations

Developers should make an effort to avoid throwing exceptions for expected conditions or normal control flow. For example, developers should not expect users to enter valid text when specifying their age. 7

> 7. In general, developers should expect their users to perform unexpected actions; in turn, they should code defensively to handle “stupid user tricks.”

Therefore, instead of relying on an exception to validate data entered by the user, developers should provide a means of checking the data before attempting the conversion. (Better yet, they should prevent the user from entering invalid data in the first place.) Exceptions are designed specifically for tracking exceptional, unexpected, and potentially fatal situations. Using them for an unintended purpose such as expected situations will cause your code to be hard to read, understand, and maintain.

Additionally, like most languages, C# incurs a slight performance hit when throwing an exception—taking microseconds compared to the nanoseconds most operations take. This delay is generally not noticeable in human time—except when the exception goes unhandled. For example, when Listing 5.22 is executed and the user enters an invalid age, the exception is unhandled and there is a noticeable delay while the runtime searches the environment to see whether there is a debugger to load. Fortunately, slow performance when a program is shutting down isn’t generally a factor to be concerned with.

### Guidelines

- **DO NOT** use exceptions for handling normal, expected conditions; use them for exceptional, unexpected conditions.

### ADVANCED TOPIC

### Numeric Conversion with TryParse()

One of the problems with the `Parse()` method is that the only way to determine whether the conversion will be successful is to attempt the cast and then catch the exception if it doesn’t work. Because throwing an exception is a relatively expensive operation, it is better to attempt the conversion without exception handling. In the first release of C#, the only data type that enabled this behavior was a `double` method called `double.TryParse()`. However, this method is included with all numeric primitive types starting with the Microsoft .NET Framework 2.0. It requires the use of the `out` keyword because the return from the `TryParse()` function is a `bool` rather than the converted value. Listing 5.28 is a code snippet that demonstrates the conversion using `int.TryParse()`.

### LISTING 5.28: Conversion Using int.TryParse()

```csharp
if (int.TryParse(ageText, out int age))
{
    Console.WriteLine(
        $"Hi { firstName }! "
        + $"You are { age*12 } months old.");
}
else
{
    Console.WriteLine(
        $"The age entered, { ageText }, is not valid.");
}
```

With the Microsoft .NET Framework 4, a `TryParse()` method was also added to enum types.

With the `TryParse()` method, it is no longer necessary to include a try/catch block simply for the purpose of handling the string-to-numeric conversion.

### SUMMARY

This chapter discussed the details of declaring and calling methods, including the use of the keywords `out` and `ref` to pass and return variables rather than their values. In addition to method declaration, this chapter introduced exception handling.

A method is a fundamental construct that is a key to writing readable code. Instead of writing large methods with lots of statements, you should use methods to create “paragraphs” of roughly 10 or fewer statements within your code. The process of breaking large functions into smaller pieces is one of the ways you can refactor your code to make it more readable and maintainable.

The next chapter considers the class construct and describes how it encapsulates methods (behavior) and fields (data) into a single unit.

This page intentionally left blank

## 6 Classes

You briefly saw in Chapter 1 how to declare a new class called `HelloWorld`. In Chapters 2 and 3, you learned about the built-in primitive types included with C#. Since you have now also learned about control flow and how to declare methods, it is time to discuss defining your own types. Type definition is a core construct of any C# program; this support for classes and the objects created from them is what makes C# an object-oriented language.

![](img/ef6a8a417630b222bfb3f3b949facff0_277_0.png)

This chapter introduces the basics of object-oriented programming using C#. A key focus is on how to define classes, which are the templates for objects themselves.

All of the constructs of structured programming from the previous chapters still apply within object-oriented programming. However, by wrapping those constructs within classes, you can create larger, more organized programs that are more maintainable. The transition from structured, control-flow-based programs to object-oriented programs revolutionized programming because it provided an extra level of organization. The result was that smaller programs were simplified somewhat. Even more important, it was easier to create much larger programs because the code within those programs was better organized.

One of the key advantages of object-oriented programming is that instead of creating new programs entirely from scratch, you can assemble a collection of existing objects from prior work, extending the classes with new features, adding more classes, and thereby providing new functionality.

Readers unfamiliar with object-oriented programming should read the Beginner Topic blocks for an introduction. The general text outside the Beginner Topics focuses on using C# for object-oriented programming with the assumption that readers are already familiar with object-oriented concepts.

This chapter delves into how C# supports encapsulation through its support of constructs such as classes, properties, and access modifiers; we covered methods in Chapter 5. Chapter 7 builds on this foundation with the introduction of inheritance and the polymorphism that object-oriented programming enables.

### BEGINNER TOPIC

### Object-Oriented Programming

The key to programming successfully today lies in the ability to provide organization and structure to the implementation of the complex requirements of large applications. Object-oriented programming provides one of the key methodologies in accomplishing this goal, to the point that it is difficult for object-oriented programmers to envision transitioning back to structured programming, except for the most trivial programs.
