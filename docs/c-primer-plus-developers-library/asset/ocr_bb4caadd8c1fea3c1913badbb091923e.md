```
```cpp
using namespace std;
int times;
char ch;

cout << "Enter a character: ";
cin >> ch;
cout << "Enter an integer: ";
cin >> times;
char * ps = buildstr(ch, times);
cout << ps << endl;
delete [] ps;                 // free memory
ps = buildstr('+', 20);       // reuse pointer
cout << ps << "-DONE-" << ps << endl;
delete [] ps;                 // free memory
return 0;
}

// builds string made of n c characters
char * buildstr(char c, int n)
{
    char * pstr = new char[n + 1];
    pstr[n] = '\0';           // terminate string
    while (n-- > 0)
        pstr[n] = c;          // fill rest of string
    return pstr;
}
```
```

Here’s a sample run of the program in Listing 7.10:

```
```text
Enter a character: V
Enter an integer: 46
VVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVV
++++++++++++++++++++++++++++++++DONE-++++++++++++++++++++
```
```

# Program Notes

To create a string of n visible characters, you need to store for n + 1 characters in order to have space for the null character. So the function in Listing 7.10 asks for n + 1 bytes to hold the string. Next, it sets the final byte to the null character. Then it fills in the rest of the array from back to front. In Listing 7.10, the following loop cycles n times as n decreases to 0, filling n elements:

```
```cpp
while (n-- > 0)
    pstr[n] = c;
```
```

At the start of the final cycle, n has the value 1. Because n-- means use the value and then decrement it, the while loop test condition compares 1 to 0, finds the test to be true, and continues. But after making the test, the function decrements n to 0, so pstr[0]