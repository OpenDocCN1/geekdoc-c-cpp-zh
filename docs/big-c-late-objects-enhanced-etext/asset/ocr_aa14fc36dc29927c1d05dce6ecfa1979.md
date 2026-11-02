# 7.3.5 C++ Strings and the [] Operator

Up to this point, we have always used the substr member function to access individual characters in a C++ string. For example, if a string variable is defined as

```
string name = "Harry";
```

the expression

```
name.substr(3, 1)
```

yields a string of length 1 containing the character at index 3.

You can access individual characters with the [] operator:

```
name[0] = 'L';
```

Now the string is "Larry". The [] operator is more convenient than the substr function if you want to visit a string one character at a time.

Here is a useful example. The following function makes a copy of a string and changes all characters to uppercase:

```
/**
 Makes an uppercase version of a string.
 @param str a string
 @return a string with the characters in str converted to uppercase
 */
string uppercase(string str)
{
 string result = str; // Make a copy of str
 for (int i = 0; i < result.length(); i++)
 {
 result[i] = toupper(result[i]); // Convert each character to uppercase
 }
 return result;
}
```

For example, uppercase("Harry") returns a string with the characters "HARRY".

The toupper function is defined in the <cctype> header. It converts lowercase characters to uppercase. (The tolower function does the opposite.)

EXAMPLE CODE See sec03 of your companion code for a program that demonstrates string processing.

You can access characters in a C++ string object with the [] operator.

![](bbox=[0.08, 0.86, 0.18, 0.93])

# Special Topic 7.4

# Working with C Strings

Before the string class became widely available, it was common to work with character arrays directly.

Table 4 shows several commonly used functions for manipulating C strings. All of these functions are declared in the <cstring> header.

Consider the task of concatenating a first name and a last name into a string. The string class makes this very easy:

```
string first = "Harry";
string last = "Smith";
string name = first + " " + last;
```