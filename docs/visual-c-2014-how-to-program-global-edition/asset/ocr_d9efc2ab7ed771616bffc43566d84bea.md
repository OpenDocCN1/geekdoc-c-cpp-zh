# Chapter 21 Generic Collections: Functional Programming with LINQ/PLINQ

```
Console.Write("\nValues: ");
// iterate through the int array with an enumerator
enumerator = intValues.GetEnumerator();
while (enumerator.MoveNext()) {
    Console.Write("$ {enumerator.Current}");
}
Console.Write("\nValuesCopy: ");
// iterate through the second int array with a foreach statement
foreach (var element in intValuesCopy) {
    Console.Write("$ {element}");
}
Console.WriteLine();
```

Initial array values:
doubleValues: 8.4 9.3 0.2 7.9 3.4
intValues: 1 2 3 4 5 6
intValuesCopy: 0 0 0 0 0 0

Array values after Sort and Copy:
doubleValues: 0.2 3.4 7.9 8.4 9.3
intValues: 1 2 3 4 5 6
intValuesCopy: 1 2 3 4 5 6

5 found at element 4 in intValues
8763 not found in intValues

> Fig. 21.3 | Array class static methods for common array manipulations. (Part 3 of 3)

# 21.3.1 C# using static Directive

The directives in lines 3 and 5 use the namespace System (for Array and Console) and System.Collections (for interface Enumerator, which we discuss shortly). Line 4 introduces C# 6 using static directive for accessing a type's static members without fully qualifying their names—in this case, class Array's static members. Line 23

Sort(doubleValues); // unqualified call to Array static method Sort
shows an unqualified call to Array static Sort, which is equivalent to
Array.Sort(doubleValues); // call to Array static method Sort

Though we could use unqualified calls for all of Array's static members in this example (e.g., Copy in line 26 and BinarySearch in lines 33 and 39), the code is easier to read with the fully qualified method calls, which make it absolutely clear which class contains a generic method.