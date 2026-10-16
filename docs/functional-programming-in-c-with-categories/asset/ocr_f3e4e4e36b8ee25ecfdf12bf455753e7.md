# C# Functional Features

An overview

> "1996 - James Gosling invents Java. Java is a relatively verbose, garbage collected, class based, statically typed, single dispatch, object oriented language with single implementation inheritance and multiple interface inheritance. Sun loudly heralds Java's novelty.
> 
> 2001 - Anders Hejlsberg invents C#. C# is a relatively verbose, garbage collected, class based, statically typed, single dispatch, object oriented language with single implementation inheritance and multiple interface inheritance. Microsoft loudly heralds C#'s novelty."
> -Brief, Incomplete and Mostly Wrong History of Programming Languages,

# 1 Language Functional support

# 1.1 Pure functions and Side effects

No matter the programming paradigm the minimal unit of processing is a function a→b. There would not be any motion if a value could not be transformed into another value. In Object oriented programming we call them methods. the most important thing about a function is its Type signature. A type signature or type annotation defines the inputs and outputs for a function, subroutine or method. In Object oriented programming we do not think about the function types that much, whilst in functional programming the function types are the main focus.

Look for example, the following function:

```
public double GetDiscountedPrice(double price, double discount)
{
    return price * (1 - discount);
}
```

This function has a signature like this GetDiscountedPrice: (double, double) → double. This is almost a perfect function. First, it's called total because no matter what value you input for the price and discount it will yield a result. Does not throw exceptions or return null. If only all functions where like this one. Also, its Pure because it does not access any outside