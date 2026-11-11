The `strcat()` function appends one string with another and returns a pointer with the resulting string. Listing 11 shows a program using the `strcat()` function and returns a char pointer (you can find the `ConcatenFunction.cpp` file on the CD in the `code\\chapter4` folder):

# ▶ **Listing 11: Using the strcat() Function**

```
```cpp
#include <iostream.h>
#include <string.h>
int main()
{
    char string1[] = "Good";//declare a character array of string
    char string2[] = " morning!"; //declare another array of string
    char* string3; // declare a character pointer
    string3 = strcat(string1,string2);//storing the result of concatenation
    cout<< string3<<endl;//print the result
    return 0;
}
```
```

**Output:**

```
```text
Good morning!
```
```

In Listing 11, we are declaring two character strings string1 and string2. Then we are calling the library function `strcat()`, which takes two strings (string1 and string2) as arguments, and returns the concatenated string. We have also declared a character pointer variable to hold the address of the string returned by the `strcat()` function. At last, we are retrieving the concatenated string with the help of character pointer variable.

# ■ **Exploring Dynamic Array**

As stated earlier, the new and delete operators are used to allocate and de-allocate memory to the pointers. The pointers to which you can allocate and de-allocate memory using these operators are called Dynamic array. For example, consider the following code snippet that allocate memory to the integer array arr by using the new operator, and de-allocate memory by using the delete operator:

```
```cpp
Int arr = new int [10]; // for creating and initializing array at run time.

delete arr; // for de-allocating memory assigned to the arr array.
```
```

Generally, dynamic arrays are preferred in comparison of static arrays (general arrays) because of the following benefits:

+   - The memory to static array is allocated at compile time, whether it is used in the program or not. On the other hand, the memory to dynamic array is allocated while executing the statement (declaring dynamic array) at run time by the program.