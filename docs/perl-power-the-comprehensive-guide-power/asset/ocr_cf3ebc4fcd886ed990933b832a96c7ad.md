# # CHAPTER 5 Scalars and Formatting

for or while loop), they do not cause your loops to repeat too many or too few times (see Chapters 10 and 11).

As a reminder, an _identifier_ is a word you use as the name of a variable. Generally, programmers say that they _declare_ a variable when they type the identifier. When you assign a value to a variable, you _initialize_ it. Some programmers refer to this as _defining_ the variable.

The Perl interpreter regards an identifier to which you have assigned a value as _defined_. It recognizes an identifier to which you have not assigned a value as _undefined_. The `defined()` function does not change the value in your identifier; rather, it evaluates your identifier. If it determines that you have defined the identifier, it returns true (1). If it finds that you have not defined the identifier, it returns false (0). In contrast to the `defined()` function, the `undef()` function does change the value of your identifier, for it strips the identifier of its definition. Listing05_02 examines some of the uses you can make of the `defined()` and `undef()` functions.

> When you use the `undef()` function, you make it so that you can safely reuse identifiers. If you are unsure of whether you might have assigned a string to an identifier and now want to use an identifier as a number, `undef()` ensures that you can remove the definition of the identifier as a string and make a fresh start with a number.

```
#Listing05_02
#use of define() and undef()

#1 Defining some scalars
#Scalars as strings
$FirstValue = "Hello";
#An undefined scalar
$SecondValue;
#A defined numeric scalar
$ThirdValue = 10;
#Other
$NL = "\n";

#2 Use defined to detect defined identifiers
```