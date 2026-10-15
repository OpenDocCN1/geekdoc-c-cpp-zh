FindAll() takes a parameter of type Predicate<T>, which is a reference to a method called a delegate. Listing 16.4 demonstrates how to use the FindAll() method.

# LISTING 16.4: Demonstrating FindAll() and Its Predicate Parameter

```
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        List<int> list = new List<int>();
        list.Add(1);
        list.Add(2);
        list.Add(3);
        list.Add(2);

        List<int> results = list.FindAll(Even);

        foreach(int number in results)
        {
            Console.WriteLine(number);
        }
    }

    public static bool Even(int value) =>
        (value % 2) == 0;
}
```

In Listing 16.4’s call to FindAll(), you pass a delegate instance, Even(). This method returns true when the integer argument value is even. FindAll() takes the delegate instance and calls into Even() for each item within the list (this listing uses C# 2.0’s delegate type inferencing). Each time the return value is true, it adds it to a new List<T> instance and then returns this instance once it has checked each item within list. A complete discussion of delegates occurs in Chapter 12.

# Dictionary Collections: Dictionary<TKey, TValue>

Another category of collection classes is the dictionary classes—specifically, Dictionary<TKey, TValue> (see Figure 16.3). Unlike the list collections, dictionary classes store name/value pairs. The name functions as a unique key that can be used to look up the corresponding element in a manner similar to that of using a primary key to access a record in a database. This adds