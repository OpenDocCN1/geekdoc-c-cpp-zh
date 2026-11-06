
You use the `//` syntax for single-line comments. If you have a comment that spans multiple lines, enclose it between `/*` and `*/` delimiters. The compiler ignores these delimiters and everything in between.

Here is a typical example, a long comment at the beginning of a program, to explain the program’s purpose:

```cpp
/*
   This program computes the volume (in liters) of a six-pack of soda
   cans and the total volume of a six-pack and a two-liter bottle.
*/
```

We are now ready to finish our program. The following program shows the use of variables, constants, and the assignment statement. The program displays the volume of a six-pack of cans and the total volume of the six-pack and a two-liter bottle. We use constants for the can and bottle volumes. The `total_volume` variable is initialized with the volume of the cans. Using an assignment statement, we add the bottle volume.

### ch02/volume1.cpp

```cpp
#include <iostream>

using namespace std;

/*
   This program computes the volume (in liters) of a six-pack of soda
   cans and the total volume of a six-pack and a two-liter bottle.
*/

int main()
{
   int cans_per_pack = 6;
   const double CAN_VOLUME = 0.355; // Liters in a 12-ounce can
   double total_volume = cans_per_pack * CAN_VOLUME;

   cout << "A six-pack of 12-ounce cans contains "
        << total_volume << " liters." << endl;

   const double BOTTLE_VOLUME = 2; // Two-liter bottle
   total_volume = total_volume + BOTTLE_VOLUME;

   cout << "A six-pack and a two-liter bottle contain "
        << total_volume << " liters." << endl;

   return 0;
}
```

### Program Run

```
A six-pack of 12-ounce cans contains 2.13 liters.
A six-pack and a two-liter bottle contain 4.13 liters.
```

![](img/23fb3582e93ebc95909e1de029c3d388_63_0.png)

1. Define a variable suitable for holding the number of bottles in a case.
2. What is wrong with the following variable definition?  
   `int ounces per liter = 28.35`
3. Define and initialize two variables, `unit_price` and `quantity`, to contain the unit price of a single bottle and the number of bottles purchased. Use reasonable initial values.
4. Use the variables defined in Self Check 3 to display the total purchase price.
5. Some drinks are sold in four-packs instead of six-packs. How would you change the `volume1.cpp` program to compute the total volume?
6. What is wrong with this comment?
   ```cpp
   double can_volume = 0.355; /* Liters in a 12-ounce can //
   ```
7. Suppose the type of the `cans_per_pack` variable in the `volume1.cpp` program was changed from `int` to `double`. What would be the effect on the program?
8. Why can’t the variable `total_volume` in the `volume1.cpp` program be declared as `const`?
9. How would you explain assignment using the parking space analogy?

### Practice It

Now you can try these exercises at the end of the chapter: R2.1, R2.2, P2.1.

### Common Error 2.1

### Using Undefined Variables

![](img/23fb3582e93ebc95909e1de029c3d388_64_0.png)

You must define a variable before you use it for the first time. For example, the following sequence of statements would not be legal:

```cpp
double can_volume = 12 * liter_per_ounce;
double liter_per_ounce = 0.0296;
```

In your program, the statements are compiled in order. When the compiler reaches the first statement, it does not know that `liter_per_ounce` will be defined in the next line, and it reports an error.

### Common Error 2.2

### Using Uninitialized Variables

![](img/23fb3582e93ebc95909e1de029c3d388_64_1.png)

If you define a variable but leave it uninitialized, then your program can act unpredictably. To understand why, consider what happens when you define a variable. Just enough space is set aside in memory to hold values of the type you specify. For example, with the definition

```cpp
int bottles;
```

a block of memory big enough to hold integers is reserved. There is already *some* value in that memory. After all, you don’t get freshly minted transistors—just an area of memory that has previously been used, filled with flotsam left over from prior computations. (In this regard, a variable differs from a parking space. A parking space can be empty, containing no vehicle. But a variable always holds some value.)

If you use the variable without initializing it, then that prior value will be used, yielding unpredictable results. For example, consider the program segment

```cpp
int bottles; // Forgot to initialize
int bottle_volume = bottles * 2; // Result is unpredictable
```

There is no way of knowing what value will be computed. If you are unlucky, a plausible value will happen to appear when you run the program at home, and an entirely different result will occur when the program is graded.

### Programming Tip 2.1

![](img/23fb3582e93ebc95909e1de029c3d388_65_0.png)

### Choose Descriptive Variable Names

We could have saved ourselves a lot of typing by using shorter variable names, as in

```cpp
double cv = 0.355;
```

