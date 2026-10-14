object in the delegate, the application can subsequently invoke the method through the delegate, like this:

```
performCalculationDelegate();
```

This looks like an ordinary method call; if you did not know otherwise, it looks like you might actually be running a method named *performCalculationDelegate*. However, the common language runtime (CLR) knows that this is a delegate, so it retrieves the method that the delegate references and runs that instead. Later on, you can change the method to which a delegate refers, so a statement that calls a delegate might actually run a different method each time it executes. Additionally, a delegate can reference more than one method at a time (think of it as a collection of method references), and when you invoke a delegate all the methods to which it refers will run.

# Note

If you are familiar with C++, a delegate is similar to a function pointer. However, unlike function pointers, delegates are completely type safe. You can make a delegate refer only to a method that matches the signature of the delegate, and you cannot invoke a delegate that does not refer to a valid method.

# Examples of delegates in the .NET Framework class library

The Microsoft .NET Framework class library makes extensive use of delegates for many of its types, two examples of which are in Chapter 18, “Using collections”: the *Find* method and the *Exists* method of the *List<T>* class. If you recall, these methods search through a *List<T>* collection, either returning a matching item or testing for the existence of a matching item. When the designers of the *List<T>* class were implementing it, they had absolutely no idea about what should actually constitute a match in your application code, so they let you define that by providing your own code in the form of a predicate. A predicate is really just a delegate that happens to return a Boolean value.

The following code should help to remind you how to use the *Find* method:

Click here to view code image

```
struct Person
{
    public int ID { get; set; }
    public string Name { get; set; }
    public int Age { get; set; }
}
...
List<Person> personnel = new List<Person>()
```