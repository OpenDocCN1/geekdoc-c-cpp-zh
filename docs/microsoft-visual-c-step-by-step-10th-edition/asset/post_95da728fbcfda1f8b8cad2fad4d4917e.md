
Click here to code image

```cs
Processor p = new Processor();
delegate ... performCalculationDelegate ...;
performCalculationDelegate = p.performCalculation;
```

Keep in mind that the statement that assigns the method reference to the delegate does not run the method at point; there are no parentheses after the method name, and you do not specify any parameters (if the method takes them). This is just an assignment statement.

Having stored a reference to the performCalculation method of the Processor object in the delegate, the application can subsequently invoke the method through the delegate, like this:

```cs
performCalculationDelegate();
```

This looks like an ordinary method call. If you didn't know otherwise, it looks like you might be running a method named performCalculationDelegate. However, the common language runtime (CLR) knows that this is a delegate, so it retrieves the method that the delegate references and that instead. Later, you can change the method to which the delegate refers, so a statement that calls a delegate might actually run a different method each time it executes. Additionally, a delegate can reference more than one method at a time (think of it as a collection of method references). When you invoke a delegate, all the methods it refers to will run.

> Note
> If you're familiar with C++, a delegate is similar to a function pointer. However, unlike function pointers, delegates are completely type safe. You can make a delegate refer only to a method that does not match the signature of the delegate, and you cannot invoke a delegate that does not refer to a valid method.

## Examples of delegates in the .NET class library

The Microsoft .NET class library makes extensive use of delegates for many of its types. Two examples are in Chapter 18, “Using collections”: the Find method and the EXISTS method of the List<T> class. As you might recall, these methods search through a List<T> collection, either returning a matching item or testing for the existence of a matching item. When the designers of the List<T> class were implementing, they had absolutely no idea about what should actually constitute a match in your application code, so they let you define that by providing your own code in the form of a predicate. A predicate is really just a delegate that happens to return a Boolean value.

The following code should help remind you how to use the Find method (shown in bold):

Click here to view code image

```cs
struct Person
{
    public int ID { get; set; }
    public string Name { get; set; }
    public int Age { get; set; }
}
...
List<Person> personnel = new List<Person>
{
    new Person() { ID = 1, Name = "John", Age = 53 },
    new Person() { ID = 2, Name = "Sid", Age = 28 },
    new Person() { ID = 3, Name = "Fred", Age = 34 },
    new Person() { ID = 4, Name = "Paul", Age = 22 }
};
// Find the member of the list that has an ID of 3
Person match = personnel.Find(p => p.ID == 3);
```

Other examples of methods exposed by the List<T> class that use delegates to perform their operations are Average, Max, Min, Count, and Sum. These methods take a Func delegate as the parameter. A Func delegate refers to a method that returns a value (a function). In the following examples, the Average method is used to calculate the average age of items in the personnel collection (Func<T> delegate simply returns the value in the Age field of each item in the collection), the Max method is used to determine the item with the highest ID, and the Count method is used to determine the number of items.

```cs
int averageAge = personnel.Average(p => p.Age);
int maxID = personnel.Max(p => p.ID);
int count = personnel.Count(p => p.Age > 30);
```
