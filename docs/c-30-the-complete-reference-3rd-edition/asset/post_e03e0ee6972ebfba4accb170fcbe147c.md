
```
else
    Console.WriteLine("nums contains no negative values.");
}
}
```

The output is shown here:

```
Contents of nums: 1 4 -1 5 -9
nums contains a negative value.
First negative value is : -1
```

In the program, the method passed to Exists() and Find() for the predicate is IsNeg(). Notice that IsNeg() is declared like this:

```
static bool IsNeg(int v) {
```

The methods Exists() and Find() will automatically pass the elements of the array (in sequence) to v. Thus, each time IsNeg() is called, v will contain the next element in the array.

## Using an Action

The Action delegate is used by Array.ForEach() to perform an action on each element of an array. There are various forms of Action, each taking a different number of type parameters. The one used here is

```
public delegate void Action<T>(T obj)
```

The object to be acted upon is passed in obj. When used with ForEach(), each element of the array is passed to obj in turn. Thus, through the use of ForEach() and Action, you can, in a single statement, perform an operation over an entire array.

The following program demonstrates both ForEach() and Action. It first creates an array of MyClass objects, then uses the method Show() to display the values. Next, it uses Neg() to negate the values. Finally, it uses Show() again to display the negated values. These operations all occur through calls to ForEach().

// Demonstrate an Action.

using System;

class MyClass {
    public int i;

    public MyClass(int x) { i = x; }
}

class ActionDemo {

    // An Action method.
    // It displays the value it is passed.
    static void Show(MyClass o) {
        Console.Write(o.i + " ");
    }

    // Another Action method.
    // It negates the value it is passed.
static void Neg(MyClass o) {
    o.i = -o.i;
}

static void Main() {
    MyClass[] nums = new MyClass[5];

    nums[0] = new MyClass(5);
    nums[1] = new MyClass(2);
    nums[2] = new MyClass(3);
    nums[3] = new MyClass(4);
    nums[4] = new MyClass(1);

    Console.Write("Contents of nums: ");

    // Use action to show the values.
    Array.ForEach(nums, ActionDemo.Show);

    Console.WriteLine();

    // Use action to negate the values.
    Array.ForEach(nums, ActionDemo.Neg);

    Console.Write("Contents of nums negated: ");

    // Use action to show the values again.
    Array.ForEach(nums, ActionDemo.Show);

    Console.WriteLine();
}
```

The output is shown here:

Contents of nums: 5 2 3 4 1
Contents of nums negated: -5 -2 -3 -4 -1

## BitConverter

In programming one often needs to convert a built-in data type into an array of bytes. For example, some hardware device might require an integer value, but that value must be sent one byte at a time. The reverse situation also frequently occurs. Sometimes data will be received as an ordered sequence of bytes that needs to be converted into one of the built-in types. For example, a device might output integers, sent as a stream of bytes. Whatever your conversion needs, .NET provides the BitConverter class to meet them.

BitConverter is a static class. It contains the methods shown in Table 21-13. It defines the following field:

```
public static readonly bool IsLittleEndian
```

This field is true if the current environment stores a word with the least significant byte first and the most significant byte last. This is called “little-endian” format. IsLittleEndian is false if the current environment stores a word with the most significant byte first and the least significant byte last. This is called “big-endian” format. Intel Pentium-based machines use little-endian format.

| Method | Meaning |
| --- | --- |
| public static string ToString(byte[ ] a) | Converts the bytes in a into a string. The string contains the hexadecimal values associated with the bytes, separated by hyphens. |
| public static string ToString(byte[ ] a, int start) | Converts the bytes in a, beginning at a[start], into a string. The string contains the hexadecimal values associated with the bytes, separated by hyphens. |
| public static string ToString(byte[ ] a, int start, int count) | Converts the bytes in a, beginning at a[start] and running for count bytes, into a string. The string contains the hexadecimal values associated with the bytes, separated by hyphens. |
| public static ushort ToUInt16(byte[ ] a, int start) | Converts two bytes starting at a[start] into its ushort equivalent and returns the result. |
| public static uint ToUInt32(byte[ ] a, int start) | Converts four bytes starting at a[start] into its uint equivalent and returns the result. |
| public static ulong ToUInt64(byte[ ] a, int start) | Converts eight bytes starting at a[start] into its ulong equivalent and returns the result. |

**TABLE 21-13** Methods Defined by BitConverter (continued)

## Generating Random Numbers with Random

To generate a sequence of pseudorandom numbers, you will use the Random class. Sequences of random numbers are useful in a variety of situations, including simulations and modeling. The starting point of the sequence is determined by a seed value, which can be automatically provided by Random or explicitly specified.

Random defines these two constructors:

```
```csharp
public Random()
public Random(int seed)
```
```

The first version creates a Random object that uses the system time to compute the seed value. The second uses the value of seed as the seed value.

Random defines the methods shown in Table 21-14.
Here is a program that demonstrates Random by creating a pair of computerized dice:

```
```csharp
// An automated pair of dice.

using System;

class RandDice {
    static void Main() {
        Random ran = new Random();

        Console.Write(ran.Next(1, 7) + " ");
        Console.WriteLine(ran.Next(1, 7));
    }
}
```
```

| Method | Meaning |
|---|---|
| public virtual int Next() | Returns the next random integer, which will be between 0 and Int32.MaxValue-1, inclusive. |
| public virtual int Next(int upperBound) | Returns the next random integer that is between 0 and upperBound-1, inclusive. |
| public virtual int Next(int lowerBound, int upperBound) | Returns the next random integer that is between lowerBound and upperBound-1, inclusive. |
| public virtual void NextBytes(byte[] buf) | Fills buf with a sequence of random integers. Each byte in the array will be between 0 and Byte.MaxValue-1, inclusive. |
| public virtual double NextDouble() | Returns the next random value from the sequence represented as a floating-point number that is greater than or equal to 0.0 and less than 1.0. |
| protected virtual double Sample() | Returns the next random value from the sequence represented as a floating-point number that is greater than or equal to 0.0 and less than 1.0. To create a skewed or specialized distribution, override this method in a derived class. |

TABLE 21-14 Methods Defined by Random

Here are three sample runs:

```
5 2
4 4
1 6
```

The program works by first creating a Random object. Then it requests the two random values, each between 1 and 6, inclusive.

## Memory Management and the GC Class

The GC class encapsulates the garbage-collection facility. The methods defined by GC are shown in Table 21-15. It defines the read-only property shown here:

```
public static int MaxGeneration { get; }
```

MaxGeneration contains the maximum generation number available to the system. A generation number indicates the age of an allocation. Newer allocations have a lower number than older ones. Generation numbers help improve the efficiency of the garbage collector.

For most applications, you will not use any of the capabilities of GC. However, in specialized cases, they can be very useful. For example, you might want to use Collect() to force garbage collection to occur at a time of your choosing. Normally, garbage collection occurs at times unspecified by your program. Since garbage collection takes time, you might not want it to occur during some time-critical task, or you might want to take advantage of idle time to perform garbage collection and other types of “housekeeping” chores.
