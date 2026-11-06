

```cpp
// Fig. 21.1: Fig21_01.cpp
// Demonstrating string assignment and concatenation.
#include <iostream>
#include <string>
using namespace std;

int main() {
   string string1{"cat"};
   string string2; // initialized to the empty string
   string string3; // initialized to the empty string

   string2 = string1; // assign string1 to string2
   string3.assign(string1); // assign string1 to string3
   cout << "string1: " << string1 << "\nstring2: " << string2
      << "\nstring3: " << string3 << "\n\n";

   // modify string2 and string3
   string2[0] = string3[2] = 'r';

   cout << "After modification of string2 and string3:\n" << "string1: "
      << string1 << "\nstring2: " << string2 << "\nstring3: "
      << string3 << '\n';

   // demonstrating member function at
   for (size_t i{0}; i < string3.size(); ++i) {
      cout << string3.at(i); // can throw out_of_range exception
   }

   // declare string4 and string5
   string string4{string1 + "apult"}; // concatenation
   string string5{}; // initialized to the empty string

   // overloaded +=
   string3 += "pet"; // create "carpet"
   string1.append("acomb"); // create "catacomb"

   // append subscript locations 4 through end of string1 to
   // create string "comb" (string5 was initially empty)
   string5.append(string1, 4, string1.size() - 4);

   cout << "\n\nAfter concatenation:\n" << "string1: " << string1
      << "\nstring2: " << string2 << "\nstring3: " << string3
      << "\nstring4: " << string4 << "\nstring5: " << string5 << endl;
}
```

```
string1: cat
string2: cat
string3: cat

After modification of string2 and string3:
string1: cat
string2: rat
string3: car
```

## 图 21.1 演示 `string` 赋值和连接。

第 18 行使用下标运算符将 `'r'` 赋给 `string3[2]`（形成 `"car"`），并将 `'r'` 赋给 `string2[0]`（形成 `"rat"`）。然后输出这些 `string`。

第 24–26 行使用成员函数 `at` 逐字符输出 `string3` 的内容。成员函数 `at` 提供**检查访问**（或**范围检查**）；也就是说，越过 `string` 的末尾会抛出 `out_of_range` 异常。*下标运算符 `[]` 不提供检查访问。* 这与它在数组上的使用是一致的。请注意，你还可以使用 C++11 的基于范围的 `for` 遍历字符串中的字符，如下所示：

```cpp
for (char c : string3) {
    cout << c;
}
```

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2455_0.png)

### 常见编程错误 21.1

*使用下标运算符访问 `string` 边界之外的元素是未定义的逻辑错误。*

`string4` 在第 29 行声明，并初始化为使用*重载的* `+` *运算符*将 `string1` 和 "apult" 连接的结果，对于类 `string`，该运算符表示*连接*。第 33 行使用*重载的加赋值运算符* `+=` 连接 `string3` 和 "pet"。第 34 行使用成员函数 `append` 连接 `string1` 和 "acomb"。

第 38 行将字符串 "comb" 追加到空的 `string string5`。这个成员函数接收要从中检索字符的字符串（`string1`）、`string` 中的起始下标（4）以及要追加的字符数（由 `string1.size() - 4` 返回的值）。

## 21.3 比较 `strings`

类 `string` 提供了用于比较 `string` 的成员函数。

**图 21.2** 演示了类 `string` 的比较功能。

