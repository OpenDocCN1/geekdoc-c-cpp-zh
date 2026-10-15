# Overloaded Negation Operator

Line 22 of Fig. 11.9 declares the overloaded negation operator (defined in Fig. 11.10, lines 77–80). This operator determines whether an object of our `String` class is empty. For example, when the compiler sees the expression `!string1`, it generates the function call

```
string1.operator!()
```

This function simply returns the result of testing whether `length` is equal to zero.

# Overloaded Equality and Relational Operators

Lines 23–24 of Fig. 11.9 declare the overloaded equality operator (defined in Fig. 11.10, lines 83–86) and the overloaded less-than operator (defined in Fig. 11.10, lines 89–92) for class `String`. These are similar, so let us discuss only one example, namely, overloading the `==` operator. When the compiler sees the expression `string1 == string2`, the compiler generates the member-function call

```
string1.operator==( string2 )
```

which returns true if string1 is equal to string2. Each of these operators uses function `strcmp` (from <cstring>) to compare the character strings in the `String` objects. Many C++ programmers advocate using some of the overloaded operator functions to implement others. So, the !=, >, <= and >= operators are implemented (Fig. 11.9, lines 27–48) in terms of operator== and operator<. For example, overloaded function operator>= (implemented in lines 45–48 in the header file) uses the overloaded < operator to determine whether one String object is greater than or equal to another. Note that the operator functions for !=, >, <= and >= are defined in the header file. The compiler inlines these definitions to eliminate the overhead of the extra function calls.

> **Software Engineering Observation 11.10**
> 
> By implementing member functions using previously defined member functions, you reuse code to reduce the amount of code that must be written and maintained.

# Overloaded Subscript Operators

Lines 50–51 in the header file declare two overloaded subscript operators (defined in Fig. 11.10, lines 95–106 and 109–120, respectively)—one for non-const Strings and one for const Strings. When the compiler sees an expression like `string1[ 0 ]`, the compiler generates the member-function call

```
string1.operator[]( 0 )
```

(using the appropriate version of `operator[]` based on whether the String is const). Each implementation of `operator[]` first validates the subscript to ensure that it is in range. If the subscript is out of range, each function prints an error message and terminates the program with a call to `exit.`⁵ If the subscript is in range, the non-const version of `operator[]` returns a `char &` to the appropriate character of the `String` object; this `char &` may be used as an lvalue to modify the designated character of the String object. The const version of `operator[]` returns the appropriate character of the String object; this can be used only as an rvalue to read the value of the character.

5. Again, it is more appropriate when the subscript is out of range to “throw an exception” indicating the out-of-range subscript.