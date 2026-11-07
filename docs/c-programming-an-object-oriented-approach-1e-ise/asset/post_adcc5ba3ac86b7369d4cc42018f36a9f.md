
## Program 19.6 Printing list elements (Continued)

```text
Run:
Enter an integer: 25
Enter an integer: 32
Enter an integer: 41
Enter an integer: 72
Enter an integer: 95
Print the list in forward direction.
25    32    41    72    95
Print the list in reverse direction.
95    72    41    32    25
```

We can rewrite Program 19.2 without using the + or − operators, which are not defined for bidirectional iterators. Program 19.7 shows a solution.

## Program 19.7 Printing some elements in a list

```cpp
/*~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
 * Rewrite of Program 19-2 using list instead of vector
 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~*/
#include <iostream>
#include <list>
using namespace std;

int main()
{
    // Instantiation of the list container and defining two iterators
    list <int> lst;
    list <int>:: iterator iter1;
    list <int>:: reverse_iterator iter2;
    // Inserting 10 integers into the list
    for (int i = 0; i < 10; i++)
    {
        lst.push_back(i * 10);
    }
    // Moving two steps forward and two steps backward using iter1
    cout << "Printing 40 followed by 20" << endl;
    iter1 = lst.begin();
    iter1++;
    iter1++;
    iter1++;
    iter1++;
    cout << *iter1 << " ";
    iter1--;
    iter1--;
    cout << *iter1 << endl;
    // Moving two steps forward and two steps backward using iter2
    cout << "Printing 50 followed by 70" << endl;
    iter2 = lst.rbegin();
    iter2++;
    iter2++;
    iter2++;
    iter2++;
    cout << *iter2 << " ";
    iter2--;
    iter2--;
    cout << *iter2 << endl;
    return 0;
}
```

```text
Run:
Printing 40 followed by 20
40     20
Printing 50 followed by 70
50     70
```

We create a big integer class that handles any integer with any arbitrary number of digits. We provide only the addition operation of two big integers. Program 19.8 shows the interface for a simple big integer class with only the addition (+) operation. We use a list in which each element holds a digit. Another solution is to allow each element to hold three or six digits, but the coding is more complicated.

## Program 19.8 The file bigInteger.h

```cpp
/*************************************************************
 * The interface for the big integer class                   *
 *************************************************************/
#include <string>
#include <list>
#include <iostream>
#ifndef BIGINTEGER_H
#define BIGINTEGER_H
using namespace std;

class BigInteger
{
private:
    list <int> lst;
public:
    BigInteger();
    BigInteger(string str);
    ~BigInteger();
    string toString();
    friend BigInteger operator+(BigInteger first, BigInteger second);
};
#endif
```

Program 19.9 shows the implementation file for the big integer class. We have coded two constructors, one destructor, one addition operator, and one member function called toString(). It is customary in computer programming to define a toString function that creates a string object out of a value so that the object can be exported to other programs.

## Program 19.9 The file bigInteger.cpp

```cpp
/*************************************************************
 * The implementation file for the BigInteger class          *
 *************************************************************/
#include <iostream>
#include <string>
#include <iomanip>
#include "bigInteger.h"
using namespace std;

// Default constructor
BigInteger :: BigInteger()
:lst (list<int>())
{
}
// Parameter constructor
BigInteger :: BigInteger(string str)
:lst (list<int>())
{
    for (int i = 0; i < str.length(); i++)
    {
        int num = str[i] - 48;
        lst.push_back(num);
    }
}
// Destructor
BigInteger :: ~BigInteger()
{
// Changing a list to a string for printing
}
```

