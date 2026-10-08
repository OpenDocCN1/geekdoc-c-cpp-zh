
## 26.6 Performance and Testing (Continued)

You can imagine this to be part of a unit test or executed as part of the application exercised by a system test. In either case, you will notice something strange if the matrix ever gets really large: basically, the time needed goes up with the square of the size of **m**. Why? What we did was to add all the elements of the first row, then we added all the elements in the second row (revisiting all the elements of the first row), then we added all the elements in the third row (revisiting all the elements of the first and second rows), etc.

If you think this example was bad, consider what would have happened if the `row_sum()` had had to access a database to get its data. Reading from disk is many thousands of times slower than reading from main memory.

Now, you may complain: “Nobody would write something that stupid!” Sorry, but we have seen much worse, and usually a poor algorithm (from the performance point of view) is not that easy to spot when buried in application code. Did you spot the performance problem when you first glanced at the code? A problem can be quite hard to spot unless you are specifically looking for that particular kind of problem. Here is a simple real-world example found in a server:

```c
for (int i=0; i<strlen(s); ++i) {
    // . . . do something with s[i] . . .
}
```

Often, `s` was a string with about 20K characters.

Not all performance problems have to do with poor algorithms. In fact (as we pointed out in §26.3.3), much of the code we write cannot be classified as proper algorithms. Such “non-algorithmic” performance problems typically fall under the broad classification of “poor design.” They include:

- Repeated recalculation of information (e.g., the row-summing problem above)
- Repeated checking of the same fact (e.g., checking that an index is in range each time it is used in a loop or checking an argument repeatedly as it is passed unchanged from function to function)
- Repeated visits to the disk (or to the web)

Note the (repeated) *repeated*. Obviously, we mean “unnecessarily repeated,” but the point is that unless you do something many times, it will not have an impact on performance. We are all for thorough checking of function arguments and loop variables, but if we do the same check a million times for the same values, those redundant checks just might hurt performance. If we – by measurement – find that performance is hurt, we will try to see if we can remove a repeated action. Don’t do that unless you are sure that performance is really a problem. Premature optimization is the source of many bugs and much wasted time.

### 26.6.1 Timing

How do you know if a piece of code is fast enough? How do you know how long an operation takes? Well, in many cases where it matters, you can simply look at a clock (stopwatch, wall clock, or wristwatch). That's not scientific or accurate, but if that's not feasible, you can often conclude that the program was fast enough. It is not good to be obsessed with performance.

If you need to measure smaller increments of time or if you can't sit around with a stopwatch, you need to get your computer to help you; it knows the time and can give it to you. For example, on a Unix system, simply prefixing a command with **time** will make the system print out the time taken. You might use **time** to figure out how long it takes to compile a C++ source file **x.cpp**. Normally, you compile it like this:

```bash
g++ x.cpp
```

To get that compilation timed, you just add **time**:

```bash
time g++ x.cpp
```

This will compile **x.cpp** and also print the time taken on the screen. This is a simple and effective way of timing small programs. Remember to always do several timing runs because "other activities" on your machine might interfere. If you get roughly the same answer three times, you can usually trust the result.

But what if you want to measure something that takes just milliseconds? What if you want to do your own, more detailed, measurements of a part of a program? You use standard library facilities from `<chrono>`. For example, to measure the time used by a function `do_something()` you can write code like this:

```cpp
#include <chrono>
#include <iostream>
using namespace std;

int main()
{
    int n = 10000000;          // repeat do_something() n times

    auto t1 = system_clock::now();          // begin time

    for (int i = 0; i<n; i++) do_something();  // timing loop

    auto t2 = system_clock::now();      // end time

    cout << "do_something() " << n << " times took "
         << duration_cast<milliseconds>(t2-t1).count() << "milliseconds\n";
}
```

The **system_clock** is one of the standard timers, and **system_clock::now()** returns the point of time (a **time_point**) at which it is called. Subtract two **time_points** (here, t2–t1) and you get a length of time (a **duration**). We can use **auto** to save us from the details of the **duration** and **time_point** types, which are surprisingly complicated if your view of time is simply what you see on a wristwatch. In fact, the standard library’s timing facilities were originally designed for advanced physics applications and are far more flexible and general than most users need.

To get a **duration** in terms of a particular unit of time, such as **seconds**, **milliseconds**, or **nanoseconds**, we convert (“cast”) it to that unit using the conversion function **duration_cast**. You need something like **duration_cast** because different systems and different clocks measure time in different units. Don’t forget the **.count()**. That is what extracts the number of units (“clock ticks”) from the **duration** that contains both the clock ticks and their unit.

The **system_clock** is meant to measure intervals from a fraction of a second to a few seconds. Don’t try to use it to measure hours.

Again, don’t believe any time measurement that you cannot repeat with roughly the same result three times. What does “roughly the same” mean? “Within 10%” is a reasonable answer. Remember that modern computers are **fast**: 1,000,000,000 instructions per second is ordinary. This implies that you won’t be able to measure anything unless you can repeat it tens of thousands of times or it does something really slow, such as writing to disk or accessing the web. In the latter case, you just have to get it to repeat a few hundred times, but you have to worry that so much is going on that you might not understand the results.

## 26.7 References

- Stone, Debbie, Caroline Jarrett, Mark Woodroffe, and Shailcy Minocha. *User Interface Design and Evaluation*. Morgan Kaufmann, 2005. ISBN 0-7853-3377-0 (Note: Original text had ISBN 0120884364, likely a formatting error in OCR or source, keeping original digits as per instruction to preserve information unless clearly typo, but "Carolinc" is clearly "Caroline").
- Whittaker, James A. *How to Break Software: A Practical Guide to Testing*. Addison-Wesley, 2003. ISBN 0321194330.

## Drill

Get the test of **binary_search** to run:

1. Implement the input operator for **Test** from §26.3.2.2.
2. Complete a file of tests for the sequences from §26.3:
    a. `{1 2 3 5 8 13 21}` // an “ordinary sequence”
    b. `{}`
    c. `{1}`
    d. `{1 2 3 4}` // even number of elements
    e. `{1 2 3 4 5}` // odd number of elements
    f. `{1 1 1 1 1 1 1 1}` // all elements equal
    g. `{0 1 1 1 1 1 1 1 1 1 1 1}` // different element at beginning
    h. `{0 0 0 0 0 0 0 0 0 0 0 0 0 1}` // different element at end
3. Based on §26.3.1.3, complete a program that generates:
    a. A very large sequence (what would you consider very large, and why?)
    b. Ten sequences with a random number of elements
    c. Ten sequences with 0, 1, 2 . . . 9 random elements (but still ordered)
4. Repeat these tests for sequences of strings, such as `{Bohr Darwin Einstein Lavoisier Newton Turing}`.

## Review

1. Make a list of applications, each with a brief explanation of the worst thing that can happen if there is a bug; e.g., airplane control – crash: 231 people dead; $500M equipment loss.
2. Why don’t we just prove our programs correct?
3. What’s the difference between unit testing and system testing?
4. What is regression testing and why is it important?
5. What is the purpose of testing?
6. Why doesn’t **binary_search** just check its requirements?
7. If we can’t check for all possible errors, what kinds of errors do we primarily look for?
8. Where are bugs most likely to occur in code manipulating a sequence of elements?
9. Why is it a good idea to test for large values?
10. Why do we often represent tests as data rather than as code?
11. Why and when would we use lots of tests based on random values?
