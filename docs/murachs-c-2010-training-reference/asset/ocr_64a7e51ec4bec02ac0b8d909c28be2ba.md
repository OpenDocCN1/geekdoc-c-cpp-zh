# A class that implements the IEnumerable<T> interface

```
public class CustomList<T> : IEnumerable<T>
{
    private List<T> list = new List<T>();
    // other members
    #region IEnumerable<T> Members
    public IEnumerator<T> GetEnumerator()
    {
        foreach (T item in list)
        {
            yield return item;
        }
    }
    #endregion
    #region IEnumerable Members
    System.Collections.IEnumerator System.Collections.GetEnumerator()
    {
        throw new Exception("The method or operation is not implemented.");
    }
    #endregion
}
```

# Code that use the class

```
Product p1 = new Product("VB10", "Murach's Visual Basic 2010", 54.50m);
Product p2 = new Product("CS10", "Murach's C# 2010", 54.50m);
CustomList<Product> list = new CustomList<Product>();
list.Add(p1);
list.Add(p2);
foreach (Product p in list)
{
    Console.WriteLine(p.ToString());
}
```

# Description

+   - The foreach loop only works on generic collections that implement the IEnumerable<T> interface. As a result, if you want to use the foreach loop on a generic collection that you've defined, you must implement the IEnumerable<T> interface.

+   - When implementing the GetEnumerator method, you can use the yield keyword with the return keyword to return the current element to the object that implements the IEnumerable<T> interface and yield control.

![](bbox=[0.058, 0.943, 0.585, 0.958])