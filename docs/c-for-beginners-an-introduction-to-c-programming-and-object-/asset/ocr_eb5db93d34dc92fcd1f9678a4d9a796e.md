# ## 17.5 String Palindrome

A string is said to be a palindrome if the string and its reverse are the same. Consider a string - "madam". If you reverse the word "madam", you will still get "madam". This is a palindrome. Let us write a C++ program to take a string as an input from the user. We shall then reverse the string using a *for loop* and check if the original string and its reverse are the same using *strcmp* function (from *cstring* header). The strcmp function will return 0 if both strings are equal. Here is the C++ program:

```
```cpp
#include <iostream>
#include <cstring>

using namespace std;

int main ()
{
    char str[ ], reverse[ ];
    int length, j;
    // Temporary variable for swapping purpose
    int temp;
    //Ask the user to enter a string
    cout << endl << endl << "Enter a string: ";
    //Wait for user to enter
    cin.getline (str, sizeof (str) );
    length = strlen (str);
    // for reverse
    strcpy (reverse , str);
    //Reverse the string, store in reverse
    for ( int i = (length - 1); i > ((length - 1) / 2) ; i-- )
    {
        temp = reverse [i];
```
```