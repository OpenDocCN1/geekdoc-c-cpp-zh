
### Output

Average of elements of array is 27.5

## 6.2 Array Class

### Concept

In C#, an array is treated as an object and inherited from the Array class. The Array class is defined in the System namespace.

### Explanation

- 1. Various properties of the Array class are listed below.

| Properties | Description | Basic syntax |
|---|---|---|
| Length | Returns the length of an array. It returns a 32-bit integer value. | Arrayname.Length |
| LongLength | Returns the length of an array. It returns a 64-bit integer value. | Arrayname.LongLength |
| Rank | Returns the rank or number of dimensions of an array. It returns an integer value. | Arrayname.Rank |
| IsFixedSize | Checks whether the array is of fixed size or not. It returns a Boolean value. | Arrayname.IsFixedSize |
| IsReadOnly | Checks whether the array is read-only or not. It returns a Boolean value. | Arrayname.IsReadOnly |

### Example

```csharp
// illustration of class Array and its properties
namespace arrayconcept
{
    class Arrayclassproperties
    {
        static void Main(string[] args)
        {
            int[] numbers = new int[9] { 11, 22, 33, 44, 55, 66, 77, 88, 99 };
            int arraylength, rank;
            long longlength;
            bool fixedsize, isarrayreadonly;

            arraylength = numbers.Length;
            Console.WriteLine("Length of array is {0}", arraylength);
            longlength = numbers.LongLength;
            Console.WriteLine("LongLength of array is {0}", longlength);
            rank = numbers.Rank;
            Console.WriteLine("Rank of array is {0}", rank);
            fixedsize = numbers.IsFixedSize;
            if (fixedsize)
                Console.WriteLine("Array has fixed size ");
            else
                Console.WriteLine("Array has No fixed size ");

            isarrayreadonly = numbers.IsReadOnly;
            if (isarrayreadonly)
                Console.WriteLine("Array is readonly");
            else
                Console.WriteLine("Array is NOT readonly");

            Console.ReadLine();
        }
    }
}
```

Input nil

### Output

```text
Length of array is 9
LongLength of array is 9
Rank of array is 1
Array has fixed size
Array is NOT readonly
```

### 2. Array Class methods

Commonly used methods of an array class are given below in the table.

| Array Class Methods | Description |
|---|---|
| Clear | Sets a range of elements in the Array to zero, to false, or to Nothing, depending on the element type. |
| Copy | Copies a range of elements from one Array starting at the first element and pastes them into another Array starting at the first element. |
| GetLength | Gets the number of elements present in an array. |
| GetLowerBound | Gets the lower bound of the specified dimension in the Array. |
| GetUpperBound | Gets the upper bound of the specified dimension in the Array. |
| IndexOf | Searches for the specified object and returns the index of the first occurrence within the entire one-dimensional Array. |
| Reverse | Reverses the sequence of elements of an array. |
| Sort | Sorts an array. |

### Example

```csharp
// Illustration of methods of class Array.

using System;

namespace arrayconcept
{
    class Arrayclassmethods
    {
        static void Main(string[] args)
        {
            int[] numbers1 = new int[5] { 15, 12, 13, 11, 16 };
            int[] numbers2 = new int[3];
            int cnt;
            int length, lowerbound, upperbound;

            Console.WriteLine("Original Array ");
            for (cnt = 0; cnt < 5; cnt++)
            {
                Console.WriteLine("" + numbers1[cnt]);
            }

            Console.WriteLine("Sorted array ");
            Array.Sort(numbers1); // Sorting of array.
            for (cnt = 0; cnt < 5; cnt++)
            {
                Console.WriteLine("" + numbers1[cnt]);
            }

            Console.WriteLine("Reversed array ");
            Array.Reverse(numbers1); // Reversing array
            for (cnt = 0; cnt < 5; cnt++)
            {
                Console.WriteLine("" + numbers1[cnt]);
            }

            length = numbers1.GetLength(0); // returning length from specific position
            Console.WriteLine("Length of array is {0}", length);
            lowerbound = numbers1.GetLowerBound(0);
            Console.WriteLine("Lower bound of the array is {0}", lowerbound);
            upperbound = numbers1.GetUpperBound(0);
            Console.WriteLine("Upper bound of the array is {0}", upperbound);

            Array.Copy(numbers1, numbers2, 3); // copying first three elements of array numbers1 to array numbers2
            Console.WriteLine("Elements of copied array are ");
            for (cnt = 0; cnt < 3; cnt++)
            {
                Console.WriteLine("" + numbers2[cnt]);
            }

            Array.Clear(numbers1, 0, 5); // Removing items from array.
            Console.WriteLine("Array after removing the elements");
            for (cnt = 0; cnt < 5; cnt++)
            {
                Console.WriteLine("" + numbers1[cnt]);
            }

            Console.ReadLine();
        }
    }
}
```

Input nil

### Output

