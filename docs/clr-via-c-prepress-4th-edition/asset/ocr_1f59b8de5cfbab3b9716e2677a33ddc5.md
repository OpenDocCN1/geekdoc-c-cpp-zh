amount of money to transfer between accounts. Obviously, the goal of the Transfer method is to subtract money from one account and add money to another. The Transfer method could fail for many reasons: the from or to argument might be null; the from or to argument might not refer to an open account; the from account might have insufficient funds; the to account might have so much money in it that adding more would cause it to overflow; or the amount argument might be 0, negative, or have more than two digits after the decimal place.

When the Transfer method is called, its code must check for all of these possibilities, and if any of them are detected, it cannot transfer the money and should notify the caller that it failed by throwing an exception. In fact, notice that the Transfer method's return type is void. This is because the Transfer method has no meaningful value to return; if it returns at all, it was successful. If it fails, it throws a meaningful exception.

Object-oriented programming allows developers to be very productive because you get to write code like this:

```
```
Boolean f = "Jeff".Substring(1, 1).ToUpper().EndsWith("E"); // true
```
```

Here I'm composing my intent by chaining several operations together.¹¹ This code was easy for me to write and is easy for others to read and maintain because the intent is obvious: Take a string, grab a portion of it, uppercase that portion, and see if it ends with an 'E.' This is great, but there is a big assumption being made here: no operation fails. But, of course, errors are always possible, so we need a way to handle those errors. In fact, there are many object-oriented constructs—constructors, getting/setting a property, adding/removing an event, calling an operator overload, calling a conversion operator—that have no way to return error codes, but these constructs must still be able to report an error. The mechanism provided by the Microsoft .NET Framework and all programming languages that support it is called exception handling.

**Important** Many developers incorrectly believe that an exception is related to how frequently something happens. For example, a developer designing a file Read method is likely to say the following: "When reading from a file, you will eventually reach the end of its data. Since reaching the end will always happen, I'll design my Read method so that it reports the end by returning a special value; I won't have it throw an exception." The problem with this statement is that it is being made by the developer designing the Read method, not by the developer calling the Read method.
When designing the Read method, it is impossible for the developer to know all of the possible situations in which the method gets called. Therefore, the developer can't possibly know how often the caller of the Read method will attempt to read past the end of the file. In fact, since most files contain structured data, attempting to read past the end of a file is something that rarely happens.

¹¹ In fact, C#'s extension method feature exists in the language to allow you to chain more methods together that would not have been chainable otherwise.