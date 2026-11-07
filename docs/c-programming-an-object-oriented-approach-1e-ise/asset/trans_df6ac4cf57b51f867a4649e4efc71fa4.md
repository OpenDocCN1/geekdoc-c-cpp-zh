
## 程序 10.20 字符串的整数比较（续）

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
运行：
Hello my friends compared with Hello friends: 1
Hello compared with Hello: 0
Hello compared with Hello: -8
Hel compared with Hell: -1
```

我们来检查结果：

- 1. 在第一次比较中（第 15 行），我们比较的是“Hello my friends”和“Hello friends”。比较会逐个字符进行，直到将字符‘m’与字符‘f’进行比较。字符‘m’大于字符‘f’，比较停止，函数返回 1（一个正数）。
- 2. 在第二次比较中（第 18 行），我们比较的是“Hello”和“Hello”。两个子字符串相等，因此结果为 0。
- 3. 在第三次比较中（第 21 行），我们比较的是“Hello”和“Hello friends”。空字符与空格进行比较。结果为负数（−8）。
- 4. 在第四次比较中（第 24 行），我们比较的是“Hel”和“Hell”。当比较到第四个字符时，实际上是在比较空字符和字符‘l’。结果为负数（−1）。

在整数比较中，我们必须注意不能将整数结果转换为布尔类型，因为 1 和 −1 都会被转换为 true，这样做是不正确的。

### 逻辑比较

逻辑比较会比较两个字符串，并返回一个布尔值（*true* 或 *false*）。与整数比较一样，逻辑比较也会比较两个字符串。第一个字符串始终是宿主字符串，第二个字符串可以是 C++ 字符串或 C 字符串。与整数比较不同，我们不能比较两个子字符串。如果确实需要这样做，就必须根据子字符串创建临时 C++ 字符串，然后再对它们进行比较。

这些原型使用了运算符重载，我们将在第 13 章讨论这一内容。原型中的 Oper 可以是关系运算符或相等运算符（<、<=、>、>=、== 或 !=）中的任何一个。我们可以使用这些运算符来比较两个字符串，就像它们是基本类型一样。你可能会想，我们是否可以比较两个 C 字符串。我们可以这样做，但 C 字符串会被视为基本类型，并且会对它们应用普通的关系运算符和相等运算符（不需要 `<string>` 头文件）。请注意，在逻辑比较中，两个字符串中的一个必须是 C++ 字符串。

下面展示了如何使用这些成员函数。

```cpp
bool result = strg1 oper strg2;      // Comparing two C++ strings
bool result = strg oper str;         // Comparing a C++ string and a C string
bool result = str oper strg;         // Comparing a C string and a C++ string
```

## 示例 10.21

程序 10.21 比较字符串。

### 程序 10.21 使用逻辑运算符比较字符串

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
运行：
strg1 < strg2 : true
strg2 >= strg3: true
strg2 < strg3: false
strg1 == strg2: false
Hi P != strg4: false
```

## 示例 10.22

如果一个字符串正读和反读都相同，那么它就是回文。字符串“rotor”、“dad”和“noon”都是回文。更复杂的回文示例包括“Madam, I am Adam”和“Able was I ere I saw Elba”。通过将字符串与其反转形式进行比较，我们可以轻松检查一个字符串是否为回文。在某些情况下，我们必须先删除标点符号，并将所有字符统一为相同形式，然后再反转字符串。程序 10.22 展示了如何检查字符串是否为回文。

### 程序 10.22 检查回文

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
运行：
输入一个字符串：rotor
rotor 是回文。
```

```text
运行：
输入一个字符串：mom
mom 是回文。
```

```text
运行：
输入一个字符串：son
son 不是回文。
```

### Push_Back

我们经常需要向字符串中添加字符。字符串库定义了 *push_back* 函数，它会将一个字符添加到字符串末尾。可以按如下方式使用该库成员函数：

```cpp
strg.push_back (c);           // Append character c at the end of strg
```

在程序设计部分，我们将展示如何在字符串的前面添加字符，同时也会展示如何从字符串的前端或后端弹出字符。

### 修改操作

C++ 字符串库为修改操作提供了一组不同的函数定义。不过，如果我们将临时字符串构造为参数，就可以将成员函数的数量减少为四类。字符串 *temp* 是我们要查找的字符集合。

```cpp
temp (strg);                // A complete C++ string
temp (strg, pos2, n2);      // A part of C++ string
temp (1, c);                // A string made of one character
temp (cstr);                // A complete C-string
temp (cstr, n);             // The first n characters of a C-string
```

![](img/d68f6199646ca63591a6d8419e0ed4ba_499_0.png)

**图 10.12** append、insert、replace 和 assign 背后的基本思想

图 10.12 展示了四组函数如何使用临时字符串来修改宿主字符串。

下面展示了如何使用这四类函数：

```cpp
strg.append (temp);        // Append
strg.insert (pos1, temp);  // Insert
strg.replace (pos1, n1, temp); // Replace
strg.assign (temp);        // Assign
```

### 部分或全部擦除

有两个函数可以在不销毁字符串的情况下，全部或部分擦除字符串中的字符。对象仍然存在，但其中的字符可能被部分或全部删除。

```cpp
strg.clear ();             // Erase all character in the string
strg.erase (pos, n);       // Erase part of the string
```

### 重载运算符

一些修改操作是通过重载运算符实现的。C++ 对赋值运算符（=）、复合赋值运算符（+=）和加法运算符（+）进行了重载，如下所示。*temp*、*temp1* 和 *temp2* 是 *string* 类的实例。

```cpp
string strg = temp;        // Assignment
string strg += temp;       // Compound Assignment
string strg = temp1 + temp2; // Addition
```
