# Defining "Exception"

When designing a type, you first imagine the various situations in which the type will be used. The type name is usually a noun, as FileStream or StringBuilder. Then you define the properties, methods, events, and so on for the type. The way you define these members (property data types, method parameters, return values, and so forth) becomes the programmatic interface for your type. These members indicate what action can be performed by the type itself or on an instance of the type. These action members are usually verbs as Read, Write, Flush, Append, Insert, Remove, etc. When an action member cannot complete its task, the member should throw an exception.

> Important An exception is when a member fails to complete the task it is supposed to perform as indicated by its name.

Look at the following class definition.

```
internal sealed class Account {
    public static void Transfer(Account from, Account to, Decimal amount) {
        from = amount;
        to += amount;
    }
}
```

The Transfer method accepts two Account objects and a Decimal value that identifies an amount of money to transfer between. Obviously, the goal of the Transfer method is to subtract money from one account and add money to another. The Transfer method could fail for many reasons: the from or argument might be null; the from or argument might not refer to an open account; the account might have insufficient funds; the account might have so much money in it that adding more would cause it to overflow; or the amount might be 0, or more than two digits after the decimal place.

When the Transfer method is called, it must check for all of its possibilities, and if any of them are detected, it cannot transfer the money and notify the caller that it failed by throwing an exception. In fact, the Transfer method's return type is void. This is because the Transfer method has no meaningful value to return; if it returns at all, it was successful. If it fails, it throws a meaningful exception.

Object-oriented programming allows developers to be very productive because you get to write code like this:

```
Boolean f = "Jeff".Substring(1, 1).ToUpper().EndsWith("E"); // true
```

Here I'm composing my intent by chaining several operations together.¹ This code was easy to write and is easy to read and maintain because the intent is obvious: to take a string, grab

> ¹ In fact, C#'s extension method exists in the language to allow you to chain more methods together that would not have been chainable otherwise.