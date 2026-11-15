
## Character Strings

Recall from Chapter 7 that a character array is an array in which the individual elements are stored as characters. A C-style character string is a character array in which the last array element is a null character. Character strings are used in many engineering applications, including cryptography and pattern recognition. It is often convenient to manipulate character strings via pointers to strings. Many of the character functions in the header file cstring, introduced in Chapter 6, require pointers to strings as arguments, and many return pointers to strings. In this section, we will look at the syntax required to reference C-style character strings using pointers.

One of the functions included in the header file cstring is the function named strstr(). The function strstr(ps, pt) takes a pointer to string s and a pointer to string t as arguments and returns a pointer to the start of the string t within the string s. If t does not occur in s, a NULL pointer is returned. We will use this function in our next example.

Assume that we want to count the occurrences of one string in another string. For example, suppose we want to count the number of times that the string “bb” occurs in the string “abcfgwdbbibw”. The strstr() function will return a pointer to the start of the first occurrence of “bb” in “abcfgwdbbibw”, or a NULL pointer if “bb” is not found. In this example, the strstr() function will return a pointer to the beginning of the first occurrence of “bb”, as follows:

```
"abcfgwdbbibw"
```

To find the next occurrence of the string “bb”, we need to search the portion of the string that follows the first position of the occurrence of “bb”. The strstr() function will then return a pointer to the beginning of the first occurrence of “bb” in the new portion of the string as follows:

```
"bcfgwdbbibw"
```

We repeat the process until the strstr() function returns a NULL value. The complete program to implement this process follows:

```
/* .................................................... */
/* Program chapter9_4 ............................... */
/* .................................................... */
/* This program counts and prints the number of */
/* times one string appears within another string. */
/* .................................................... */
#include <iostream> //Required for cout
#include <cstring> //Required for strstr
using namespace std;

int main()
{ // Declare and initialize objects.
    int count(0);
    char strg1[] = "abcfgwdbbibw", strg2[] = "bb";
    char *ptr1(strg1), *ptr2(strg2);

// Count number of occurrences of strg2 in strg1.
// While function strstr does not return NULL
// increment count and move ptr1 to next section
// of strg1.
while ((ptr1=strstr(ptr1,ptr2)) != NULL)
{
    count++;
    ptr1++;
}
// Print the number of occurrences.
cout << "Count: " << count << endl;
return 0;
/*-------------------------------------------------------------*/
```

The output from this program is:

Count: 2

## Pointers as Function Arguments

When a pointer is passed as an argument to a function, the pointer can be passed by value or passed by reference. If a pointer is passed by value, the pointer can be used to modify the object it points to, but the value of the pointer argument cannot be modified by the function.

If a pointer is passed by reference, the pointer can be used to modify the object it points to, and the value of the pointer argument can also be modified.

Consider the following program that calls a function to convert a string to uppercase:

```
/*-------------------------------------------------------------*/
/* Program chapter9_5                                          */
/*                                                             */
/* This program converts a string to all upper case.           */
/*                                                             */
/*-------------------------------------------------------------*/
#include <iostream> //Required for cout
#include <cctype>   //Required for toupper()
using namespace std;
//Function prototypes
void stringupper(char*);
int main()
{
    // Declare and initialize objects.
    char strg1[] = "abbfgwdhbbw";
    char *ptr_str1(strg1);
    // Ouput string before and after call to function.
    cout << ptr_str1 << endl;
stringupper(ptr_str1);
cout << ptr_str1 << endl;
return 0;
/********************************************************************
* *
* *
* This function converts each character in
* the string pointed to by ptr_strg to upper case.
* *
********************************************************************/
void stringupper(char* ptr_strg)
{
// While not end of string (while character is not null).
while(*ptr_strg)
{
// Convert character to upper case
*ptr_strg = toupper(*ptr_strg);
// Move pointer to next character
ptr_strg++;
}
}
/********************************************************************
*/
```

In this example, the pointer ptr_str1 is passed to the function stringupper(), and the string pointed to by ptr_str1 is converted to uppercase. The formal parameter ptr_strg is incremented in the function to traverse the string, but no change is made to the argument in main because a pass by value is used. The output from this program is

abbcfgwdibbw
ABCCFGWDBIBBW

The next program modifies the function in program 9_5 to use pass by reference instead of pass by value:

```
/********************************************************************
* Program chapter9_6 *
* *
* This program converts a string to all upper case. *
* *
********************************************************************/
#include <iostream> //Required for cout
#include <cctype> //Required for toupper
using namespace std;
//Function prototypes
void stringupper(char*&);
int main()
{
// Declare and initialize objects.
char strg1[] = "abbcfgwdibbw";
char *ptr_strg1 = strg1;
// Output string before and after call to function.
cout << ptr_strg1 << endl;
stringupper(ptr_strg1);
cout << ptr_strg1 << endl;
return 0;
/* ----------------------------------------------------------- */
/*
/* This function converts each character in the string
/* pointed to by ptr_strg1 to upper case.
/*
void stringupper(char *&ptr_strg1)
{
// While not end of string.
while(*ptr_strg1)
{
    // Convert character to upper case
    *ptr_strg1 = toupper(*ptr_strg1);
    // Move pointer to next character
    ptr_strg1++;
}
/* ----------------------------------------------------------- */
```

![](img/f2bfa570e453b020c16e048c79a3ea0e_466_0.png)

> Notice the order of operators in the function prototype and the function header. When passing a pointer by reference the address operator must follow the dereference operator.

In this version of the program, the string is converted to uppercase just as it was in program Chapter9_6. However, in this version, incrementing the formal parameter in the function changes the argument in main because a pass by reference is used. After the call to the function stringupper(), the pointer ptr_strg1 points to the null character at the end of the string. Thus, the uppercase string will not be printed. A sample output from this program is

abcfgwdbibbw

In both examples, the function stringupper() was able to modify the string being pointed to by the formal parameter.

Sometimes it is desirable to pass a pointer as an argument to a function and also ensure that the function will not inadvertently modify the object being pointed to. We can use the const modifier in the function prototype, and the function header, to protect the object being pointer to, as illustrated in the next example. The definition for the function stringupper() is not included in this example:

```
/* ----------------------------------------------------------- */
/*
/* Program chapter9_7
/*
/* This program counts the number of times a specified
/* letter appears in an upper case string.
/*
#include <iostream> //Required for cout
#include <cctype> //Required for toupper()
using namespace std;

//Function prototypes.
void stringupper(char*);
int countchar(const char*, char);

int main()
{
    // Declare and Initialize objects.
    char strg1[] = "aBcFgGwdIbbW";
    char *ptr_strg1 = strg1, ch='B';

    // Convert string to upper case.
    stringupper(ptr_strg1);

    cout << "The letter " << ch << " appears "
         << countchar(ptr_strg1, ch) << " times in the string "
         << ptr_strg1 << endl;

    return 0;
}

/**
* *********************************************************************
* *
* * This function counts the number of times the character ch *
* * appears in the string pointed to by ptr_strg. *
* *
* *********************************************************************
*/

int countchar(const char* ptr_strg, char ch)
{
    // Declare and initialize local objects.
    int cnt(0);

    // While not end of string.
    while(*ptr_strg)
    {
        // Look for ch and increment cnt.
        if( *ptr_strg == ch)
            cnt++;

        // Move pointer to next character
        ptr_strg++;
    }
    return cnt;
}
```

This program generates the following output:

The letter B appears 5 times in the string ABCBCFGWDIBIBW
