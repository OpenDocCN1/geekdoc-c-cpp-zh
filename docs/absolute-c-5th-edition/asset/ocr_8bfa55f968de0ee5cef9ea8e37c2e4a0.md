# Introduction to the string class

Although C++ lacks a simple data type to directly manipulate strings (sequences of text), there is a string class that may be used to process strings in a manner similar to the data types we see thus far. The distinction between a class and a simple type such as an int is discussed in Chapter 6. Further details about the string class are discussed in Chapter 9.

To use the string class we must first include the string library by adding the following line of code at the top of your program:

```
#include <string>
```

You declare variables of type string as you declare variables of type int or double. For example, the following declares one variable of type string and stores the text "durian" in:

```
string fruit;
fruit = "durian";
```

![](bbox=[0.125, 0.442, 0.198, 0.493])

# PITFALL: Uninitialized Variables

A variable has no meaningful value until a program gives it one. For example, if the minimumNumber has not been given a value either as the left-hand side of an assignment statement or by some other method (such as being given an input value with a cin statement), then the following is an error:

```
desiredNumber = minimumNumber + 10;
```

This is because minimumNumber has no meaningful value, and so the entire expression on the right-hand side of the equation has no meaningful value. A variable like minimumNumber that has not been given a value is said to be uninitialized. This situation is, in fact, worse than it would be if minimumNumber had no value at all. An uninitialized variable, like minimumNumber, will simply have some garbage value. The value of an uninitialized variable is determined by whatever location by the last program used that position of memory.

One way to avoid an uninitialized variable is to initialize variables at the same time they are declared. This can be done by adding an equal sign and a value, as follows:

```
int minimumNumber = 3;
```

This both declares minimumNumber to be a variable of type int and sets the value of the variable minimumNumber equal to 3. You can use a more complicated expression involving operations such as addition or multiplication when you initialize a variable inside the declaration in this way. As another example, the following declares variables and initializes two of them:

```
double rate = 0.07, time, balance = 0.00;
```