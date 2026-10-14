```
string name = colorful.ToString();
Console.WriteLine(name);      // also writes out 'Fall'
```

Many of the standard operators that you can use on integer variables you can also use on enumeration variables (except the bitwise and shift operators, which are covered in Chapter 16, “Using indexers”). For example, you can compare two enumeration variables of the same type for equality by using the equality operator (==), and you can even perform arithmetic on an enumeration variable—although the result might not always be meaningful!

# Choosing enumeration literal values

Internally, an enumeration type associates an integer value with each element of the enumeration. By default, the numbering starts at 0 for the first element and goes up in steps of 1. It’s possible to retrieve the underlying integer value of an enumeration variable. To do this, you must cast it to its underlying type. The discussion in Chapter 8 on unboxing instructs that casting a type converts the data from one type to another as long as the conversion is valid and meaningful. The following code example writes out the value 2 and not the word Fall (remember, in the Season enumeration, Spring is 0, Summer 1, Fall 2, and Winter 3):

Click here to view code image

```
enum Season { Spring, Summer, Fall, Winter }
...
Season colorful = Season.Fall;
Console.WriteLine((int)colorful); // writes out '2'
```

If you prefer, you can associate a specific integer constant (such as 1) with an enumeration literal (such as Spring), as in the following example:

Click here to view code image

```
enum Season { Spring = 1, Summer, Fall, Winter }
```

# Important

The integer value with which you initialize an enumeration literal must be a compile-time constant value (such as 1).

If you don’t explicitly give an enumeration literal a constant integer value, the compiler gives it a value that is one greater than the value of the previous enumeration literal, except for the very first enumeration literal, to which the compiler gives the default value 0. In the preceding example, the underlying values of Spring, Summer, Fall, and Winter are now 1, 2, 3, and 4.

You are allowed to give more than one enumeration literal the same underlying value. For example, in the United Kingdom, fall is referred to as autumn. You can