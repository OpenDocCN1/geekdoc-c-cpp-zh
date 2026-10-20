# A class that implements the IEnumerable<> interface

```
public class CustomList<T> : IEnumerable<T>
{
    private List<T> list = new List<T>();

    // other members

    public IEnumerator<T> GetEnumerator()
    {
        foreach (T item in list)
        {
            yield return item;
        }
    }

    System.Collections.IEnumerator
        System.Collections.IEnumerable.GetEnumerator()
    {
        throw new NotImplementedException();
    }
}
```

# Code that uses the class

```
Product p1 = new Product("JAVA", "Murach's Java Programming", 59.50m);
Product p2 = new Product("C#", "Murach's C#", 59.50m);
CustomList<Product> list = new CustomList<Product>();
list.Add(p1);
list.Add(p2);
foreach (Product p in list)
{
    Debug.WriteLine(p.ToString());
}
```

# Description

+   - The foreach loop only works on generic collections that implement the IEnumerable<> interface. As a result, if you want to use the foreach loop on a generic collection that you’ve defined, you must implement the IEnumerable<> interface.
+   - When implementing the GetEnumerator() method, you can use the yield keyword with the return keyword to return the current element to the object that implements the IEnumerable<> interface and yield control.