```text
Original array
15
12
13
11
16

Sorted array
11
12
13
15
16

Reversed array
16
15
13
12
11

Length of array is 5

Lower bound of the array is 0

Upper bound of the array is 4

Elements of copied array are
16
15
13

Array after removing the elements
0
0
0
0
0
```

### 3. Using GetValue and SetValue methods of class Array

- The GetValue and SetValue methods of the Array class can be used to get and set values of an array's elements.

### Example

```csharp
// Illustration of GetValue and SetValue methods of class Array.

using System;

namespace arrayconcept
{
    class ArrayclassGetSet
    {
        static void Main(string[] args)
        {
            Array names = Array.CreateInstance(typeof(String), 2, 3);
            names.SetValue("Anil", 0, 0);
            names.SetValue("Ravi", 0, 1);
            names.SetValue("Ram", 0, 2);

            names.SetValue("Mita", 1, 0);
            names.SetValue("Seeta", 1, 1);
            names.SetValue("Rita", 1, 2);

            int total1 = names.GetLength(0);
            int total2 = names.GetLength(1);
            for (int cnt1 = 0; cnt1 < total1; cnt1++)
                for (int cnt2 = 0; cnt2 < total2; cnt2++)
                    Console.WriteLine(cnt1.ToString() + "," + cnt2.ToString() + ":" +
                        names.GetValue(cnt1, cnt2));
            Console.WriteLine();
        }
    }
}
```

Input nil

### Output

```text
0,0: Anil
0,1: Ravi
0,2: Ram
1,0: Mita
1,1: Seeta
1,2: Rita
```

### 4. Cloning an Array

- Clone method creates a shallow copy of an array.
- A shallow copy of an array copies only the elements of the array, whether they are reference types or value types, but it does not copy the objects that the references refer to.
- The references in the new array point to the same objects that the references in the original array point to.

Syntax for using Clone method

```csharp
int[] clonedArray = (int[])numArray.Clone();
```

## 6.3 ArrayList Class

### Concept

It represents an ordered collection of an object that can be indexed individually.

### Explanation

- 1. It is used as an alternative to an array. Unlike an array, items can be added or removed from a list at a specified position using an **index**, and the array resizes itself automatically.
- 2. This collection dynamically resizes. It grows in capacity as elements are added (if space is needed). **It holds objects.** It stores elements of type object; casting is needed.
- 3. It supports operations like adding, searching and sorting items in the list.

### 4. Properties of ArrayList Class

Commonly used **properties** of the **ArrayList** class are,

| Property | Description |
|---|---|
| Capacity | Gets or sets the number of elements that the ArrayList may contain. |
| Count | Gets the number of elements actually contained in the ArrayList. |
| IsFixedSize | Gets a boolean value indicating whether the ArrayList has a fixed size. |
| IsReadOnly | Gets a boolean value indicating whether the ArrayList is read-only. |
| Item | Gets or sets the element at the specified index. |

### 5. Methods of ArrayList class

Commonly used **methods** of the **ArrayList** class are,

**Methods**

- 1. **public virtual int Add(object value);**
  Adds an object to the end of the ArrayList.
- 2. **public virtual void AddRange(ICollection c);**
  Adds the elements of an ICollection to the end of the ArrayList.
- 3. **public virtual void Clear();**
  Removes all elements from the ArrayList.
- 4. **public virtual bool Contains(object item);**
  Determines whether an element is in the ArrayList.
- 5. `public virtual ArrayList GetRange(int index, int count);`
  Returns an ArrayList which represents a subset of the elements in the source ArrayList.
- 6. `public virtual int IndexOf(object);`
  Returns the zero-based index of the first occurrence of a value in the ArrayList or in a portion of it.
- 7. `public virtual void Insert(int index, object value);`
  Inserts an element into the ArrayList at the specified index.
- 8. `public virtual void InsertRange(int index, ICollection c);`
  Inserts the elements of a collection into the ArrayList at the specified index.
- 9. `public virtual void Remove(object obj);`
  Removes the first occurrence of a specific object from the ArrayList.
- 10. `public virtual void RemoveAt(int index);`
  Removes the element at the specified index of the ArrayList.
- 11. `public virtual void RemoveRange(int index, int count);`
  Removes a range of elements from the ArrayList.
- 12. `public virtual void Reverse();`
  Reverses the order of the elements in the ArrayList.
- 13. `public virtual void SetRange(int index, ICollection c);`
  Copies the elements of a collection over a range of elements in the ArrayList.
- 14. `public virtual void Sort();`
  Sorts the elements in the ArrayList.
- 15. `public virtual void TrimToSize();`
  Sets the capacity to the actual number of elements in the ArrayList.

### Example

```csharp
// illustration of ArrayList class
using System;
using System.Collections;

namespace CollectionDemo
{
    class UseArrayList
    {
        static void Main(string[] args)
        {
            ArrayList arlist = new ArrayList();
```
