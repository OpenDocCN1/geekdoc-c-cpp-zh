
## Use Integers Rather Than Floating-Point Numbers

Cross-Reference For details on using integers and floating point, see Chapter 12, "Fundamental Data Types."

Integer addition and multiplication tend to be faster than floating point. Changing a loop index from a floating point to an integer, for example, can save time:

![](img/649c8eee28c38ca1e062691e45dc9883_661_0.png)

```
Visual Basic Example of a Loop That Uses a Time-Consuming Floating-Point Loop Index
Dim x As Single
For x = 0 to 99
    a( x ) = 0
Next
```

Contrast this with a similar Visual Basic loop that explicitly uses the integer type:

```
Visual Basic Example of a Loop That Uses a Timesaving Integer Loop Index
Dim i As Integer
For i = 0 to 99
    a( i ) = 0
Next
```

How much difference does it make? Here are the results for this Visual Basic code and for similar code in C++ and PHP:

| Language | Straight Time | Code-Tuned Time | Time Savings | Performance Ratio |
|---|---|---|---|---|
| C++ | 2.80 | 0.801 | 71% | 3.5:1 |
| PHP | 5.01 | 4.65 | 7% | 1:1 |
| Visual Basic | 6.84 | 0.280 | 96% | 25:1 |

## Use the Fewest Array Dimensions Possible

Cross-Reference For details on arrays, see Section 12.8, "Arrays."

Conventional wisdom maintains that multiple dimensions on arrays are expensive. If you can structure your data so that it’s in a one-dimensional array rather than a two-dimensional or three-dimensional array, you might be able to save some time. Suppose you have initialization code like this:

```
Java Example of a Standard, Two-Dimensional Array Initialization
for ( row = 0; row < numRows; row++ ) {
    for ( column = 0; column < numColumns; column++ ) {
        matrix[ row ][ column ] = 0;
    }
}
```

When this code is run with 50 rows and 20 columns, it takes twice as long with my current Java compiler as when the array is restructured so that it’s one-dimensional. Here’s how the revised code would look:

```
Java Example of a One-Dimensional Representation of an Array
```java
for ( entry = 0; entry < numRows * numColumns; entry++ ) {
    matrix[ entry ] = 0;
}
```
```

And here’s a summary of the results, with the addition of comparable results in several other languages:

| Language | Straight Time | Code-Tuned Time | Time Savings | Performance Ratio |
|---|---|---:|---:|---:|
| C++ | 8.75 | 7.82 | 11% | 1:1 |
| C# | 3.28 | 2.99 | 9% | 1:1 |
| **Java** | **7.78** | **4.14** | **47%** | **2:1** |
| PHP | 6.24 | 4.10 | 34% | 1.5:1 |
| Python | 3.31 | 2.23 | 32% | 1.5:1 |
| Visual Basic | 9.43 | 3.22 | 66% | 3:1 |

Note: Times for Python and PHP aren’t directly comparable to times for the other languages because they were run <1% as many iterations as the other languages.

The results of this optimization are excellent in Visual Basic and Java, good in PHP and Python, but mediocre in C++ and C#. Of course, the C# compiler’s unoptimized time was easily the best of the group, so you can’t be too hard on it.

This wide range of results again shows the hazard of following any code-tuning advice blindly. You can never be sure until you try the advice in your specific circumstances.

## Minimize Array References

In addition to minimizing accesses to doubly or triply dimensioned arrays, it’s often advantageous to minimize array accesses, period. A loop that repeatedly uses one element of an array is a good candidate for the application of this technique. Here’s an example of an unnecessary array access:

```
C++ Example of Unnecessarily Referencing an Array Inside a Loop
```cpp
for ( discountType = 0; discountType < typeCount; discountType++ ) {
    for ( discountLevel = 0; discountLevel < levelCount; discountLevel++ ) {
        rate[ discountLevel ] = rate[ discountLevel ] * discount[ discountType ];
    }
}
```
```

## Independent, Parallel Index Structure

Sometimes it's more efficient to manipulate an index to a data type than it is to manipulate the data type itself. If the items in the data type are big or hard to move (on disk, perhaps), sorting and searching index references is faster than working with the data directly. If each data item is large, you can create an auxiliary structure that consists of key values and pointers to the detailed information. If the difference in size between the data-structure item and the auxiliary-structure item is great enough, sometimes you can store the key item in memory even when the data item has to be stored externally. All searching and sorting is done in memory, and you have to access the disk only once, when you know the exact location of the item you want.

## Use Caching

