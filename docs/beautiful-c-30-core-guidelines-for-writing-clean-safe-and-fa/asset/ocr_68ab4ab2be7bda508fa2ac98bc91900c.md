It has long been known, since before the advent of C++, that errno is problem-atic. Plenty of alternatives have been considered, with varying degrees of success, which permeate codebases around the world, some of which have been adopted as standard practice. Let’s take a look at other approaches to error handling.

# Return codes

The most common way of signaling an error is to simply tell the caller directly. You can achieve this with a return value. If your function has a well-defined domain of results, you can use values outside that domain to signal an error. For example, scanf returns the number of receiving arguments that have been successfully assigned to, which is a number greater than or equal to zero. However, it signals an error by returning EOF, which is a negative value.

This method has one obvious shortcoming, which is that the returned type must accommodate the result domain and the error domain. Consider the standard library function for finding the natural logarithm of a number:

```
double log(double);
```

Conceptually, the result domain completely exhausts the type. There is no way to signal an error. The standard has such a function and returns special values which signal that something has gone wrong; it can do this because there are a few values of double set aside to represent error conditions. This can be quite a surprise to the new programmer.

A more practical shortcoming is that callers can ignore return codes unless the function is marked with [no_discard]. Even then, the caller can choose to ignore the object that contains the return code. While this quietly shifts the blame to the caller, it is not in anyone’s interests to permit errors to be absorbed without consequence.

Another way of returning an error code is to pass an error-reporting destination into the function. This leads to an API that looks like this:

```
double log(double, int&);
```