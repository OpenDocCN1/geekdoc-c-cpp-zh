# Set Operators

LINQ supports some of the set operations through the standard LINQ operators. The set operation in LINQ produces the resultant set based on the presence or absence of the equivalent elements within the same or different sets. Let’s learn about the four types of standard LINQ set operations, which are given as follows:

+   - Union
+   - Except
+   - Intersect
+   - Distinct

The Union operation in LINQ is performed with the help of Union() method. This method takes two sets of elements and returns a set containing the unique elements that appear in both the sets. The Except operation signifies the set difference between two sets that gives a set containing elements of one set that do not appear in the second set. The Except() method is used to carry the set difference operation between two sets. The Intersect operation is achieved with the Intersect() method, which gives a set that contains the common elements in two sets. The Distinct operation removes all the duplicate elements from a set and it is performed using the Distinct() method. Listing 19.32 shows the implementation of all the four operations:

**Listing 19.32:** Showing an Example of Union, Except, Intersect, and Distinct Operations

```
using System;
using System.Linq;

class Program
{
    public static void Main()
    {
        int[] set1 = { 1, 2, 3, 4, 5 };
        int[] set2 = { 3, 5, 6, 7, 8 };

        //Union operation
        var resultUnion = set1.Union(set2);

        Console.WriteLine("The result of Union operation is....");
        foreach (int i in resultUnion)
            Console.WriteLine(i);

        //Except operation
        var resultExcept = set1.Except(set2);

        Console.WriteLine("The result of Except operation is....");
        foreach (int i in resultExcept)
            Console.WriteLine(i);

        //Intersection operation
        var resultIntersect = set1.Intersect(set2);

        Console.WriteLine("The result of Intersection operation is....");
        foreach (int i in resultIntersect)
            Console.WriteLine(i);

        //Distinct operation
        int[] set = { 1, 2, 3, 2, 1, 5, 1, 9 };
```