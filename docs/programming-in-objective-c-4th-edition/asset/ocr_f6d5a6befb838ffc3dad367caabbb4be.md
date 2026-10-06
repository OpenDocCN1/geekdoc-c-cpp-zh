(Note: we acknowledge that there is already a predefined symbol called M_PI that you can use whenever you need the value of π.) Assigning a constant to a symbolic name frees you from having to remember the particular constant value every time you want to use it in a program. Furthermore, if you ever need to change the value of the constant (if perhaps you found that you were using the wrong value, for example), you would have to change the value in only one place in the program: in the #define statement. Without this approach, you would have to search throughout the program and explicitly change the value of the constant whenever it was used.

You might have realized that all the defines so far (TRUE, FALSE, and PI) have been written in capital letters. This is done to visually distinguish a defined value from a variable. Some programmers adopt the convention that all defined names are capitalized, so determining when a name represents a variable or an object, a class name, or a defined name is easy. Another common convention is to prefix the define with the name k. In that case, the following characters of the name are not capitalized. kMaximumValues and kSignificantDigits are examples of two defined names that adhere to this convention.

Using a name for a constant value helps make programs more readily extendable. For example, when you learn how to work with arrays, instead of hard-coding in the size of the array you want to allocate, you can define a value as follows:

```
#define MAXIMUM_DATA_VALUES 1000
```

Then you can base all references on the array's size (such as allocation of the array in memory) and valid indexes into this array on this defined value.

Also, if the program were written to use MAXIMUM_DATA_VALUES in all cases where the size of the array was used, the preceding definition could be the only statement in the program that would have to be changed if you later needed to change the array size.