```cpp
string BigInteger :: toString()
{
    string strg;
    list <int> :: iterator iter;
    iter = lst.begin();
    while (iter != lst.end())
    {
        strg.append(1, *iter + 48);
        iter++;
    }
    return strg;
}
// Friend operator+
BigInteger operator+(BigInteger first, BigInteger second)
{
    list <int> :: reverse_iterator iter1;
    list <int> :: reverse_iterator iter2;
    BigInteger result;
    int num1, num2, sum;
    int carry = 0;
    iter1 = first.lst.rbegin();
    iter2 = second.lst.rbegin();
    while ((iter1 != first.lst.rend()) && (iter2 != second.lst.rend()))
    {
        num1 = *iter1;
        num2 = *iter2;
        sum = (num1 + num2 + carry) % 10;
        carry = (num1 + num2 + carry) / 10;
        result.lst.push_front(sum);
        iter1++;
        iter2++;
    }
    while ((iter1 != first.lst.rend()))
    {
        num1 = *iter1;
        sum = (num1 + carry) % 10;
        carry = (num1 + carry) / 10;
        result.lst.push_front (sum);
        iter1++;
    }
    while ((iter2 != second.lst.rend()))
    {
        num2 = *iter2;
        sum = (num2 + carry) % 10;
        carry = (num2 + carry) / 10;
        result.lst.push_front(sum);
        iter2++;
    }
    if (carry == 1)
    {
        result.lst.push_front(carry);
    }
    return result;
}
```

In Program 19.9 the default constructor creates an empty list. The parameter constructor takes a string representing a big integer, such as “4572349876509”, extracts the digits, one by one as ASCII characters, subtracts 48 from the integer value of the ASCII character to create a digit, and then pushes it to the back of the list. Note that the character is copied from the front of the string, but it is pushed to the back of the list. The next digit pushes the digit at the back of the list toward the front. When the big integer object is instantiated, we have a list of integers in which each element holds one digit.

The next member function is the toString() function, which does the reverse. It copies digits one by one from the list and appends them to a string.

The heart of the implementation is the friend operator+() function, which takes two big integer objects, adds the digits from the right, and creates a sum and a carry. We need to use three while loops. If the two lists are of the same size, the first loop does the job. If either of the lists is exhausted, one of the other two loops continues. Note that if both loops are exhausted, we may still have a carry from the last two digits added; the if statement at the end takes care of this situation. Program 19.10 shows a sample application that uses our BigInteger class.

## Program 19.10 The application file (app.cpp)

```cpp
/**************************************************************
 * Application file to test the BigInteger class              *
 ***************************************************************/
#include <iostream>
#include <iomanip>
#include "bigInteger.h"
using namespace std;

int main()
{
    // Inputting two strings
    string str1, str2;
    cout << "Enter the first big integer: ";
    cin >> str1;
    cout << "Enter the second big integer: ";
    cin >> str2;
    // Creation of two objects of type BigInteger
    BigInteger first (str1);
    BigInteger second (str2);
    // Adding two big integers and storing the result in the third object
    BigInteger result = first + second;
    // Changing big integers to strings
    str1 = first.toString();
    str2 = second.toString();
    string strg3 = result.toString();
    string dashes(strg3.length(), '-');
    // Printing the result
    cout << "First big integer " << setw(strg3.length());
    cout << right << str1 << endl;
    cout << "Second big integer " << setw(strg3.length());
    cout << right << str2 << endl;
    cout << "                 " << dashes << endl;
    cout << "Result           " << setw(strg3.length());
    cout << right << strg3 << endl;
    return 0;
}
```

```text
Run:
Enter the first big integer: 346786543098762378
Enter the second big integer: 78654329876

First big integer          346786543098762378 +
Second big integer              78654329876
                           --------------------------
Result                    346786621753092254

Run:
Enter the first big integer: 3478654212345690
Enter the second big integer: 7654329876543567

First big integer             3478654212345690 +
Second big integer             7654329876543567
                              --------------------------
Result                       11132984088880257

Run:
Enter the first big integer: 356709876567
Enter the second big integer: 19283848484848987654356

First big integer                 356709876567 +
Second big integer            19283848484848987654356
                                --------------------------
Result                       19283848485205697530923
```

In the first run, the first integer is longer; in the second run, the two integers are of equal length and create an extra carry; in the third run, the first integer is shorter.
