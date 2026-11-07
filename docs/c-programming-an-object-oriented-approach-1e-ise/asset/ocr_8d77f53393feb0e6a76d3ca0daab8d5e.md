# **Program 3.17**  Expressions with the same precedence (Continued)

```
```cpp
// Declaration and initialization
int x = 10;
int y = 20;
// Assignment
y += x *= 40;
// Printing values of x and y
cout << "Value of x: " << x << endl;
cout << "Value of y: " << y;
return 0;
}
```
```

```
Run:
Value of x: 400
Value of y: 420
```

![](bbox=[0.248, 0.358, 0.912, 0.483])

# 3.4 **OVERFLOW AND UNDERFLOW**

Before we write more programs, we discuss an issue all programmers need to understand: *overflow* and *underflow*. In real life, it is possible to write a very large number on paper. However, the memory allocation for data types in each computer system is limited. What happens if we try to store a number larger than the maximum value or smaller than the minimum value for a type? The result is **overflow or underflow**. C++ does not create an error message during the compilation, although it may give us a warning. What happens is that the result is not what we expected. The overflow and underflow behavior is different for integers and floating-point values (other types are promoted to either integer or floating-point, as we discussed before).

# 3.4.1 Overflow and Underflow in Integers

As we know, integer data types can be unsigned or signed. The overflow and underflow error is different for unsigned and signed integers. We discuss each case separately.

# Overflow and Underflow in Unsigned Integers

The range of an unsigned integer is from zero to the positive maximum value. We want to see what happens when we try to use a value larger than the maximum value or a value less than zero. In the first case, we have an overflow situation; in the second case, we have an underflow situation. Both are shown in Figure 3.8. In either case, the values are wrapped back