are not expected to understand all these concepts from this chapter. Rather, the idea is to point out that they are all somewhat related. The details come later.

# 1.2 Functions

Functions are a well-established mathematical concept: A function associates every value from a set with a unique value from another set (both sets may or may not be the same). The first set is often referred to as the domain of the function and the second as its range or codomain. Functions are said to map values from the domain to values from the codomain, and functions are sometimes called mappings. Functional programming is rooted in a yearning to write programs in terms of constructs that approach mathematical functions.

This mathematical notion of function does not necessarily coincide with what a function keyword might do in a programming language, or what you think of when you decide to implement a “function” in your favorite language. Instead, you need to think back to the functions you saw in your high-school algebra class. In that sense, f(x) = √x and g(x) = x² − 1 are functions (on real numbers), while Java’s sorting method Arrays.sort is not.

Why? The Java method sorts an array by rearranging its contents. By doing so, it modifies the array; it does not map it to another value. In mathematics, functions do not modify anything. What is there to modify, anyway? The number 4 is a value; √4 is another value, also a number; and so is 4² − 1. Functions map values to values, but values are not modified. Using √4 or 4² − 1 in a larger expression does not “modify” the number 4, whatever that would mean. Similarly, a sorting function—as opposed to Java’s Arrays.sort—would map an array value to another, sorted array value, but would not modify its input array in any way.

A core principle of functional programming is to organize code in terms of functions that do not modify anything. Consider, for instance, these two Java “functions”:

```
Java
String firstString1(List<String> strings) {
    return strings.get(0);
}

String firstString2(List<String> strings) {
    return strings.remove(0);
}
```

Both return the first string of a list of strings (assuming the list is not empty). Seen as functions, they are equivalent: For any non-empty list of strings x, the strings firstString1(x) and firstString2(x) are the same.¹ However, the firstString2 function also removes the first string from the list—thus modifying the list—while firstString1 does not.