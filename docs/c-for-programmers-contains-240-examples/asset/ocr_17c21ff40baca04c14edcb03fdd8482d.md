Remember that operator = in the preceding declaration is not an assignment; rather it is an implicit call to the string class constructor, which does the conversion.

Note that class string provides no conversions from int or char to string in a string definition. For example, the definitions

```
string error1 = 'c';
string error2( 'u' );
string error3 = 22;
string error4( 8 );
```

result in syntax errors. Note that assigning a single character to a string object is permitted in an assignment statement as in

```
string1 = 'n';
```

> **Common Programming Error 18.1**
> 
> Attempting to convert an int or char to a string via an initialization in a declaration or via a constructor argument is a compilation error.

Unlike C-style char * strings, strings are not necessarily null terminated. [Note: The C++ standard document provides only a description of the interface for class string—implementation is platform dependent.] The length of a string can be retrieved with member function length and with member function size. The subscript operator, [], can be used with strings to access and modify individual characters. Like C-style strings, strings have a first subscript of 0 and a last subscript of length() − 1.

Most string member functions take as arguments a starting subscript location and the number of characters on which to operate.

The stream extraction operator (>>) is overloaded to support strings. The statements

```
string stringObject;
cin >> stringObject;
```

declare a string object and read a string from the standard input device. Input is delimited by whitespace characters. When a delimiter is encountered, the input operation is terminated. Function getline also is overloaded for strings. Assuming string1 is a string, the statement

```
getline( cin, string1 );
```

reads a string from the keyboard into string1. Input is delimited by a newline ('\n'), so getline can read a line of text into a string object.

# 18.2 string Assignment and Concatenation

Figure 18.1 demonstrates string assignment and concatenation. Line 7 includes header <string> for class string. The strings string1, string2 and string3 are created in lines 12–14. Line 16 assigns the value of string1 to string2. After the assignment takes place, string2 is a copy of string1. Line 17 uses member function assign to copy string1 into string3. A separate copy is made (i.e., string1 and string3 are independent objects). Class string also provides an overloaded version of member function assign that copies a specified number of characters, as in

```
targetString.assign( sourceString, start, numberOfCharacters );
```