```cpp
// Fig. 21.2: Fig21_02.cpp
// Comparing strings
#include <iostream>
#include <string>
using namespace std;

int main() {
    string string1{"Testing the comparison functions."};
    string string2{"Hello"};
    string string3{"string"};
    string string4{string2}; // "Hello"

    cout << "string1: " << string1 << "\nstring2: " << string2
         << "\nstring3: " << string3 << "\nstring4: " << string4 << "\n\n";

    // comparing string1 and string4
    if (string1 == string4) {
        cout << "string1 == string4\n";
    }
    else if (string1 > string4) {
        cout << "string1 > string4\n";
    }
    else { // string1 < string4
        cout << "string1 < string4\n";
    }

    // comparing string1 and string2
    int result{string1.compare(string2)};

    if (result == 0) {
        cout << "string1.compare(string2) == 0\n";
    }
    else if (result > 0) {
        cout << "string1.compare(string2) > 0\n";
    }
    else { // result < 0
        cout << "string1.compare(string2) < 0\n";
    }

    // comparing string1 (elements 2-5) and string3 (elements 0-5)
    result = string1.compare(2, 5, string3, 0, 5);

    if (result == 0) {
        cout << "string1.compare(2, 5, string3, 0, 5) == 0\n";
    }
    else if (result > 0) {
        cout << "string1.compare(2, 5, string3, 0, 5) > 0\n";
    }
    else { // result < 0
        cout << "string1.compare(2, 5, string3, 0, 5) < 0\n";
    }

    // comparing string2 and string4
    result = string4.compare(0, string2.size(), string2);

    if (result == 0) {
        cout << "string4.compare(0, string2.size(), string2) == 0\n";
    }
    else if (result > 0) {
        cout << "string4.compare(0, string2.size(), string2) > 0\n";
    }
    else { // result < 0
        cout << "string4.compare(0, string2.size(), string2) < 0\n";
    }

    // comparing string2 and string4
    result = string2.compare(0, 3, string4);

    if (result == 0) {
        cout << "string2.compare(0, 3, string4) == 0\n";
    }
    else if (result > 0) {
        cout << "string2.compare(0, 3, string4) > 0\n";
    }
    else { // result < 0
        cout << "string2.compare(0, 3, string4) < 0\n";
    }
}
```

```
string1: Testing the comparison functions.
string2: Hello
string3: string
string4: Hello

string1 > string4
string1.compare(string2) > 0
string1.compare(2, 5, string3, 0, 5) == 0
string4.compare(0, string2.size(), string2) == 0
string2.compare(0, 3, string4) < 0
```

图 21.2 比较 `string`。

程序声明了四个 `string`（第 8–11 行）并输出每一个（第 13–14 行）。第 17 行使用*重载的相等运算符*测试 `string1` 与 `string4` 是否相等。如果条件为 `true`，则输出 `"string1 == string4"`。如果条件为 `false`，则测试第 20 行的条件。所有 `string` 类重载的关系运算符和相等运算符函数都返回 `bool` 值。

第 28 行使用 `string` 成员函数 **compare** 将 `string1` 与 `string2` 进行比较。如果这些 `string` 相等，则变量 `result` 被赋值为 `0`；如果 `string1` **按字典序**大于 `string2`，则被赋值为*正数*；如果 `string1` *按字典序*小于 `string2`，则被赋值为*负数*。当我们说一个 `string` *按字典序*小于另一个时，我们的意思是 **compare** 成员函数使用每个 `string` 中字符的数值（参见**附录 B**，ASCII 字符集）来确定第一个 `string` 小于第二个。lexicon 是字典的意思。因为以 `'T'` 开头的 `string` 被认为按字典序大于以 `'H'` 开头的字符串，所以 `result` 被赋值为大于 `0` 的值，正如输出所确认的那样。

第 41 行使用成员函数 **compare** 的一个*重载*版本比较 `string1` 和 `string3` 的部分内容。前两个参数（`2` 和 `5`）指定要与 `string3` 比较的 `string1` 部分的*起始下标*和*长度*。第三个参数是比较 `string`。最后两个参数（`0` 和 `5`）是被比较的 `comparison string` 部分的*起始下标*和*长度*（同样为 `"string"`）。赋给 `result` 的值：相等时为 `0`；如果 `string1` *按字典序*大于 `string3`，则为正数；如果 `string1` *按字典序*小于 `string3`，则为负数。这里比较的两个部分是相同的，因此 `result` 被赋值为 `0`。

第 54 行使用函数 `compare` 的另一个*重载*版本来比较 `string4` 和 `string2`。前两个参数相同——*起始下标*和*长度*。最后一个参数是比较 `string`。返回值也相同——相等时为 `0`；如果 `string4` *按字典序*大于 `string2`，则为正数；如果 `string4` *按字典序*小于 `string2`，则为负数。因为这里比较的两个 `string` 部分是相同的，所以 `result` 被赋值为 `0`。

第 67 行调用成员函数 `compare` 将 `string2` 中前 `3` 个字符与 `string4` 进行比较。因为 `"Hel"` 小于 `"Hello"`，所以返回一个小于零的值。

