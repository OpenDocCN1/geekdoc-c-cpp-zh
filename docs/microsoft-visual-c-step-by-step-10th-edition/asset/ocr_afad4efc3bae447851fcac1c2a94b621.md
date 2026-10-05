```
static void Main(string[] args)
{
    foreach (int item in tree)
    {
        Console.WriteLine(item);
    }
}
```

9. On the Debug menu, select Start Without Debugging.

The program runs and displays the values in the following sequence:

Click here to view code image

-12, -8, 0, 5, 5, 10, 11, 14, 15

+   10. Press Enter to return to Visual Studio 2022.

# Implementing an enumerator by using an iterator

As you can see, the process of making a collection enumerable can become complex and potentially prone to error. To make life easier, C# provides iterators that can automate much of this process.

An iterator is a block of code that yields an ordered sequence of values. An iterator is not actually a member of an enumerator class; rather, it specifies the sequence that an enumerator should use for returning its values. In other words, an iterator is just a description of the enumeration sequence that the C# compiler can use for creating its own enumerator. This concept requires a little thought to understand properly, so consider the following simple example.

# A simple iterator

The following BasicCollection<T> class illustrates the principles of implementing an iterator. The class uses a List<T> object to hold data and provides the FillList method to populate this list. Notice also that the BasicCollection<T> class implements the IEnumerable<T> interface. The GetEnumerator method is implemented by using an iterator: