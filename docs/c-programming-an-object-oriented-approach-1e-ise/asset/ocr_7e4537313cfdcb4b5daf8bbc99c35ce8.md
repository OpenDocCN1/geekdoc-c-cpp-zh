# **Program 3.19** Testing overflow and underflow in signed integers (Continued)

```
```cpp
22    return 0;
23  }
```
```

```
```text
Run:
The value of maximum signed int: 2147483647
The value of minimum signed int: −2147483648
The value of num1 + 1 after overflow: −2147483648
The value of num2 − 1 after underflow: 2147483647
```
```

![](bbox=[0.264, 0.284, 0.812, 0.363])

# ### 3.4.2 Overflow and Underflow in Floating-Point Values

We also have overflow and underflow in floating-point values; however, there are two differences here. First, all floating-point values are signed. Second, there is no wrapping when overflow and underflow occurs; instead we have *sinking*. Overflow results in sinking to +infinity; underflow results in sinking to −infinity. Figure 3.10 shows the concept.

Note that we have two max values and two min values. The min values define the small numbers nearest zero. The positive max and negative max values may create positive or negative infinity when increased or decreased, respectively. Program 3.20 initializes num1 and num2 to positive max and negative max values and then multiplies each number by 1000.00 to make the values overflow to +inf and −inf. Since positive maximum and negative maximum values are system dependent, we use a library function in lines 11 and 12 to instigate them.

# **Program 3.20** Overflow and underflow in doubles

```
```cpp
 1  /**************************************************************
 2  * A program to test overflow and underflow in doubles          *
 3  ***************************************************************/
 4  #include <iostream>
 5  #include <limits>
 6  using namespace std;
 7
 8  int main()
 9  {
10      // Find the positive and negative maximum double
11      double num1 = +numeric_limits<double>::max();
12      double num2 = −numeric_limits<double>::max();

(continued)
```
```