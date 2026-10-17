# CHAPTER 4 } Print Functions

![](bbox=[0.075, 0.108, 0.797, 0.261])

interpreter processes the argument using the code associated with the function, it frequently *returns* a value. Some functions accept many arguments, but most are restricted to one return value. Sometimes the returned value consists of an altered form of the argument you have passed to the function. At other times the returned value consists of an integer (usually 0 or 1) that reports whether the function has successfully completed its operation. In the case of the `print()` function, you see the argument(s) you have passed to it rendered to the appropriate output device (usually either the monitor or a file).

> In this book, to distinguish function names from the names of other things, parentheses are appended to function names. Example: `print()`.

# Variations on Call and Return

Perl can sometimes prove confusing because it requires you to use no strict syntax conventions when you call functions. For example, if you program with a language like C, C++, or Java, you use a standard form of function call. This standard form always involves the name of the function, parentheses, and inside the parentheses the argument you submit to the function. With Perl, you can employ this form of calling functions, and throughout this book you are encouraged to do so, but in many instances, particularly respecting the `print()` function, you often see function calls as represented in Listing04_01.

```
```perl
#Listing04_01
#Perl functions allow you to use parentheses
#to enclose arguments (standard form, recommended):

$argumentForFunction = "\nHello";
print "\n#1";
#1 Standard function form
print ("$argumentForFunction");
```
```