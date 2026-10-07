# Chapter 8 Adventures in Functions

function type is string. This means the contents of temp will be copied to a temporary return location. Then, in main(), the contents of the return location are copied to the string name result:

```
result = version1(input, ****);
```

# Passing a C-Style String Argument to a string Object Reference Parameter

You may have noticed a interesting fact about the version1() function: Both parameters (s1 and s2) are type const string &, but the actual arguments (input and "****") are type string and const char *, respectively. Because input is type string, there is no problem having s1 refer to it. But how is that the program accepts a pointer-to-char as a string reference?

Two things are going on. One is that the string class defines a char-*string conversion, which makes it possible to initialize a string object to a C-style string. The second is property of const formal parameters which is discussed earlier in this chapter. Suppose the actual argument type doesn't match the reference type but can be converted to the reference type. Then the program creates a temporary variable of the correct type, initializes it to the converted value, and passes a reference to the temporary variable. Earlier this chapter you saw, for instance, a const double & parameter can handle an integer in this fashion. Similarly, a const string & parameter can handle a char * or const char * argument in this fashion.

The convenient outcome of this is that if the formal parameter type const string &, the actual argument used in the function call can be a string object or a C-style string, such as a quoted literal, a null-terminated array of char, or a pointer variable that points to a char. Here the following works fine:

```
result = version1(input, ****);
```

The version2() function doesn't create a temporary string. Instead, it directly alters the original string:

```
const string & version2(string & s1, const string & s2)   // has side effect
{
    s1 = s2 + s1;
    // safe to return reference passed to function
    return s1;
}
```

This function is allowed to alter s1 because s1, unlike s2, is not declared using const. Because s1 is a reference to an object (input) in main(), it's safe to return s1 as a reference. Because s1 is a reference to input, the line

```
result = version2(input, ####);
```

essentially becomes equivalent to the following:

```
version2(input, ####);   // input altered directly by version2()
result = input;         // reference to s1 is reference to input
```