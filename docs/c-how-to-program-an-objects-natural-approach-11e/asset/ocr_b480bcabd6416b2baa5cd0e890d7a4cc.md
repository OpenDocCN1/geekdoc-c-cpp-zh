```
```cpp
std::cout << std::format("x: {}\ny: {}\nz: {}\n",
    x.toString(), y.toString(), z.toString());

x = y + z;
std::cout << std::format("{} = {} + {}\n",
    x.toString(), y.toString(), z.toString());

x = y - z;
std::cout << std::format("{} = {} - {}\n",
    x.toString(), y.toString(), z.toString());
}
```
```

```
```
x: (0.00, 0.00)
y: (4.30, 8.20)
z: (3.30, 1.10)

(7.60, 9.30) = (4.30, 8.20) + (3.30, 1.10)

(1.00, 7.10) = (4.30, 8.20) - (3.30, 1.10)
```
```

*Fig. 11.11* | Complex class test program. (Part 2 of 2.)

# ### 11.4 (HugeInteger Class)

A machine with 32-bit integers can represent integers in the range of approximately −2 billion to +2 billion. This fixed-size restriction is rarely troublesome, but there are applications in which you would like to be able to use a much wider range of integers. This is what C++ was built to do, namely, create powerful new data types. In Chapter 3’s Objects-Natural Case Study, we introduced super-sized integers via objects of the Boost Multiprecision library’s powerful cpp_int class. In this exercise, you’ll enhance the custom class HugeInteger shown in Figs. 11.12–11.14. This exercise is designed to give you practice overloading class operators. For real-world applications, rather than reinventing the wheel, you should use the Boost Multiprecision library or another similar library for super-sized integers.

Study the HugeInteger class carefully, then respond to the following:

+   a) Describe precisely how it operates.
+   b) What restrictions does the class have?
+   c) Overload the * multiplication operator.
+   d) Overload the / division operator.
+   e) Overload all the rational and equality operators.

> *[Note: We do not show an assignment operator or copy constructor for class HugeInteger, because the assignment operator and copy constructor provided by the compiler are capable of copying the entire array data member properly.]*