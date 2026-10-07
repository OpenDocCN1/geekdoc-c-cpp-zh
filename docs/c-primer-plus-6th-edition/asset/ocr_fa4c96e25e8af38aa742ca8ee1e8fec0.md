# Chapter 3 Dealing with Data

The stream class to cout belongs to class member functions that give you precise control over how the output is formatted—field widths, places to the right of the decimal point, decimal form or E form, and so on. Chapter 17 outlines these choices. This book's examples keep it simple and usually use the << operator. Occasionally, this displays more digits than necessary, but that causes aesthetic harm. If you do mind, you can skip Chapter 17 to see how to use the formatting methods. Don't, however, expect to fully follow the explanations at this point.

# Reading Include Files

The includes directives at the top of C++ source files often take the air of a magical incantation; unlike C++ programmers learn, through reading and experience, which header files add particularities, and they include solely to make their programs work. Don't rely on the include files as they are some of mystic and arcane knowledge; free to open them up and read them. They are text files, so you can read them easily. The files you include in programs exist on your computer or in a place where your computer can use. Find the includes you use and see what they contain. You'll quickly see that the source and header files you use are an excellent source of knowledge and information—in some cases, the best documentation available. Later, as you progress into more complex inclusions and use other, nonstandard libraries in your applications, this habit will serve you well.

# Floating-Point Constants

When you write a floating-point constant in a program, in which floating-point type does the program store it? By default, floating-point constants like 8.24 and 2.4E8 are of type double. If you want a constant to be float, use an f or F suffix. For type long double, use an l or L suffix. (Because the lowercase l looks a lot like the digit 1, the uppercase L is a better choice). Here are some samples:

```
1.234f      // a float constant
2.45E08     // a float constant
2.345324E28  // a double constant
2.2L        // a long double constant
```

# Advantages and Disadvantages of Floating-Point Numbers

Floating-point numbers have two advantages over integers. First, they can represent values between integers. Second, because of the scaling factor, they can represent a much greater range of values. On the other hand, floating point operations are slightly slower than integer operations, and can lose precision. Listing 3.9 illustrates the last point.

# Listing 3.9 ftldd.cpp

```
// ftldd.cpp  -- precision problems with float
#include <iostream>
int main()
{
```