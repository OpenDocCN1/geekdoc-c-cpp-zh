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

# Memory Management and the GC Class

The GC class encapsulates the garbage-collection facility. The methods defined by GC are shown in Table 21-15. It defines the read-only property shown here:

```
public static int MaxGeneration { get; }
```

MaxGeneration contains the maximum generation number available to the system. A generation number indicates the age of an allocation. Newer allocations have a lower number than older ones. Generation numbers help improve the efficiency of the garbage collector.

For most applications, you will not use any of the capabilities of GC. However, in specialized cases, they can be very useful. For example, you might want to use Collect() to force garbage collection to occur at a time of your choosing. Normally, garbage collection occurs at times unspecified by your program. Since garbage collection takes time, you might not want it to occur during some time-critical task, or you might want to take advantage of idle time to perform garbage collection and other types of “housekeeping” chores.