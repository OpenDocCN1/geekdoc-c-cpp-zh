
# Enumerations 151

By default, enumerators are assigned integer values starting with 0 for the first enumerator, 1 for the second enumerator, and so forth. You can override the default by explicitly assigning integer values. You'll see how later in this chapter.

You can use an enumeration name to declare a variable of the enumeration type: spectrum band; // band a variable of type spectrum

An enumeration variable has special properties, which we'll examine now. The only valid values that you can assign to an enumeration variable without a type cast are the enumerator used in defining the type. Thus, we have the following:

```
band = blue; // valid, blue is an enumerator
band = 2000; // invalid, 2000 is not an enumerator
```

Thus, a spectrum variable is limited to just eight possible values. Some compilers issue a compiler error if you attempt to assign an invalid value, whereas others issue a warning. For maximum portability, you should regard assigning a non-enum value to an enum as an error.

Only the assignment operator is defined for enumerations. In particular, arithmetic operations are not defined:

```
band = orange; // valid
++++; // not valid, defined in Chapter 5
band = orange + red; // not valid, a little tricky
```

However, some implementations do not honor this restriction. That can make it possible to violate the type limits. For example, if band has the value ultraviolet, or 7, then ++++; if valid, increments band to 8, which is not a valid value for a spectrum type. Again, for maximum portability, you should adopt the stricter limitations.

Enumerators are of integer type and can be promoted to type int, but int types are not converted automatically to the enumeration type:

```
int color = blue; // valid, spectrum type promoted to int
band = 3; // invalid, int not converted to spectrum
color = 3 + red; // valid, red converted to int
...
```

Note that in this example, even 3 corresponds to the enumerator green, assigning 3 to a band is a type error. But assigning green to band is fine because both type are spectrum. Again, some implementations do not enforce this restriction. In the expression 3 + red, addition is not defined for enumerators. However, red is converted to type int, and the result is type int. Because of conversion from enumeration to int in this situation, you can use enumerations in arithmetic expressions to combine them though arithmetic isn't defined for enumerations themselves.

```
band = orange + red; // not valid, a little tricky
```

fails for a somewhat involved reason. It is true that the + operator is not defined for enumerators. It is also true that enumerators are converted to integers when used in arithmetic expressions, the expression orange + red gets converted to 1 + 0, which is a valid expression. But it is of type int and hence cannot be assigned to the type spectrum variable band.

You can assign an int value to an enum, provided that the value is valid and that you use an explicit type cast:

```
band = spectrum(3);          // typecast 3 to type spectrum
```

What if you try to cast an inappropriate value? The result is undefined, meaning the attempt won't be flagged as an error but that you can't rely on the value of the result:

```
band = spectrum(40003);      // undefined
```

(See the "Value Ranges for Enumerations," later in this chapter for a discussion of what values are and not appropriate.)
As you see, the rules governing enumerations are fairly restrictive. In practice, enumerations are used more often as a value of defining symbolic constants than as new types. For example, you might use an enumeration to define symbolic constants for a switch statement. (See Chapter 6, "Branching Statements and Logic Operators") If you plan to use just the constants and not create variables of the enumeration type, you can omit an enumeration type name, as in this example:

```
enum {red, orange, yellow, green, blue, violet, indigo, ultraviolet};
```

## Setting Enumerator Values

You can set enumerator values explicitly by the assignment operator:

```
enum bits{one = 1, two = 2, four = 4, eight = 8};
```

The assigned values must be integers. You can also define just some of the enumerators explicitly:

```
enum bigstep{first, second = 100, third};
```

In this case, first is 0 by default. Subsequent uninitialized enumerators are larger by one than their predecessors. So, third would have the value 101.

Finally, you can create more than one enumerator with the same value:

```
enum {zero, null = 0, one, numero_uno = 1};
```

Here, both zero and null are 0, and both numero_uno and uno are 1. In earlier versions of C++, you could assign only int values (or values that promote to int) to enumerators, but that restriction has been removed so that you can use type long or long long values.

## Value Ranges for Enumerations

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

## Pointers and the Free Store

The beginning of Chapter 3 mentions three fundamental properties of a computer program must keep track where it stores data. To save the book and tear of your thumbing back to that chapter, there are those properties again:

- Where the information is stored
- What value is kept there
- What kind of information is stored

You've used one strategy for accomplishing these ends: defining a simple variable. The declaration statement provides the type and a symbolic name for the value. It also causes the program to allocate memory for the value and to keep track of the location internally.

Let's look at a second strategy now, that becomes particularly important in developing C++ classes. This strategy is based on pointers, which are variables that store addresses of values rather than the values themselves. Before discussing pointers, let's talk about how to explicitly find addresses for ordinary variables.You just apply the address operator, represented by &, to a variable to get its location; for example, if home is a variable, &home is its address. Listing 4.14 demonstrates this operator.

### Listing 4.14 address.cpp

```
// address.cpp -- using the & operator to find addresses
#include <iostream>
int main()
{
    using namespace std;
    int donuts = 6;
    double cups = 4.5;

    cout << "donuts value = " << &donuts << endl;
    // NOTE: you may need to use unsigned (donuts)
    // and unsigned (cups)
    cout << "cups value = " << &cups;
    cout << " and cups address = " << &cups << endl;
    return 0;
}
```

Here is the output from the program in Listing 4.14 on one system:
donuts value = 6 and donuts address = 00065fd40
cups value = 4.5 and cups address = 00065fd44

The particular implementation of cout shown here uses hexadecimal notation when displaying values because that is the usual notation used to specify a memory address. (Some implementations use base 10 instead.) Our implementation stores donuts at a lower memory location than cups.The difference between the two addresses is 00065fd44 - 00065fd40, or 4. This makes sense because donuts is type int, which uses 4 bytes. Different systems will give different values for the address. Also some store cups first, then donuts, giving a difference of 8 bytes because cups is double. And some may not even use adjacent locations.

Using ordinary variables, then, treats the value as a named quantity and the location as a derived quantity. Now let's look at the pointer strategy, one that is essential to the C++ programming philosophy of memory management. (See the following sidebar,"Pointers and the C++ Philosophy.")