Compare this definition with the one that we actually used, though. Which one is easier to read? There is no comparison. Just reading `can_volume` is a lot less trouble than reading `cv` and then figuring out it must mean “can volume”.

In practical programming, this is particularly important when programs are written by more than one person. It may be obvious to you that `cv` stands for can volume and not current velocity, but will it be obvious to the person who needs to update your code years later? For that matter, will you remember yourself what `cv` means when you look at the code three months from now?

### Special Topic 2.1

![](img/23fb3582e93ebc95909e1de029c3d388_65_1.png)

### Numeric Types in C++

In addition to the `int` and `double` types, C++ has several other numeric types.

C++ has two floating-point types. The `float` type uses half the storage of the `double` type that we use in this book, but it can only store 6–7 digits. Many years ago, when computers had far less memory than they have today, `float` was the standard type for floating-point computations, and programmers would indulge in the luxury of “double precision” only when they needed the additional digits. Today, the `float` type is rarely used.

By the way, these numbers are called “floating-point” because of their internal representation in the computer. Consider numbers 29660, 2.96, and 0.0296. They can be represented in a very similar way; namely, as a sequence of the significant digits—296—and an indication of the position of the decimal point. When the values are multiplied or divided by 10, only the position of the decimal point changes; it “floats”. Computers use base 2, not base 10, but the principle is the same.

#### Table 4 Number Types

| Type | Typical Range | Typical Size |
| --- | --- | --- |
| `int` | −2,147,483,648 ... 2,147,483,647 (about 2 billion) | 4 bytes |
| `unsigned` | 0 ... 4,294,967,295 | 4 bytes |
| `short` | −32,768 ... 32,767 | 2 bytes |
| `unsigned short` | 0 ... 65,535 | 2 bytes |
| `long long` | −9,223,372,036,854,775,808 ... 9,223,372,036,854,775,807 | 8 bytes |
| `double` | The double-precision floating-point type, with a range of about ±10<sup>308</sup> and about 15 significant decimal digits | 8 bytes |
| `float` | The single-precision floating-point type, with a range of about ±10<sup>38</sup> and about 7 significant decimal digits | 4 bytes |

In addition to the `int` type, C++ has integer types `short`, `long`, and `long long`. For each integer type, there is an `unsigned` equivalent. For example, the `short` type typically has a range from −32,768 to 32,767, whereas `unsigned short` has a range from 0 to 65,535. These strange-looking limits are the result of the use of binary numbers in computers. A `short` value uses 16 binary digits, which can encode 2¹⁶ = 65,536 values. Keep in mind that the ranges for integer types are not standardized, and they differ among compilers. Table 4 contains typical values.

### Special Topic 2.2

![](img/23fb3582e93ebc95909e1de029c3d388_66_0.png)

### Numeric Ranges and Precisions

Because numbers are represented in the computer with a limited number of digits, they cannot represent arbitrary integer or floating-point numbers.

The `int` type has a limited range: On most platforms, it can represent numbers up to a little more than two billion. For many applications, this is not a problem, but you cannot use an `int` to represent the world population.

If a computation yields a value that is outside the `int` range, the result overflows. No error is displayed. Instead, the result is truncated to fit into an `int`, yielding a useless value. For example,

```cpp
int one_billion = 1000000000;
cout << 3 * one_billion << endl;
```

displays −1294967296.

In situations such as this, you can switch to `double` values. However, read Common Error 2.6 on page 45 for more information about a related issue: roundoff errors.

### Programming Tip 2.2

![](img/23fb3582e93ebc95909e1de029c3d388_66_1.png)

### Do Not Use Magic Numbers

A magic number is a numeric constant that appears in your code without explanation. For example,

```cpp
total_volume = bottles * 2;
```

Why 2? Are bottles twice as voluminous as cans? No, the reason is that every bottle contains 2 liters. Use a named constant to make the code self-documenting:

```cpp
const double BOTTLE_VOLUME = 2;
total_volume = bottles * BOTTLE_VOLUME;
```

There is another reason for using named constants. Suppose circumstances change, and the bottle volume is now 1.5 liters. If you used a named constant, you make a single change, and you are done. Otherwise, you have to look at every value of 2 in your program and ponder whether it means a bottle volume, or something else. In a program that is more than a few pages long, that is incredibly tedious and error-prone.

Even the most reasonable cosmic constant is going to change one day. You think there are seven days per week? Your customers on Mars are going to be pretty unhappy about your silly prejudice. Make a constant.

```cpp
const int DAYS_PER_WEEK = 7;
```

![](img/23fb3582e93ebc95909e1de029c3d388_66_2.png)
