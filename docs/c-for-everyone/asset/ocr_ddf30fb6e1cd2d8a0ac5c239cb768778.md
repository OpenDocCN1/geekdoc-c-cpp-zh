```
```cpp
/*
Makes an uppercase version of a string.
@param str a string
@return a string with the characters in str converted to uppercase
*/
string uppercase(string str)
{
    string result = str; // Make a copy of str
    for (int i = 0; i < str.length(); i++)
    {
        result[i] = toupper(result[i]); // Convert each character to uppercase
    }
    return result;
}
```
```

For example, uppercase("Harry") returns a string with the characters "HARRY". The toupper function is defined in the <ctype> header. It converts lowercase characters to uppercase. (The tolower function does the opposite.)

![](bbox=[0.145, 0.344, 0.229, 0.431])

# SELF CHECK

+   11. How many char values are stored in the character array `"Hello, World!\n"`?
+   12. What is `strlen("Hello, World!\n")`?
+   13. Allocate a pointer variable that points to the string `"Hello"`.
+   14. Consider this statement:
+   
+       ```cpp
+       string title = "Agent" + 007;
+       ```
+   
+       Does the statement compile? What is its effect?
+   15. Consider the following statements:
+   
+       ```cpp
+       cout << "Enter an integer, Q to quit";
+       string input;
+       cin >> input;
+       if (input == "Q") { return; }
+       ```
+   
+       If the input is not the letter Q, how do you extract the number stored in the string input?

**Practice It**  Now you can try these exercises at the end of the chapter: R7.15, R7.16, P7.6.

# Special Topic 7.4

![](bbox=[0.124, 0.732, 0.23, 0.804])

# Working with C Strings

Before the string class became widely available, it was common to work with character arrays directly.

Table 4 on page 324 shows several commonly used functions for manipulating C strings. All of these functions are declared in the `<cstring>` header.

Consider the task of concatenating a first name and a last name into a string. The string class makes this very easy:

```
```cpp
string first = "Harry";
string last = "Smith";
string name = first + " " + last;
```
```

Let us implement this task with C strings. Allocate an array of characters for the result:

```
```cpp
const int NAME_SIZE = 40;
char name[NAME_SIZE];
```
```