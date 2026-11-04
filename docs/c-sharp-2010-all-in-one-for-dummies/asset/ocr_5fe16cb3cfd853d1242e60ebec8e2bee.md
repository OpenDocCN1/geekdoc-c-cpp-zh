Generics are nonvariant in C# 2.0 and 3.0. This means that if Basket<apple> is of type Basket<fruit>, those Baskets are not interchangeable like strings and objects are in the preceding example.

# Variance

If we look at a method like the preceding one:

```
```csharp
public static void WriteMessages()
{
    List<string> someMessages = new List<string>();
    someMessages.Add("The first message");
    someMessages.Add("The second message");
    MessagesToYou(someMessages);
}
```
```

and then we try to call that method like we did earlier with a string type:

```
```csharp
//This doesn't work in C#3!!
public static void MessagesToYou(IEnumerable<object> theMessages)
{
    foreach (var item in theMessages)
        Console.WriteLine(item);
}
```
```

this fails in Visual Studio 2008. Generics are invariant in C# 3.0. But, in Visual Studio 2010 this complies because IEnumerable<T> is covariant — you can use a more derived type as a substitute for a higher-order type. Let's look at a real example.

# Contravariance

In my scheduling application, I have Events, which have a date, and then a set of subclasses, one of which is Course. A Course is an Event. Courses know their own number of students.

Anyway, back at the ranch, I have a method called MakeCalendar.

```
```csharp
public void MakeCalendar(IEnumerable<Event> theEvents)
{
    foreach (Event item in theEvents)
    {
        Console.WriteLine(item.WhenItIs.ToString());
    }
}
```
```