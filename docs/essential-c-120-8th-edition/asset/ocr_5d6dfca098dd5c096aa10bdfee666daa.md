# Chapter 4: Operators and Control Flow

In Chapter 1 we encountered warning CS8600, "Converting null literal or possible null value to non-nullable type" when assigning Console.ReadLine() to a string. The occurs because Console.ReadLine() returns a string rather than a non-nullable string. In reality, Console.ReadLine() returns null only if the input is redirected, which isn't a case we are expecting in these intro programs, but the compiler doesn't know that. To avoid the warning, we use the null-forgiving operator on the Console.ReadLine() return—stating we know that the value returned will be null (and if it is, we are comfortable throwing a null-reference exception).

```
string text = Console.ReadLine();
```

# ADVANCED TOPIC

# Leveraging the Null-Conditional Operator with its Delegates

The null-conditional operator is a great feature on its own. However, using it in combination with a delegate invocation resolves a C# pain point that has existed since C# 1.0. Notice in Listing 4.39 how the PropertyChanged event handler is assigned to a local copy (propertyName) before we check the value for null and finally fire the event. This is the easiest thread-safe way to invoke events without running the risk that an event unsubscribe will occur between the time when the check for null occurs and the time the event is fired. Unfortunately, this approach leads developers to follow this pattern—with the result of throwing inconsistent NullReferenceExceptions. Fortunately, with the introduction of the null-conditional operator, this issue has been resolved.

# LISTING 4.39: Null-Conditional Operator with Event Handlers

```
System.EventHandler propertyChanged =
    PropertyChanged;
if (propertyName != null)
{
    propertyName(this,
        new System.EventArgs());
}
```