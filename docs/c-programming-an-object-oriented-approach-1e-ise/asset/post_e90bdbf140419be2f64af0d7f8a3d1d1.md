
## Program 10.20 Integral comparison of strings (Continued)

```cpp
 8  int main()
 9  {
10      // Declaration of two C++ strings
11      string strg1("Hello my friends");
12      string strg2("Hello friends");
13      // Comparing two C++ strings
14      cout << strg1 << " compared with " << strg2 << ": ";
15      cout << strg1.compare(strg2) << endl;
16      // Comparing part of the two C++ strings
17      cout << "Hello compared with Hello: ";
18      cout << strg1.compare(0, 5, strg2, 0, 5) << endl;
19      // Comparing part of the first C++ string and a C-string
20      cout << "Hello compared with Hello: ";
21      cout << strg1.compare(0, 5, strg2) << endl;
22      // Comparing part of a C++ string and part of a C-string
23      cout << "Hel compared with Hell: ";
24      cout << strg2.compare(0, 3, "Hello", 4) << endl;
25      return 0;
26 }
```

```text
Run:
Hello my friends compared with Hello friends: 1
Hello compared with Hello: 0
Hello compared with Hello: -8
Hel compared with Hell: -1
```

We check the results:

- 1. In the first comparison (line 15), we are comparing “Hello my friends” with “Hello friends”. The comparison goes character by character until we compare the ‘m’ character with the ‘f’ character. The ‘m’ character is larger than the ‘f’ character, the comparison stops, and the function returns 1 (a positive number).
- 2. In the second comparison (line 18), we are comparing “Hello” with “Hello”. The two substrings are equal, the result is 0.
- 3. In the third comparison (line 21), we are comparing “Hello” and “Hello friends”. A null character is compared to a space. The result is a negative number (−8).
- 4. In the fourth comparison (line 24), we are comparing “Hel” with “Hell”. When we reach the fourth character, we are comparing a null character with ‘l’. The result is a negative number (−1).

We must be careful that we do not convert the integral result to a Boolean type in integral comparison because both 1 and −1 are converted to true, which is not correct.

### Logical Comparison

The logical comparison compares two strings and returns a Boolean value (*true* or *false*). Just like the integral comparison, two strings are compared. The first is always the host, and the second is a C++ string or a C string. Unlike the integral comparison, we cannot compare two substrings. If we want to do so, we must make temporary C++ strings out of the substrings and then compare them.

The prototypes use operator overloading, which we will discuss in Chapter 13. The term Oper in the prototypes can be one of the relational or equality operators (<, <=, >, >=, ==, or !=). We can compare the two strings as though they are fundamental types using these operators. You may wonder if we can compare two C strings. We can do that, but they are considered fundamental types, and normal relational and equality operators are applied to them (we do not need the <string> header). Note that in logical comparisons, one of the two strings must be a C++ string.

The following shows how we can use these member functions.

```cpp
bool result = strg1 oper strg2;      // Comparing two C++ strings
bool result = strg oper str;         // Comparing a C++ string and a C string
bool result = str oper strg;         // Comparing a C string and a C++ string
```

## EXAMPLE 10.21

Program 10.21 compares strings.

### Program 10.21 Using logical operators to compare strings

```cpp
/*********************************************************************
 * The program to test logical operators to compare two strings.       *
 *********************************************************************/
#include <string>
#include <iostream>
using namespace std;

int main ( )
{
  // Creation of four C++ strings
  string strg1;
  string strg2 (5, 'a');
  string strg3 ("Hello Friends");
  string strg4 ("Hi People", 4);
  // Using six logical operators (relational and equality)
  cout << "strg1 < strg2 :" << boolalpha << (strg1 < strg2);
  cout << endl;
  cout << "strg2 >= strg3:" << boolalpha << (strg2 >= strg3);
  cout << endl;
  cout << "strg1 == strg2:" << boolalpha << (strg1 == strg2);
  cout << endl;
  cout << "Hi P != strg4:" << boolalpha << ("Hi P" != strg4);
  return 0;
}
```

