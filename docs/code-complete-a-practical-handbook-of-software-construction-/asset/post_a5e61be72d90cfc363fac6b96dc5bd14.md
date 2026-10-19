
Performance is an issue, find out how expensive your system calls are. If they’re expensive, consider these options:

- Write your own services. Sometimes you need only a small part of the functionality offered by a system routine and can build your own from lower-level system routines. Writing your own replacement gives you something that’s faster, smaller, and better suited to your needs.
- Avoid going to the system.
- Work with the system vendor to make the call faster. Most vendors want to improve their products and are glad to learn about parts of their systems with weak performance. (They might seem a little grouchy about it at first, but they really are interested.)

In the code-tuning effort I described in “When to Tune” in Section 25.2, the program used an *AppTime* class that was derived from a commercially available *BaseTime* class. (These names have been changed to protect the guilty.) The *AppTime* object was the most common object in this application, and we instantiated tens of thousands of *AppTime* objects. After several months, we discovered that *BaseTime* was initializing itself to the system time in its constructor. For our purposes, the system time was irrelevant, which meant we were needlessly generating thousands of system-level calls. Simply overriding *BaseTime*’s constructor and initializing the *time* field to 0 instead of to the system time gave us about as much performance improvement as all the other changes we made put together.

*Interpreted languages* Interpreted languages tend to exact significant performance penalties because they must process each programming-language instruction before creating and executing machine code. In the performance benchmarking I performed for this chapter and Chapter 26, I observed the approximate relationships in performance among different languages that are described in Table 25-1.

## Table 25-1 Relative Execution Time of Programming Languages

| Language | Type of Language | Execution Time Relative to C++ |
|---|---|---|
| C++ | Compiled | 1:1 |
| Visual Basic | Compiled | 1:1 |
| C# | Compiled | 1:1 |
| Java | Byte code | 1.5:1 |
| PHP | Interpreted | >100:1 |
| Python | Interpreted | >100:1 |

As you can see, C++, Visual Basic, and C# are all comparable. Java is close but tends to be slower than the other languages. PHP and Python are interpreted languages, and code in those languages tended to run a factor of 100 or more slower than code in C++, Visual Basic, C#, and Java. The general numbers presented in this table must be viewed cautiously. For any particular piece of code, C++, Visual Basic, C#, or Java

might be twice as fast or half as fast as the other languages. (You can see this for yourself in the detailed examples in Chapter 26.)

***Errors***  A final source of performance problems is errors in the code. Errors can include leaving debugging code turned on (such as logging trace information to a file), forgetting to deallocate memory, improperly designing database tables, polling nonexistent devices until they time out, and so on.

A version 1.0 application I worked on had a particular operation that was much slower than other similar operations. A great deal of project mythology grew up to explain the slowness of this operation. We released version 1.0 without ever fully understanding why this particular operation was so slow. While working on the version 1.1 release, however, I discovered that the database table used by the operation wasn’t indexed! Simply indexing the table improved performance by a factor of 30 for some operations. Defining an index on a commonly used table is not optimization; it’s just good programming practice.

## Relative Performance Costs of Common Operations

Although you can’t count on some operations being more expensive than others without measuring them, certain operations tend to be more expensive. When you look for the molasses in your program, use Table 25-2 to help make some initial guesses about the sticky parts of your program.

**Table 25-2  Costs of Common Operations**

| Operation | Example | C++ | Java |
|---|---|---:|---:|
| *Baseline (integer assignment)* | *i = j* | *1* | *1* |
| **Routine Calls** |  |  |  |
| Call routine with no parameters | *foo()* | 1 | n/a |
| Call private routine with no parameters | *this.foo()* | 1 | 0.5 |
| Call private routine with 1 parameter | *this.foo(i)* | 1.5 | 0.5 |
| Call private routine with 2 parameters | *this.foo(i,j)* | 2 | 0.5 |
| Object routine call | *bar.foo()* | 2 | 1 |
| Derived routine call | *derivedBar.foo()* | 2 | 1 |
| Polymorphic routine call | *abstractBar.foo()* | 2.5 | 2 |
| **Object References** |  |  |  |
| Level 1 object dereference | *i = obj.num* | 1 | 1 |
| Level 2 object dereference | *i = obj1.obj2.num* | 1 | 1 |
| Each additional dereference | *i = obj1.obj2.obj3...* | not measurable | not measurable |

