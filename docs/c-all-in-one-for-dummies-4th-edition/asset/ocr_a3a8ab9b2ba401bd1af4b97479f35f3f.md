# RANDOM NUMBERS AND STRINGS

Some special code appears in GetSecretCode() that requires explanation. The call to int randomnumber = rand(); generates a random number. To obtain a random number and convert it to a string, you add two more include lines:

```
```cpp
#include <stdlib.h>
#include <sstream>
```
```

The first line provides access to the rand() function. The second line provides access to the ostringstream type. Here are the three lines that perform the magic:

```
```cpp
int randomnumber = rand();
ostringstream converter;
converter << randomnumber;
```
```

The first of these creates a random number by calling rand(), which returns an int. The next line creates a variable of type ostringstream, which is a type that’s handy for converting numbers to strings. A variable of this type has features similar to that of a console. You can use the insertion operator (<<), except that instead of going to the console, anything you write goes into a string of type ostringstream (which comes from the words output, string, and stream; usually, things that allow the insertion operator << or the extraction operator >> to perform input and output are called streams). You can add the resulting string onto the code string variable using:

```
```cpp
code->append(converter.str());
```
```

The part inside parentheses — converter.str() — returns an actual string version of the converter variable. You use the append() function to add the string to code.

![](bbox=[0.172, 0.668, 0.24, 0.744])

Just as the parameters to a function are normally values, a function normally returns a value. In the case of returning a pointer, the function is still returning just a value — it is returning the value of the pointer, which is a number representing an address.

# Referring to Your Data Through Pointers