```text
Run:
strg1 < strg2 : true
strg2 >= strg3: true
strg2 < strg3: false
strg1 == strg2: false
Hi P != strg4: false
```

## EXAMPLE 10.22

A string is a palindrome if it reads the same forward and backward. The strings “rotor,” “dad,” and “noon” are all palindromes. Examples of more complex palindromes are “Madam, I am Adam” and “Able was I ere I saw Elba.” We can easily check if a string is a palindrome by comparing it with its own reverse. In some cases, we must remove the punctuation and make the characters all the same before reversing the string. Program 10.22 shows how to check a string for palindrome.

### Program 10.22 Testing for a palindrome

```cpp
/**************************************************************
 * The program checks to see if an input string is a palindrome. *
 **************************************************************/
#include <string>
#include <iostream>
using namespace std;

// Declaration of two functions
void reverse (string& str);
bool isPalindrome (string& str);

int main ( )
{
   // Construction of a default string object
   string str;
   // Inputting
   cout << "Enter a string: ";
   getline (cin, str);
   // Checking for palindrome
   if (isPalindrome (str))
   {
      cout << str << " is a palindrome.";
   }
   else
   {
      cout << str << " is not a palindrome.";
   }
   return 0;
}
/**************************************************************
 * The isPalindrome function calls the reverse function       *
 * to compare its parameter with its reversed parameter.      *
 **************************************************************/
bool isPalindrome (string& str)
{
   string temp (str);
   reverse (temp);
   return (temp == str);
}
/************************************************
 * The reverse function reverses the string parameter. *
 ************************************************/
void reverse (string& strg)
{
   string temp (strg);
   int size = strg.size( );
   for (int i = 0; i < size; i++)
   {
       strg[i] = temp [size - 1 - i];
   }
}
```

```text
Run:
Enter a string: rotor
rotor is a palindrome.
```

```text
Run:
Enter a string: mom
mom is a palindrome.
```

```text
Run:
Enter a string: son
son is not a palindrome.
```

### Push_Back

We often need to add a character to a string. The string library defines the *push_back* function that adds a character at the end of the string. The library member function can be used as shown below:

```cpp
strg.push_back (c);           // Append character c at the end of strg
```

In our programming design section, we show how we can push a character in front of the string. We also show how we can pop a character from the front or the back.

### Modifying Operations

The C++ string library gives a set of different function definitions for modifying operations. However, if we construct a temporary string as the parameter, the number of member functions can be reduced to four. The *temp* string is the set of characters that we are looking for.

```cpp
temp (strg);                // A complete C++ string
temp (strg, pos2, n2);      // A part of C++ string
temp (1, c);                // A string made of one character
temp (cstr);                // A complete C-string
temp (cstr, n);             // The first n characters of a C-string
```

![](img/d68f6199646ca63591a6d8419e0ed4ba_499_0.png)

**Figure 10.12** General idea behind append, insert, replace, and assign

Figure 10.12 shows how four groups of functions use the temporary string to modify the host string.

The following shows how we use these four categories of functions:

```cpp
strg.append (temp);        // Append
strg.insert (pos1, temp);  // Insert
strg.replace (pos1, n1, temp); // Replace
strg.assign (temp);        // Assign
```

### Partial or Total Erasure

There are two functions that can totally or partially erase the characters in the string without destructing the string. The object still exists, but it is partially or totally devoid of its characters.

```cpp
strg.clear ();             // Erase all character in the string
strg.erase (pos, n);       // Erase part of the string
```

### Overloaded Operators

Some of the modifying operations are achieved using overloaded operators. C++ overloads the assignment operator (=), the compound assignment operator (+=), and the addition operator (+) as shown below. The *temp*, *temp1*, and *temp2* are instances of the *string* class.

```cpp
string strg = temp;        // Assignment
string strg += temp;       // Compound Assignment
string strg = temp1 + temp2; // Addition
```
