
Replace Middle 3 Characters in S2 with S1

Now S2: `a12345e`

# 15.4 关系运算

为字符串对象定义了许多在字符串上使用的运算符（表 15.3）。我们在之前的示例中使用了运算符 `=` 和 `+` 来创建对象。我们也可以应用表 15.3 中列出的关系运算符。这些运算符被重载，可用于比较字符串对象。`compare()` 函数也可以用于此目的。

## 使用 C++ 进行面向对象编程

程序 15.3 显示了这些运算符的使用方法。

### 程序 15.3 字符串对象的关系运算

```
#include<iostream>
#include <string>
using namespace std;
int main()
{
    string s1="ABC";
    string s2="XYZ";
    string s3 = s1 + s2;

    if(s1!=s2)
        cout<<s1<<" is not equal to "<<s2<<"\n";

    if(s1<s2)
        cout<<s1<<" is greater than "<<s2<<"\n";
    else
        cout<<s2<<" is greater than "<<s1<<"\n";

    if(s3==s1+s2)
        cout<<s3<<" is equal to "<<s1+s2<<"\n";

    int x = s1.compare(s2);
    if(x==0)
        cout<<s1<<" = "<<s2<<"\n";
    else if(x>0)
        cout<<s1<<" > "<<s2<<"\n";
    else
        cout<<s1<<" < "<<s2<<"\n";

    return 0;
}
```

程序 15.3 的输出为：

```
ABC is not equal to XYZ
XYZ is greater than ABC
ABCXYZ is equal to ABCXYZ

ABC < XYZ
```

### 15.5 字符串特征

`string` 类支持许多可用于获取字符串特征的函数，如 `size`、`length`、`capacity` 等。大小或长度表示给定字符串中当前存储的元素数量。容量表示给定字符串中可以存储的总元素数。另一个特征是最大大小，即系统可以支持的字符串对象的最大可能大小。程序 15.4 说明了如何获取这些特征并在应用程序中使用它们。

### 程序 15.4 获取字符串特征

```
#include <iostream>
#include <string>

using namespace std;

void display(const string &str) {
    cout << "Size = " << str.size() << "\n";
    cout << "Length = " << str.length() << "\n";
    cout << "Capacity = " << str.capacity() << "\n";
    cout << "Maximum Size = " << str.max_size() << "\n";
    cout << "Empty: " << (str.empty() ? "yes" : "no");
    cout << "\n";
}

int main() {
    string strl;

    cout << "Initial status: \n";
    display(strl);

    cout << "Enter a string (one word) \n";
    cin >> strl;
    cout << "Status now: \n";
    display(strl);

    strl.resize(15);
    cout << "Status after resizing: \n";
    display(strl);
    cout << "\n";

    return 0;
}
```

程序 15.4 的输出为：

Initial status:

Size = 0

Length = 0

Capacity = 0

Maximum Size = 4294967295

Empty: yes

Enter a string (one word)

INDIA

Status now:

Size = 5

Length = 5

Capacity = 31

## 使用 C++ 进行面向对象编程

Maximum Size = 4294967293

Empty: no

Status after realloc:

Size is same

Length = 15

Capacity = 31

Maximum Size = 4294967293

Empty: no

## 限制

C++ 在字符串中支持 509 个字符，这取决于编译器，如 MSVC 支持 2048，GCC 无限制，在 511 个字符后显示警告。

大小和长度为 0 表示字符串不包含字符。大小和长度始终相同。`str` 最初的容量为零，但在将字符串分配给它时，其容量已增加到 31。此系统中字符串的最大大小为 4294967293。`empty()` 函数如果字符串为空则返回 true；否则返回 false。

### 15.6 访问字符串中的字符

我们可以通过多种方式访问字符串的子字符串和单个字符。`string` 类支持以下函数用于此目的：

- `at()` 用于访问单个字符
- `substr()` 用于检索子字符串
- `find()` 用于查找指定的子字符串
- `find_first_of()` 用于查找指定字符的首次出现位置
- `find_last_of()` 用于查找指定字符的最后一次出现位置

我们还可以使用重载的 `[]` 运算符（使字符串对象看起来像数组）来访问字符串中的单个元素。程序 15.5 演示了这些函数的使用。

### 程序 15.5 访问和操作字符

```
#include <iostream>
#include <string>

using namespace std;
int main()
{
    string s("ONE TWO THREE FOUR");
    cout << "The string contains: " << s.length() << "\n";
    for(int i=0;i<s.length(); i++)
        cout << s.at(i) << "    "; // Display one character

    cout << "\nString is shown again: " << s << "\n";
    for(int j=0;j<s.length(); j++)
        cout << s[j] << " ";

    cout << "\nTWO is found at: " << x1 << "\n";
}

int x2 = s.find_first_of('T');
cout << "\nT is found first at: " << x2 << "\n";
int x3 = s.find_last_of('R');
cout << "\nR is last found at: " << x3 << "\n";

cout << "\nRetrieve and print substring TWO \n";

cout << s.substr(x1,3);
cout << "\n";

return 0;
}
```

程序 15.5 的输出为：

The string contains:

ONE TWO THREE FOUR

String is shown again:

ONE TWO THREE FOUR

TWO is found at: 4

T is found first at: 4

R is last found at: 17

Retrieve and print substring

TWO

