# C++ Strings

C++ does not have a built-in native string type. It does, however, have two ways to handle strings. First, we can use the C-style null-terminated character array. This is referred to as a C string. The second way is as a class object of type string.

The string class is a specialization of a more general class template called basic_string. basic_string has two specializations: string, which supports 8-bit character strings, and wstring, which supports 16-bit wide-character strings.

# String Constructors

The most commonly used string constructors are:

```
string();                          // empty string
string(const char *ptrStr);                  // string from a C string
string(const string& str);                     // copy constructor
string(int num, const char c)
```

The first constructor creates an empty string object. The second creates a string object from a null-terminated const string pointed to by ptrStr. The third constructor is the copy constructor. It creates a new string from a string object reference. The fourth constructor creates a new string where the character 'c' is repeated num times.

# String Operators

std::string implements the following operators:

| = | assignment |
| + | concatenation |
| == | equality |
| != | inequality |