# 2.3 DATA TYPES AND EXPRESSIONS

> *They'll never be happy together. He's not her type.*

OVERHEARD AT A COCKTAIL PARTY

# The Types *int* and *double*

Conceptually, the numbers 2 and 2.0 are the same number. But C++ considers them to be of different types. The whole number 2 is of type *int*; the number 2.0 is of type *double*, because it contains a fraction part (even though the fraction is 0). Once again, the mathematics of computer programming is a bit different from what you may have learned in mathematics classes. Something about the practicalities of computers makes a computer's numbers differ from the abstract definitions of these numbers. The whole numbers in C++ behave as you would expect them to. The type *int* holds no surprises. But values of type *double* are more troublesome. Because it can store only a limited number of significant digits, the computer stores numbers of type *double* as approximate values. Numbers of type *int* are stored as exact values. The precision with which *double* values are stored varies from one computer to another, but you can expect them to be stored with 14 or more digits of accuracy. For most applications this is likely to be sufficient, though subtle problems can occur even in simple cases. Thus, if you know that the values in some variable will always be whole numbers in the range allowed by your computer, it is best to declare the variable to be of type *int*.

Number constants of type *double* are written differently from those of type *int*. Constants of type *int* must not contain a decimal point. Constants of type *double* may be written in either of two forms. The simple form for *double* constants is like the everyday way of writing decimal fractions. When written in this form, a *double* constant must contain a decimal point. There is,

# What Is Doubled?

Why is the type for numbers with a fraction part called *double*? Is there a type called "single" that is half as big? No, but something like that is true. Many programming languages traditionally used two types for numbers with a fractional part. One type used less storage and was very imprecise (that is, it did not allow very many significant digits). The second type used *double* the amount of storage and was therefore much more precise; it also allowed numbers that were larger (although programmers tend to care more about precision than about size). The kind of numbers that used twice as much storage were called *double-precision* numbers;

(continued)