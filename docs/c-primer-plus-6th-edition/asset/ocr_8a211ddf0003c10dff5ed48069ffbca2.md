Pointers and the Free Store

# Value Ranges for Enumerations

Originally, the only valid values for an enumeration were those named in the declaration. However, C++ has expanded the list of valid values that can be assigned to an enumeration variable through the use of a type cast. Each enumeration has a range, and you can assign any integer in the range, even if it's not an enumeration value, by using a type cast to an enumeration variable. For example, suppose that bits and myflag are defined this way:

```
enum bits{one = 1, two = 2, four = 4, eight = 8};
bits myflag;
```

In this case, the following is valid:

```
myflag = bits(6); // valid, because 6 is in bits range
```

Here 6 is not one of the enumerations, but it lies in the range the enumerations define. The range is defined as follows. First, to find the upper limit, you take the largest value then subtract one; the result is the upper end of the range. (For example, the largest bigstep as previously defined, is 101. The smallest power of two greater than this is 128, so the upper end of the range is 127.) Next, to find the lower limit, you find the smallest enumeration value. If it is 0 or greater, the lower limit for the range is 0. If the smallest enumerator is negative, you use the same approach as finding the lower limit but in a minus sign. (For example, if the smallest enumerator is -6, the next power of two [times a minus sign] is -8, and the lower limit is -7).

The idea is that the compiler can choose how much space to use to hold an enumeration. It might use 1 byte or less for an enumeration with a small range and 4 bytes for an enumeration with type long values.

C++11 extends enumerations with a form called the scoped enumeration. Chapter 10 discusses this form briefly in the section “Class Scope."

# Pointers and the Free Store

The beginning of Chapter 3 mentions three fundamental properties of a computer program must keep track where it stores data. To save the book and tear of your thumbing back to that chapter, there are those properties again:

+   - Where the information is stored
- What value is kept there
- What kind of information is stored

You've used one strategy for accomplishing these ends: defining a simple variable. The declaration statement provides the type and a symbolic name for the value. It also causes the program to allocate memory for the value and to keep track of the location internally.