## Table 25-2 Costs of Common Operations

| Operation | Example | Relative Time Consumed |  |
|---|---|---|---|
|  |  | C++ | Java |
| **Integer Operations** |  |  |  |
| Integer assignment (local) | i = j | 1 | 1 |
| Integer assignment (inherited) | i = j | 1 | 1 |
| Integer addition | i = j + k | 1 | 1 |
| Integer subtraction | i = j - k | 1 | 1 |
| Integer multiplication | i = j * k | 1 | 1 |
| Integer division | i = j \ k | 5 | 1.5 |
| **Floating-Point Operations** |  |  |  |
| Floating-point assignment | x = y | 1 | 1 |
| Floating-point addition | x = y + z | 1 | 1 |
| Floating-point subtraction | x = y - z | 1 | 1 |
| Floating-point multiplication | x = y * z | 1 | 1 |
| Floating-point division | x = y / z | 4 | 1 |
| **Transcendental Functions** |  |  |  |
| Floating-point square root | x = sqrt(y) | 15 | 4 |
| Floating-point sine | x = sin(y) | 25 | 20 |
| Floating-point logarithm | x = log(y) | 25 | 20 |
| Floating-point e^y | x = exp(y) | 50 | 20 |
| **Arrays** |  |  |  |
| Access integer array with constant subscript | i = a[5] | 1 | 1 |
| Access integer array with variable subscript | i = a[j] | 1 | 1 |
| Access two-dimensional integer array with constant subscripts | i = a[3, 5] | 1 | 1 |
| Access two-dimensional integer array with variable subscripts | i = a[j, k] | 1 | 1 |
| Access floating-point array with constant subscript | x = z[5] | 1 | 1 |
| Access floating-point array with integer-variable subscript | x = z[j] | 1 | 1 |
| Access two-dimensional, floating-point array with constant subscripts | x = z[3, 5] | 1 | 1 |
| Access two-dimensional, floating-point array with integer-variable subscripts | x = z[j, k] | 1 | 1 |
| Note: Measurements in this table are highly sensitive to local machine environment, compiler optimizations, and code generated by specific compilers. Measurements between C++ and Java are not directly comparable. |  |  |  |

The relative performance of these operations has changed significantly since the first edition of *Code Complete*, so if you’re approaching code tuning with 10-year-old ideas about performance, you might need to update your thinking.

Most of the common operations are about the same price—routine calls, assignments, integer arithmetic, and floating-point arithmetic are all roughly equal. Transcendental math functions are extremely expensive. Polymorphic routine calls are a bit more expensive than other kinds of routine calls.

Table 25-2, or a similar one that you make, is the key that unlocks all the speed improvements described in Chapter 26. In every case, improving speed comes from replacing an expensive operation with a cheaper one. Chapter 26 provides examples of how to do so.

## 25.4 Measurement

Because small parts of a program usually consume a disproportionate share of the run time, measure your code to find the hot spots. Once you’ve found the hot spots and optimized them, measure the code again to assess how much you’ve improved it. Many aspects of performance are counterintuitive. The earlier case in this chapter, in which 10 lines of code were significantly faster and smaller than one line, is one example of the ways that code can surprise you.

![](img/649c8eee28c38ca1e062691e45dc9883_639_0.png)

Experience doesn’t help much with optimization either. A person’s experience might have come from an old machine, language, or compiler—when any of those things changes, all bets are off. You can never be sure about the effect of an optimization until you measure the effect.

Many years ago now I wrote a program that summed the elements in a matrix. The original code looked like this:

**C++ Example of Straightforward Code to Sum the Elements in a Matrix**

```cpp
sum = 0;
for ( row = 0; row < rowCount; row++ ) {
    for ( column = 0; column < columnCount; column++ ) {
        sum = sum + matrix[ row ][ column ];
    }
}
```

This code was straightforward, but performance of the matrix-summation routine was critical, and I knew that all the array accesses and loop tests had to be expensive. I knew from computer-science classes that every time the code accessed a two-dimensional array, it performed expensive multiplications and additions. For a 100-by-100 matrix, that totaled 10,000 multiplications and additions, plus the loop overhead. By
