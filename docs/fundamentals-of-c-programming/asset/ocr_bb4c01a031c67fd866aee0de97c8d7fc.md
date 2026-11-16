# Figure 4.2 Range of ints vs. range of doubles

![](bbox=[0.223, 0.163, 0.775, 0.283])

Since a `char` is stored internally as a number (see Section 3.8), we can perform arithmetic on characters. We will have little need to apply mathematics to characters, but sometimes it is useful. As an example, the lower-case letters of the alphabet a-z occupy ASCII values 97–123, with a = 97, b = 98, etc. The upper-case letters A-Z are coded as 65–91, with A = 65, B = 66, etc. To capitalize any lower-case letter, you need only subtract 32, as in

```
```cpp
char lower = 'd', upper = lower - 32;
std::cout << upper << '\n';
```
```

This section of code would print D. If you do not remember the offset of 32 between upper- and lower-case letter, you can compute it with the letters themselves:

```
```cpp
upper = lower - ( 'a' - 'A' );
```
```

In this case, if Lower has been assigned any value in the range 'a' to 'z', the statement will assign to upper the capitalized version of Lower. On the other hand, if Lower's value is outside of that range, upper will not receive a meaningful value.

# ## 4.2 Mixed Type Expressions

Expressions may contain mixed elements; for example, the following program fragment

```
```cpp
int x = 4;
double y = 10.2, sum;
sum = x + y;
```
```

adds an `int` to a `double`, and the result is being assigned to a `double`. How is the arithmetic performed?

As shown in Figure 4.2, the range of `int`s falls completely within the range of `double`s; thus, any `int` value can represented by a `double`. The `int` 4 also can be expressed as the `double` 4.0. In fact, since the largest `int` on most systems is 2,147,483,647, the minimum 15 digits of `double` precision are more than adequate to represent all integers exactly. This means that any `int` value can be represented by a `double`. The converse is not true, however. 2,200,000,000 can be represented by a `double` but it is too big for the `int` type. We say that the `double` type is **wider** than the `int` type and that the `int` type is **narrower** than the `double` type.

It would be reasonable, then, to be able to assign `int` values to `double` variables. The process is called **widening**, and it is always safe to widen an `int` to a `double`. The following code fragment