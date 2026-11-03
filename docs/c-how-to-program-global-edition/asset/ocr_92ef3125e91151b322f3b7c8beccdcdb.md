127 parameters to a function. For more information on other limits set by the C99 Standard, see C99 Standard Section 5.2.4.1.

# E.8.2 The restrict Keyword

[This section can be read after Section 7.5.]

The keyword restrict is used to declare restricted pointers. We declare a restricted pointer when that pointer should have exclusive access to a region of memory. Objects accessed through a restricted pointer cannot be accessed by other pointers except when the value of those pointers was derived from the value of the restricted pointer. We can declare a restricted pointer to an int as:

```
int *restrict ptr;
```

Restricted pointers allow the compiler to optimize the way the program accesses memory. For example, the standard library function memcpy is defined in the C99 standard as follows:

```
void *memcpy(void *restrict s1, const void *restrict s2, size_t n);
```

The specification of the memcpy function states that it should not be used to copy between overlapping regions of memory. Using restricted pointers allows the compiler to see that requirement, and it can optimize the copy by copying multiple bytes at a time, which is more efficient. Incorrectly declaring a pointer as restricted when another pointer points to the same region of memory can result in undefined behavior. [For more information, see C99 Standard Section 6.7.3.1.]

# E.8.3 Reliable Integer Division

[This section can be read after Section 2.5.]

In compilers prior to C99, the behavior of integer division varies across implementations. Some implementations round a negative quotient toward negative infinity, while others round toward zero. When one of the integer operands is negative, this can result in different answers. Consider dividing −28 by 5. The exact answer is −5.6. If we round the quotient toward zero, we get the integer result of −5. If we round −5.6 toward negative infinity, we get an integer result of −6. C99 removes the ambiguity and always performs integer division (and integer modulus) by rounding the quotient toward zero. This makes integer division reliable—C99-compliant platforms all treat integer division in the same way. [For more information, see C99 Standard Section 6.5.5.]

# E.8.4 Flexible Array Members

[This section can be read after Section 10.3.]

C99 allows us to declare an array of unspecified length as the last member of a struct. Consider the following:

```
struct s {
    int arraySize;
    int array[];
};
```