
# Example 36 Creating Dimensional Arrays

This example shows two ways (r1, r2) to create the rectangular array and three ways (t1, t2, t3) to create the jagged array in section 9.2. One cannot create a jagged array in one operation (as in t4).

```c
double[] r1 = { 0.0, 0.1 }, { 1.0, 1.1 }, { 2.0, 2.1 };
double[] r2 = new double[3,2];
for (int i=0; i<3; i++)
  for (int j=0; j<2; j++)
    r2[i,j] = i + 0.1 * j;
```

```c
double[][] row0 = { 0.0 }, row1 = { 1.0, 1.1 }, row2 = { 2.0, 2.1, 2.2 };
double[][] t1 = { row0, row1, row2 };
double[][] t2 = { new double[0], new double[1], new double[2.0, 2.1, 2.2] };
double[][] t3 = new double[3]; // Creates first-dimension array
for (int i=0; i<3; i++)
  t3[i] = new double[i+1]; // Creates second-dimension array
  for (int j=0; j<=i; j++)
    t3[i,j] = i + 0.1 * j;
double[][] t4 = new double[3][]; // Illegal array creation
```

# Example 39 Using Multidimensional Arrays

To store the exchange rate between U.S. dollars and euros (SUS per euro) for every day in the years 2000–2009 using an array rate of type double[][]; a two-dimensional rectangular array of one-dimensional arrays with element type. The array[y,m] holds the exchange rate for year y+2000, month m+1, day d+1. The array of type double[][][] is used because each of the ten years has 12 months (rectangular), but not all months have the same number of days (jagged).

```csharp
double[][][] rate = new double[10][12];
rate[0, 0] = new double[31]; // Jan 2000 has 31 days
rate[1, 0] = new double[29]; // Feb 2000 has 29 days
rate[2, 0] = new double[31]; // Mar 2000 has 31 days
rate[3, 0] = new double[30]; // Apr 2000 has 30 days
rate[4, 0] = new double[31]; // May 2000 has 31 days
...
```

```csharp
rate[0,1][27] = 0.3748; // 28 Feb 2000
rate[0,1][28] = 0.9722; // 29 Feb 2000
rate[0,2][0] = 0.9651; // 1 Mar 2000
```

```csharp
for (int y=0; y<rate.GetLength(); y++)
  for (int m=0; m<rate[y].GetLength(); m++)
    if (rate[y,m] != null)
      for (int d=0; d<rate[y,m].Length; d++)
        if (rate[y,m][d] > 0)
          Console.WriteLine("{0:D4}-{1:D2}-{2:D2}: {3:F4} SUS/euro",
            y+2000, m+1, d+1, rate[y,m][d]);
```

# 9.3 Class Array

All types are derived from class Array, and the members of an array type are inherited from class Array. Let a be a reference of array type, o an object of any type, and i, j, ..., in integers:

- Length of type int is the length of a, that is, the total number of elements in a, if a is one-dimensional or a rectangular multidimensional array, or the number of elements in the first dimension of a, if a is a jagged array
- Rank of type int is the rank of a (sections 5 and 9.2.2)
- GetEnumerator() of type IEnumerator is a non-generic enumerator (section 27.2) for iterating through a. This enables the foreach statement to iterate over an array (section 13.6 and other 40). If a is a one-dimensional array of type t[], one can get a type-safe enumerator of type IEnumerator by computing (IList<t>).GetEnumerator()
- Length(i) of type int is the number of elements in dimension i (examples 27 and 39)
- SetValue(o,j,...,in) of type void performs the same assignment as a[i,...,in] = o when a has rank n; and GetValue(i,...,in) returns the same as a[i,...,in]. More precisely, if a[i,...,in] has reference type, then GetValue returns the same reference; otherwise it returns a boxed copy of the value of a[]
- Equals(o) of type bool returns true if a and o refer to the same array object, otherwise false.

Class Array provides static methods, which are listed below. These methods can be used in ordinary array types [t] which derive from class Array. The methods throw ArgumentNullException if the given array is null, and RankException if a is not one-dimensional.

- static BinarySearch(Array a, Object k) searches the one-dimensional array for a k using binary search. Returns an index i for which a[i].CompareTo(k) = 0; otherwise i<0 such that -i would be the proper position for k. The array must be sorted, by Sort(a), or the result is undefined; and elements must implement IComparable
- static BinarySearch(Array a, IComparer cmp) works similarly, but compares array elements using the cmp.Compare method (section 27.3). The array must be sorted, by Sort(cmp), or the result is undefined.
- static void Reverse(Array a, int i, int n) reverses the elements of a[i..(i+n-1)].
- static void Sort(Array a, IComparer cmp) sorts the one-dimensional array using a quicksort, comparing array elements using their CompareTo method (section 27). The array must be sorted, by Sort(cmp), or the result is undefined.
- static void Sort(Array a, IComparer cmp) sorts the one-dimensional array using a quicksort, comparing array elements using their CompareTo method (section 27). The array must be sorted, by Sort(cmp), or the result is undefined.

# Example 40 Length, Indexing, and foreach

This example uses rectangular array and jagged array.

# Example 41 Search in an Array

# Example 42 Swapping Two Arrays

# 10. Classes

# 10.1 Class Declarations and Class Bodies