Caching means saving a few values in such a way that you can retrieve the most commonly used values more easily than the less commonly used values. If a program randomly reads records from a disk, for example, a routine might use a cache to save the records read most frequently. When the routine receives a request for a record, it checks the cache to see whether it has the record. If it does, the record is returned directly from memory rather than from disk.

In addition to caching records on disk, you can apply caching in other areas. In a Microsoft Windows font-proofing program, the performance bottleneck was in retrieving the width of each character as it was displayed. Caching the most recently used character width roughly doubled the display speed.

You can cache the results of time-consuming computations too—especially if the parameters to the calculation are simple. Suppose, for example, that you need to compute the length of the hypotenuse of a right triangle, given the lengths of the other two sides. The straightforward implementation of the routine would look like this:

## Java Example of a Routine That's Conducive to Caching

```
double Hypotenuse(
    double sideA,
    double sideB
) {
    return Math.sqrt( ( sideA * sideA ) + ( sideB * sideB ) );
}
```

If you know that the same values tend to be requested repeatedly, you can cache values this way:

## Java Example of Caching to Avoid an Expensive Computation

```
private double cachedHypotenuse = 0;
private double cachedSideA = 0;
private double cachedSideB = 0;

public double Hypotenuse(
    double sideA,
    double sideB
) {
    // check to see if the triangle is already in the cache
    if ( ( sideA == cachedSideA ) && ( sideB == cachedSideB ) ) {
        return cachedHypotenuse;
    }
    // compute new hypotenuse and cache it
    cachedHypotenuse = Math.sqrt( ( sideA * sideA ) + ( sideB * sideB ) );
    cachedSideA = sideA;
    cachedSideB = sideB;
    return cachedHypotenuse;
}
```

The second version of the routine is more complicated than the first and takes up more space, so speed has to be at a premium to justify it. Many caching schemes cache more than one element, so they have even more overhead. Here’s the speed difference between these two versions:

| Language | Straight Time | Code-Tuned Time | Time Savings | Performance Ratio |
|---|---|---|---|---|
| C++ | 4.06 | 1.05 | 74% | 4:1 |
| Java | 2.54 | 1.40 | 45% | 2:1 |
| Python | 8.16 | 4.17 | 49% | 2:1 |
| Visual Basic | 24.0 | 12.9 | 47% | 2:1 |
| Note: The results shown assume that the cache is hit twice for each time it's set. |

The success of the cache depends on the relative costs of accessing a cached element, creating an uncached element, and saving a new element in the cache. Success also depends on how often the cached information is requested. In some cases, success might also depend on caching done by the hardware. Generally, the more it costs to generate a new element and the more times the same information is requested, the more valuable a cache is. The cheaper it is to access a cached element and save new elements in the cache, the more valuable a cache is. As with other optimization techniques, caching adds complexity and tends to be error-prone.

## 26.4 Expressions

Cross-Reference For more information on expressions, see Section 19.1, "Boolean Expressions."

Much of the work in a program is done inside mathematical or logical expressions. Complicated expressions tend to be expensive, so this section looks at ways to make them cheaper.

## Exploit Algebraic Identities

You can use algebraic identities to replace costly operations with cheaper ones. For example, the following expressions are logically equivalent:

```
not a and not b
not (a or b)
```

If you choose the second expression instead of the first, you can save a not operation.

Although the savings from avoiding a single not operation are probably inconsequential, the general principle is powerful. Jon Bentley describes a program that tested whether sqrt(x) < sqrt(y) (1982). Since sqrt(x) is less than sqrt(y) only when x is less than y, you can replace the first test with x < y. Given the cost of the sqrt() routine, you’d expect the savings to be dramatic, and they are. Here are the results:

| Language | Straight Time | Code-Tuned Time | Time Savings | Performance Ratio |
|---|---|---|---|---|
| C++ | 7.43 | 0.010 | 99.9% | 750:1 |
| Visual Basic | 4.59 | 0.220 | 95% | 20:1 |
| Python | 4.21 | 0.401 | 90% | 10:1 |

## Use Strength Reduction

As mentioned earlier, strength reduction means replacing an expensive operation with a cheaper one. Here are some possible substitutions:

- Replace multiplication with addition.
- Replace exponentiation with multiplication.
- Replace trigonometric routines with their trigonometric identities.
- Replace longlong integers with longs or ints (but watch for performance issues associated with using native-length vs. non-native-length integers)
- Replace floating-point numbers with fixed-point numbers or integers.
- Replace double-precision floating points with single-precision numbers.
- Replace integer multiplication-by-two and division-by-two with shift operations.
