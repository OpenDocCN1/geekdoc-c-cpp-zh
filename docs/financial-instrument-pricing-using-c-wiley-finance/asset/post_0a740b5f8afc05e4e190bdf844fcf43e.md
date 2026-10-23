
```
// The integral value corresponding to the bits.
unsigned long value = bs.to_ulong();
string stringValue = bs.to_string();

cout << "Numeric value: " << value << ", String value: "
    << stringValue << endl;
```

### 10.3.3 Boost dynamic_bitset

This class is almost identical to std::bitset and it has an interface similar to that of std::bitset. There is, however, one major difference; in the current case we can create bitsets of dynamic length at run-time. This is achieved in the constructors of dynamic_bitset<Block, Allocator>. It has two template parameters:

- Block: the integer type in which the bits are stored (default is unsigned long).
- Allocator: the allocator type used for all internal memory management (default is std::allocator<Block>).

An example of use is:

```
#include <iostream>
#include <boost/dynamic_bitset.hpp>

using namespace std;

int main()
{
    boost::dynamic_bitset<unsigned int> x(4);  // All 0's by default.
    x[0] = 1;
    x[1] = 1;
    x[3] = 1;
    cout << x << endl; // '1011'.

    boost::dynamic_bitset<unsigned int> y(4);
    cout << y << endl;  // '0000'.
    y = x;
    cout << y << endl;  // '1011'.

    return 0;
}
```

The other member functions are the same as those for std::bitset.

### 10.3.4 Applications of Dynamic Bitsets

There are many applications in which dynamic bitsets can be used. In general, their use results in efficient and compact code. Some applications are:

- Creating efficient and compact data structures.
- Memory allocation managers.
- Huffman coding, Bloom filters.
- Information retrieval.
- Raster graphics when we model pixels and bitmaps.
- Genetic algorithms, especially when modelling *selection*, *crossover* and *mutation* operations.
- When implementing security and access control policies.
- It can be an alternative to, and improvement on, `std::vector<bool>`.

Discussion of these topics is outside the scope of this book. See Demming and Duffy (2012) for more examples.

## 10.4 CHRONO LIBRARY

The *chrono* library provides a means to represent points in time, time durations (for example, days, minutes, seconds or nanoseconds) and several kinds of clocks (for example, system clock and high-resolution clock). It is a precision-neutral library and it is an improvement (more portable) on previous attempts to create flexible and accurate libraries to measure time.

What do we mean by ‘time’? There are various definitions and perspectives:

- *Elapsed real time* (real time): the time taken from the start of a computer program to its end. It includes I/O time and other kinds of wait. Real time is the time measured by an ordinary clock.
- *CPU* (process) time: the amount of time that a CPU uses for processing the instructions of a computer program or of an operating system as opposed to measuring I/O operations. CPU time is usually measured in *clock ticks* or seconds. CPU time can further be divided into *user time*, which is the amount of time that the CPU was busy executing code in *user space* and *system time*, which is the amount of time that the CPU was busy executing code in *kernel space*. We can also measure CPU time as a percentage of CPU capacity and this is called *CPU usage*. In a multiprocessor machine the total CPU time is the sum of the CPU times consumed by all of the CPUs utilised by a computer program.
- *Wall-clock time* (wall time): the human perception of the passage of time from the start of a task to completion. It is the sum of CPU time, I/O time and the communication channel delay.
- *System time*: the computer system’s notion of the passing of time. It also includes the passing of days on the calendar.

We now discuss in some detail how the chrono library measures time. We first introduce the supporting class for fractional arithmetic.

### 10.4.1 Compile-Time Fractional Arithmetic with `std::ratio<>`

The class template `std::ratio<>` supports compile-time rational arithmetic. A rational number is a pair consisting of a *numerator* and a non-zero *denominator*, both of which must

Other operators are:

```
ratio_not_equal
ratio_less
ratio_less_equal
ratio_greater
ratio_greater_equal
```

Finally, the standard library supports SI (International System of Units) ratios (all in the namespace std):

```
typedef ratio<1, 1000000000000000000> atto;
typedef ratio<1, 1000000000000000> femto;
typedef ratio<1, 1000000000000> pico;
typedef ratio<1, 1000000000> nano;
typedef ratio<1, 1000000> micro;
typedef ratio<1, 1000> milli;
typedef ratio<1, 100> centi;
typedef ratio<1, 10> deci;
typedef ratio<10, 1> deca;
typedef ratio<100, 1> hecto;
typedef ratio<1000, 1> kilo;
typedef ratio<1000000, 1> mega;
typedef ratio<1000000000, 1> giga;
typedef ratio<1000000000000, 1> tera;
typedef ratio<1000000000000000, 1> peta;
typedef ratio<1000000000000000000, 1> exa;
```