我们可以使用成员函数 `at()` 或下标运算符 `[ ]` 访问字符串中的单个字符。这由以下语句说明：

`cout << s.at(i);`

`cout << s[i];`

语句

`int x1 = s.find("TWO");`

定位 `"TWO"` 的第一个字符的位置。语句

`cout << s.substr(x1,3);`

查找子字符串 `"TWO"`。第一个参数 `x1` 指定所需子字符串的第一个字符的位置，第二个参数给出子字符串的长度。

### 15.7 比较和交换

`string` 支持用于比较和交换字符串的函数。`compare()` 函数可用于比较两个字符串或字符串的部分。`swap()` 函数可用于交换两个字符串对象的内容。这些函数的功能在程序 15.6 中得到演示。

## 使用 C++ 进行面向对象编程

## 程序 15.6 比较和交换字符串

```
#include <iostream>
#include <string>

using namespace std;
int main() {
    string s1("Road");
    string s2("Read");
    string s3("Red");
    cout << "s1 = " << s1 << "\n";
    cout << "s2 = " << s2 << "\n";
    cout << "s3 = " << s3 << "\n";

    int x = s1.compare(s2);
    if (x == 0) {
        cout << "s1 = " << s2 << "\n";
    } else if (x > 0) {
        cout << "s1 = " << s2 << "\n";
    } else {
        cout << "s1 = " << s2 << "\n";
    }

    int a = s1.compare(0,2,s2,0,2);
    int c = s2.compare(0,2,s3,0,2);
    int d = s2.compare(s2.size()-1,s3,0,1);

    cout << "a = " << a << " "b = " << b << "\n";
    cout << "c = " << c << " "d = " << d << "\n";

    cout << "\nBefore swap: \n";
    cout << "s1 = " << s1 << "\n";
    cout << "s2 = " << s2 << "\n";
    s1.swap(s2);
    cout << "\nAfter swap: \n";
    cout << "s1 = " << s1 << "\n";
    cout << "s2 = " << s2 << "\n";

    return 0;
}
```

程序 15.6 的输出为：

```
s1 = Road
s2 = Read
s3 = Red
s1 > s2
a = 1
b = 0
c = 0
d = -1
```

Before swap:

s1 = Road

s2 = Read

After swap:

s1 = Read

s2 = Road

## 语句

```
int x = s1.compare(s2);
```

pares the string `s1` against `s2` and `x` is assigned 0 if the strings are equal, a positive number if `s1` is lexicographically greater than `s2` or a negative number otherwise.

## 语句

```
int a = s1.compare(0,2,s2,0,2);
```

pares of `s1` and `s2`, the first two arguments give the starting subscript and length of the position of `s1` to compare to `s2`, is supplied as the third argument. The fourth and fifth arguments specify the starting subscript and length of the position of `s2` to be compared. The value assigned to `a` is 0, if the strings are equal, 1 if substring of `s1` is greater than the substring of `s2`, -1 otherwise.

## 语句

```
s2.swap(s2);
```

exchanges the contents of the strings `s1` and `s2`.

## 摘要

- Manipulation and use of C-style strings become complex and inefficient. ANSI C++ provides a new class called `string` to overcome the deficiencies of C-strings.
- The `string` class supports many constructors, member functions and operators for creating and manipulating string objects. We can perform the following operations on the strings:
  - Reading strings from keyboard
  - Assigning strings to one another
  - Finding substrings
  - Modifying strings
  - Comparing strings and substrings
  - Accessing characters in strings
  - Obtaining size and capacity of strings
  - Swapping strings
  - Sorting strings

## 关键术语

`<string>` | `append()` | `assign()` | `at()` | `begin()` | `capacity` | `capacity()` | `compare()` | `comparing strings` | `C-strings` | `C-style strings` | `empty()` | `end()` | `erase()` | `find()` | `find_first_of()` | `find_last_of()` | `getline()` | `insert()` | `length` | `length()` | `lexicographical` | `max_size()` | `maximum size` | `relational operators` | `replace()` | `size` | `size()` | `string` | `string class` | `string constructors` | `string objects` | `substr()` | `substring` | `swap()` | `swapping strings`

## 复习问题

**认知领域**

- 15.1 Discriminate between string type `string` and a C-type string.
- 15.2 The following statements are available to read strings from the keyboard.
  (a) `cin >> s1;`
  (b) `getline(cin,s1);`
  where `s1` is a string object. Distinguish their behaviour.
- 15.4 We can access strings using elements
  (a) `at()` function
  (b) subscript operator `[]`
  Compare their behavior.
- 15.5 Compute the following statements:
  (a) `s.replace(n,1,"");`
  (b) `s.erase(10);`
  (c) `s1.insert(10,s2);`
  (d) `int x = s1.compare(0, s2.size(), s2);`
  (e) `s2 = s1.substr(10, 5);`

## Distinguish between the following pair of functions.

- (a) `max_size()` and `capacity()`
- (b) `find()` and `rfind()`
- (c) `begin()` and `rbegin()`

## 情感领域

- Defend the correctness of the following statements:
  (a) For using class, we must include the header `<string>`.
  (b) `string` objects are null terminated.
  (c) The elements of a `string` object are numbered from 0.
  (d) Objects of `string` class can be copied using the assignment operator.
  (e) Function `end()` returns an iterator to the invoking `string` object.

## 图例
