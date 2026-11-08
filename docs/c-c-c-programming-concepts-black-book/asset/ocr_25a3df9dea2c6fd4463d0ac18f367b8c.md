argument type are same as the delegate. These two delegate handler methods operate on two different data types; and therefore, impose the flexibility. The two handler methods compare the emp_ID and name and depending on the result, return either true or false. The preceding code also has a class named DelExample that holds the Main() method. This class has first instantiated the two instances of the Employee class and then saved them in an Employee array. Within the Main() method, we have first created an object of the DelExample class and then created the two objects of delegate methods for each delegate handler method. The output of the preceding code is given as follows:

```
George Mallory comes before John Mathew
1001 is either equal to or smaller than 1005
```

# Defining Events

In traditional console applications, there were no options for a developer to write a code that can be fired on the click of some keys. To execute an event on the click of a key, we need to follow certain steps of execution manually. However, nowadays, most of the applications are event driven. Therefore, C# allows a developer to write events in a program. Event in C# is a kind of delegate that can only be invoked from within the class where the delegate ID is declared.

Suppose a class includes a definition of an event. It may happen that an application contains more than one class and one of the class want to use the event declared in another class. This operation can be done by using delegates. In Listing 18.17 shows how an event can be used in a C# program:

Listing 18.17: Showing an Example of Event

```
using System;
//Defining delegate
delegate void PromotedDelegate();
class Program
{
    public static void Main()
    {
        Friend f = new Friend();
        Employee e = new Employee();
        //Adding event handler to PromotedEvent event
        e.PromotedEvent += new PromotedDelegate(f.CallWhenPromoted);
        //Invoking the event
        e.Promote();
    }
}
class Employee
{
    //Defining an event
    public event PromotedDelegate PromotedEvent;
    public void Promote()
    {
        PromotedEvent();
    }
}
class Friend
{
    //This method is called when the event is fired
    public void CallWhenPromoted()
    {
        Console.WriteLine("Thanks for callling.....");
    }
}
```