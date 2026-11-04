For example, the following code defines the generic Matcher class, which takes two generic type parameters T1 and T2. (Note that this code skips important error handling such as checking for null values to keep things simple.)

```
public class Matcher<T1, T2>
    where T1 : IComparable<T2>, new()
    where T2 : new()
{
    private void test()
    {
        T1 t1 = new T1();
        T2 t2 = new T2();
        ...

        if (t1.CompareTo(t2) < 0)
        {
            // t1 is "less than" t2.
            ...
        }

        ...
    }
}
```

The first constraint requires that type parameter T1 implement the IComparable interface for the type T2 so the code can compare T1 objects to T2 objects. The next constraint requires that the T1 type also provide a parameterless constructor. You can see that the code creates a new T1 object and uses its CompareTo method (which is defined by IComparable).

The second where clause requires that the type T2 also provide a parameterless constructor. The code needs that because it also creates a new T2 instance.

In general, you should use as few constraints as possible because that makes your generic code usable in as many circumstances as possible. If your code won't need to create new instances of a data type, don't use the new constraint. If your code won't need to compare objects, don't use the IComparable constraint.

# MAKING GENERIC METHODS

In addition to building generic classes, you can also build generic methods inside either a generic class or a regular non-generic class.

For example, suppose you want to rearrange the items in a list so the new order alternately picks items from each end of the list. If the list originally contains the numbers 1, 2, 3, 4, 5, 6, then the alternated list contains 1, 6, 2, 5, 3, 4.

The following code shows how a program could declare an Alternate method to return an alternated list. The part of the code that defines the generic parameter T is shown in bold.

```
public List<T> Alternate<T>(List<T> list)
{
    // Make a new list to hold the results.
    List<T> newList = new List<T>();
}
```