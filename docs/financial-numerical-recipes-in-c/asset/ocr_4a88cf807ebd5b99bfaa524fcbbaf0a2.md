# 1.2 The structure of a C++ program

The first thing to realize about C++ is that it is a strongly typed language. Everything must be declared before it is used, both variables and functions. C++ has a few basic building blocks, which can be grouped into types, operations and functions.

# 1.2.1 Types

The types we will work with in this book are bool, int, long, double and string.

Here are some example definitions

```
```cpp
bool this_is_true=true;
int i = 0;
long j = 123456789;
double pi = 3.141592653589793238462643;
string s("this is a string");
```
```

The most important part of C++ comes from the fact that these basic types can be expanded by use of classes, of which more later.

# 1.2.2 Operations

To these basic types the common mathematical operations can be applied, such as addition, subtraction, multiplication and division:

```
```cpp
int i = 100 + 50;
int j = 100 - 50;
int n = 100 * 2;
int m = 100 / 2;
```
```

These operations are defined for all the common datatypes, with exception of the string type. Such operations can be defined by the programmer for other datatypes as well.

**Increment and decrement** In addition to these basic operations there are some additional operations with their own shorthand. An example we will be using often is incrementing and decrementing a variable. When we want to increase the value of one item by one, in most languages this is written:

```
```cpp
int i=0;
i = i+1;
i = i+1;
```
```

In C++ this operation has its own shorthand

```
```cpp
int i=0;
i++;
i--;
```
```

While this does not seem intuitive, and it is excusable to think that this operation is not really necessary, it does come in handy for more abstract data constructs. For example, as we will see later, if one defines a date class with the necessary operations, to get the next date will simply be a matter of

```
```cpp
date d(1,1,1995);
d++;
```
```

These two statements will result in the date in d being 2jan95.