
## 程序 19.6 打印列表元素（续）

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

我们可以重写程序 19.2，而不使用 + 或 − 运算符，因为这些运算符并未为双向迭代器定义。程序 19.7 给出了一种解决方案。

## 程序 19.7 打印列表中的一些元素

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

我们创建一个大整数类，它可以处理任意位数的整数。我们只提供两个大整数的加法运算。程序 19.8 展示了一个简单大整数类的接口，该类只包含加法（+）运算。我们使用一个列表，其中每个元素保存一位数字。另一种解决方案是让每个元素保存三位或六位数字，但编码会更复杂。

## 程序 19.8 文件 bigInteger.h

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

程序 19.9 展示了大整数类的实现文件。我们编写了两个构造函数、一个析构函数、一个加法运算符，以及一个名为 toString() 的成员函数。在计算机编程中，通常会定义一个 toString 函数，它从值创建字符串对象，以便该对象可以导出到其他程序。

## 程序 19.9 文件 bigInteger.cpp

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

在程序 19.9 中，默认构造函数创建一个空列表。带参构造函数接受一个表示大整数的字符串，例如“4572349876509”，逐个提取其中的数字作为 ASCII 字符，从 ASCII 字符的整数值中减去 48 来得到一个数字，然后将其推入列表的后部。注意，字符是从字符串的前部复制的，但被推入列表的后部。下一个数字会把列表后部的数字向前推。当实例化大整数对象时，我们就得到一个整数列表，其中每个元素保存一位数字。

下一个成员函数是 toString() 函数，它执行相反的操作。它逐个从列表中复制数字，并将它们追加到字符串中。

实现的核心是友元 operator+() 函数，它接受两个大整数对象，从右往左逐位相加，并生成和与进位。我们需要使用三个 while 循环。如果两个列表大小相同，第一个循环即可完成工作。如果其中一个列表已经遍历完，则另外两个循环之一会继续。注意，如果两个列表都已遍历完，最后相加的两位数字仍可能产生进位；末尾的 if 语句会处理这种情况。程序 19.10 展示了一个使用我们的 BigInteger 类的示例应用程序。

## 程序 19.10 应用程序文件（app.cpp）

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

在第一次运行中，第一个整数更长；在第二次运行中，两个整数长度相等，并产生一个额外进位；在第三次运行中，第一个整数更短。