Some examples are:

```
template <std::intmax_t Num, std::intmax_t Den>
    void print(const std::ratio<Num, Den>& r)
{
    std::cout << r.num << "/" << r.den << '\n';
}

// SI units
std::kilo myKilo; print(myKilo);        // 1000/1
std::milli myMilli; print(myMilli);     // 1/1000

std::nano myNano; print(myNano);        // 1/1'000'000'000
std::giga myGiga; print(myGiga);        // 1'000'000'000/1
```

The chrono library uses std::ratio<>.

### 10.4.2 Duration

A *duration* of time is defined as a number of ticks over a certain time unit. For example, 10 minutes is 10 ticks of a minute or 86,400 seconds, which is 86,400 ticks of a second (otherwise known as one day). Some initial examples of durations are:

```
namespace ch = std::chrono;

// 5 ticks of 1/10 second
ch::duration<int, std::ratio<1, 10>> d1(5);
// 4 ticks of 1/20 second
ch::duration<int, std::ratio<1, 20>> d2(4);
std::cout << d1.count() << ", " << d2.count() << '\n';  // 5,4
```

Other examples using SI units are:

```
// SI units
std::kilo myKilo; print(myKilo);          // 1000/1
std::milli myMilli; print(myMilli);        // 1/1000

std::nano myNano; print(myNano);          // 1/1'000'000'000
std::giga myGiga; print(myGiga);          // 1'000'000'000/1
```

Other helper predefined duration types are:

```
std::chrono::nanoseconds
    duration</*signed integer type of at least 64 bits*/, std::nano>
std::chrono::microseconds
    duration</*signed integer type of at least 55 bits*/, std::micro>
std::chrono::milliseconds
    duration</*signed integer type of at least 45 bits*/, std::milli>
std::chrono::seconds
    duration</*signed integer type of at least 35 bits*/>
std::chrono::minutes
    duration</*signed integer type of at least 29 bits*/, std::ratio<60>>
std::chrono::hours
    duration</*signed integer type of at least 23 bits*/, std::ratio<3600>>
```

Using these types is more user-friendly than using raw fractions:

```
// Duration typedefs
ch::duration<double, std::milli> mySec(30);
std::cout << mySec.count() << '\n';          // 30

std::chrono::hours h(1);                    // one hour
std::chrono::milliseconds ms{ 3 };          // 3 milliseconds
std::chrono::duration<int, std::kilo> ks(3);  // 3000 seconds
```

We now come to the topic of arithmetic duration operations and properties:

- Sum, difference, product and division of two durations using operator notation.
- Add and subtract ticks and other durations.
- Compare two durations (==, <, <=, >, >=).
- Convert a duration into another type.
- Minimum and maximum possible durations for a type.

Some typical examples are:

```
// Operations
ch::seconds s(100);                                      // 100 seconds
ch::milliseconds mills(10);      // 10 milliseconds
auto diff = s - mills;
std::cout << diff.count() << '\n';                       // 99990
diff++;
std::cout << diff.count() << '\n';                      // 99991
auto sum = s + mills;
std::cout << sum.count() << '\n';                       // 100010
std::cout << std::boolalpha << (sum == diff) << '\n';   // false

ch::hours aDay(24);
ch::milliseconds zeroMS(0);
zeroMS += aDay;
std::cout << zeroMS.count() << '\n';                    // 86,400,000
```

Finally, duration_cast converts a duration to a duration of a different type. Computation is done in the widest type available and converted to the final result. Here is an example of converting from milliseconds to seconds and between different ratios:

```
// Duration casting
ch::duration<double, std::milli> dA(3000);              // 3000 ms
auto dB = ch::duration_cast<ch::seconds>(dA);
std::cout << dB.count() << '\n';                        // 3

ch::duration<int, std::ratio<1, 10>> dC(5);
std::cout << dC.count() << '\n';                        // 5
auto dD = ch::duration_cast<ch::duration<int, std::ratio<1, 20>>> (dC);
std::cout << dD.count() << '\n';                        // 10
auto dE = ch::duration_cast<ch::duration<int, std::ratio<1, 2>>> (dC);
std::cout << dE.count() << '\n';                        // 1
```

### 10.4.3 Timepoint and Clocks

A timepoint represents a specific point in time. A clock defines an epoch (starting point of the clock). A timepoint associates a positive or negative duration with a given clock. For example, if the epoch is January 1, 1970 for a duration of 10 days then the corresponding timepoint will be January 11, 1970.
