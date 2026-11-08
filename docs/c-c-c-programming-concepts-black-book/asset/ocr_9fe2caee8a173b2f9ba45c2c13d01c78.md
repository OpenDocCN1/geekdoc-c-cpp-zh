# Listing 19.34: Implementing the Cast and OfType Operators

```
~~~csharp
using System;
using System.Linq;
using System.Collections;
using System.Collections.Generic;

class program
{
    public static void Main()
    {
        ArrayList arr1 = new ArrayList { 1, 2, 3, 4, 5, 6, 7 };
        ArrayList arr2 = new ArrayList { 1, 2, 4, "A", "B", "C", '7' };

        //Converting arr1 using Cast operator
        IEnumerable<object> result = arr1.Cast<object>();

        //IEnumerable<string> result = arr1.Cast<string>();
        //This will Throw an exception

        Console.WriteLine("After applying Cast operator on arr1...");
        foreach (object obj in result)
        {
            Console.WriteLine(obj);
        }
        //Converting arr2 using OfType operator
        IEnumerable<int> query = arr2.OfType<int>();

        Console.WriteLine("After applying OfType operator on arr2...");
        foreach (int i in query)
        {
            Console.WriteLine(i);
        }
    }
}
~~~
```

In Listing 19.34, we have first declared the two ArrayLists: one that contains only the integers and another that contains integers, strings, and characters. Then, we have applied the Cast operator on arr1 and converted the elements into an object type. This process will be executed successfully. However, if we attempt to convert an integer type to a string type by using the Cast operator, then the compiler will throw an exception. We have also applied the OfType operator on the second ArrayList, named arr2. In this case, the OfType() method goes through every element in arr2 and converts the elements that can be converted to the desired type. The resultant elements are stored in a new variable of type IEnumerable<int>. The output of the program is given as follows:

```
~~~text
After applying Cast operator on arr1...
1
2
3
4
5
6
7
After applying OfType operator on arr2...
1
2
4
~~~
```