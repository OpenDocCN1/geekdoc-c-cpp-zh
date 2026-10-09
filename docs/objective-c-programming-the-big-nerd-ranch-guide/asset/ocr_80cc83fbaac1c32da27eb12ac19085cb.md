# # Stylish pointer declarations

When you declare a pointer to float, it looks like this:

```
```c
float *powerPtr;
```
```

Because the type is a pointer to a float, you may be tempted to write it like this:

```
```c
float* powerPtr;
```
```

This is fine, and the compiler will let you do it. However, stylish programmers don't.

Why? You can declare multiple variables in a single line. For example, if I wanted to declare variables x, y, and z, I could do it like this:

```
```c
float x, y, z;
```
```

Each one is a float.

What do you think these are?

```
```c
float* b, c;
```
```

Surprise! b is a pointer to a float, but c is just a float. If you want them both to be pointers, you must put a \* in front of each one:

```
```c
float *b, *c;
```
```

Putting the \* directly next to the variable name makes this clearer.

# # Challenges

Write a program that shows you how much memory a float consumes.

On your Mac, a short is a 2-byte integer, and one bit is used to hold the sign (positive or negative). What is the smallest number it can store? What is the largest? An unsigned short only holds non-negative numbers. What is the largest number it can store?