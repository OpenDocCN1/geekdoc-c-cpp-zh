
#include <iostream>
#include <string>

using namespace std;

int main()
{
    string s1("Road");
    string s2("Read");
    string s3("Red");
    cout << "s1 = " << s1 << "\n";
    cout << "s2 = " << s2 << "\n";
    cout << "s3 = " << s3 << "\n";

    int x = s1.compare(s2);
    if (x == 0)
        cout << "s1 == s2\n";
    else if (x > 0)
        cout << "s1 > s2\n";
    else
        cout << "s1 < s2\n";

    int a = s1.compare(0, 2, s2, 0, 2);
    int b = s2.compare(0, 2, s1, 0, 2);
    int c = s2.compare(0, 2, s3, 0, 2);
    int d = s2.compare(s2.size() - 1, 1, s3, s3.size() - 1, 1);

    cout << "a = " << a << "\n";
    cout << "b = " << b << "\n";
    cout << "c = " << c << "\n";
    cout << "d = " << d << "\n";

    cout << "\nBefore swap:\n";
    cout << "s1 = " << s1 << "\n";
    cout << "s2 = " << s2 << "\n";

    s1.swap(s2);

    cout << "\nAfter swap:\n";
    cout << "s1 = " << s1 << "\n";
    cout << "s2 = " << s2 << "\n";

    return 0;
}
The output of Program 15.6 would be:

exchanges the contents of the strings s1 and s2.

# Summary

+   Manipulation and use of C-style strings become complex and inefficient. ANSI C++ provides a new class called **string** to overcome the deficiencies of C-strings.

+   The string class supports many constructors, member functions and operators for creating and manipulating string objects. We can perform the following operations on the strings:
    + Reading strings from keyboard
    + Assigning strings to one another
    + Finding substrings
    + Modifying strings
    + Comparing strings and substrings
    + Accessing characters in strings
    + Obtaining size and capacity of strings
    + Swapping strings
    + Sorting strings

# Key Terms

<string> | append() | assign() | at() | begin() | capacity | **capacity()**  
| **compare()** | comparing strings | 'C-strings' | 'C-style strings' |  
**empty()** | **end()** | **erase()** | **find()** | **find_first_of()** | **find_last_of()** |  
**getline()** | **insert()** | length | **length()** | lexicographical | **max_size()**  
| maximum size | relational operators | **replace()** | size | **size()** |  
string | 'string class' | 'string constructors' | 'string objects' | **substr()** |  
substring | **swap()** | swapping strings

# Review Questions

**15.1** State whether the following statements are TRUE or FALSE:

+   (a) For using **string** class, we must include the header `<string>`.  
+   (b) **string** objects are null terminated.  
+   (c) The elements of a **string** object are numbered from 0.  
+   (d) Objects of **string** class can be copied using the assignment operator.  
+   (e) Function **end()** returns an iterator to the invoking **string** object.

**15.2** How does a **string** type string differ from a C-type string?

**15.3** The following statements are available to read strings from the keyboard.

+   (a) `cin >> s1;`  
+   (b) `getline(cin, s1);`

where **s1** is a **string** object. Distinguish their behaviour.

**15.4** Consider the following segment of a program:

```
string s1("man"), s2, s3;
s2.assign(s1);
s3 = s1;
string s4("wo" + s1);
s2 += "age";
s3.append("ager");
s1[0] = 'v';
```

State the contents of the objects s1, s2, s3 and s4 when executed.

# 15.5 We can access string elements using

+   (a) **at()** function
+   
+   (b) subscript operator [ ]

Compare their behaviour.

# 15.6 What does each of the following statements do?

+   (a) `s.replace(n,1,"/");`
+   
+   (b) `s.erase(10);`
+   
+   (c) `s1.insert(10,s2);`
+   
+   (d) `int x = s1.compare(0, s2.size(), s2);`
+   
+   (e) `s2 = s1.substr(10, 5);`

# 15.7 Distinguish between the following pair of functions.

+   (a) max_size() and capacity()
+   
+   (b) find() and rfind()
+   
+   (c) begin() and rbegin()

# Debugging Exercises

[PAGE 645]

# 15.1 Identify the error in the following program.

```
#include <iostream.h>
#include <string>

using namespace std;

void main()
{
string str1("ghi");
string str2("abc" + "def");
str2+=str1;
cout << str2.c_str();
}
```

# 15.2 Identify the error in the following program.

```
#include <iostream.h>
#include <string>
using namespace std;
void main()
{
string str1("ABCDEF");
string str2("123");
string str3;
str1.insert(2, str2);
str1.erase(2,2);
str1.replace(2,str2);
cout << str1.c_str();
cout << endl;
}
```

# 15.3 Identify the error in the following program.

```
#include <iostream>
#include <string>
using namespace std;
class Product
```

[PAGE 646]

```
{
int iProductNumber;
string strProductName;
public:
Product()
{
}
Product(const int &number, const string &name)
{
setProductNumber(number);
setProductName(name);
}
void setProductNumber(int n)
{
iProductNumber = n;
}
void setProductName(const string str)
{
strProductName = str;
}
int getProductNumber()
{
return iProductNumber;
}
const string getProductName()
{
return strProductName ;
}
}
Products operator = (Product &source)
{
setProductNumber(source.iProductNumber);
string strTemp = source.strProductName;
setProductName(strTemp);
return *this;
}
void display()
{
}
```

[PAGE 647]

```
cout << "ProductName : " << getProductName();
cout << " " ;
cout << "ProductNumber : " << getProductNumber();
cout << endl;
}
void main()

{

404 Object Oriented Programming with C++

Product p1(1, 5);
Product p2(3, “Dates”);
Product p3;
p3 = p2 = p1;
p3.display();
p2.display();
```

15.4 Find errors, if any, in the following segment of code.

```
int len = sl. length();
for (int i=0; 1<len;++1)
cout << sl.at[];
```
```

[PAGE 648]

15.1 Write a program that reads the name

Martin Luther King

from the keyboard into three separate string objects and then concatenates them into a new string object using

+   (a) + operator and
+   (b) **append()** function

15.2 Write a program using an iterator and **while()** construct to display the contents of a **string** object.

15.3 Write a program that reads several city names from the keyboard and displays only those names beginning with characters “B” or “C”.

15.4 Write a program that will read a line of text containing more than three words and then replace all the blank spaces with an underscore(_).

15.5 Write a program that counts the number of occurrences of a particular character, say ‘e’, in a line of text.

15.6 Write a program that reads the following text and counts the number of times the word “It” appears in it.

> It is new. It is singular.
> It is simple. It must succeed!

15.7 Modify the program in Exercise 15.6 to count the number of words which start with the character ’s’.

15.8 Write a program that reads a list of countries in random order and displays them in alphabetical order. Use comparison operators and functions.

15.9 Given a string

string s(“123456789”); Write a program that displays the following:

```
1
2 3   2
3 4 5     4 3
4 5 6 7   6 5 4
5 6 7 8 9 8 7 6 5
```
```

