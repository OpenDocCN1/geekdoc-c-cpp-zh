

## 21.4 子字符串

`string` 类提供成员函数 `substr`，用于从一个 `string` 中获取子字符串。结果是一个从源 `string` 复制而来的新 `string` 对象。**图 21.3**演示了 `substr`。程序在第 8 行声明并初始化了一个 `string`。第 12 行使用成员函数 `substr` 从 `string1` 中获取子字符串。第一个参数指定所需子字符串的*起始下标*；第二个参数指定子字符串的*长度*。

```cpp
// Fig. 21.3: Fig21_03.cpp
// Demonstrating string member function substr.
#include <iostream>
#include <string>
using namespace std;

int main() {
    string string1{"The airplane landed on time."};

    // retrieve substring "plane" which
    // begins at subscript 7 and consists of 5 characters
    cout << string1.substr(7, 5) << endl;
}
```

```text
plane
```

图 21.3 演示 `string` 成员函数 `substr`。

## 21.5 交换 `string`

`string` 类提供成员函数 `swap`，用于交换 `string`。**图 21.4**交换了两个 `string`。第 8～9 行声明并初始化了 `string` `first` 和 `second`。随后输出每个 `string`。第 14 行使用 `string` 成员函数 `swap` 交换 `first` 和 `second` 的值。程序再次输出这两个 `string`，以确认它们确实已经交换。`string` 成员函数 `swap` 对实现字符串排序的程序很有用。

```cpp
// Fig. 21.4: Fig21_04.cpp
// Using the swap function to swap two strings.
#include <iostream>
#include <string>
using namespace std;

int main() {
    string first{"one"};
    string second{"two"};

    // output strings
    cout << "Before swap:\n first: " << first << "\nsecond: " << second;

    first.swap(second); // swap strings

    cout << "\n\nAfter swap:\n first: " << first
         << "\nsecond: " << second << endl;
}
```

```text
Before swap:
  first: one
  second: two

After swap:
  first: two
  second: one
```

图 21.4 使用 `swap` 函数交换两个 `string`。

## 21.6 `string` 的特性

`string` 类提供成员函数，用于获取 `string` 的*大小、长度、容量、最大长度*以及其他特性。`string` 的大小或*长度*是当前存储在 `string` 中的字符数。`string` 的**容量**是在不分配更多内存的情况下，可以存储在 `string` 中的字符数。`string` 的容量必须至少等于其当前大小，但也可以大于当前大小。`string` 的确切容量取决于具体实现。**最大大小**是 `string` 可能具有的最大大小。如果超过该值，就会抛出 `length_error` 异常。**图 21.5**演示了用于确定 `string` 各种特性的 `string` 类成员函数。

```cpp
// Fig. 21.5: Fig21_05.cpp
// Printing string characteristics.
#include <iostream>
#include <string>
using namespace std;

void printStatistics(const string&);

int main() {
    string string1; // empty string

    cout << "Statistics before input:\n" << boolalpha;
    printStatistics(string1);

    // read in only "tomato" from "tomato soup"
    cout << "\n\nEnter a string: ";
    cin >> string1; // delimited by whitespace
    cout << "The string entered was: " << string1;

    cout << "\nStatistics after input:\n";
    printStatistics(string1);

    // read in "soup"
    cin >> string1; // delimited by whitespace
    cout << "\n\nThe remaining string is: " << string1 << endl;
    printStatistics(string1);

    // append 46 characters to string1
    string1 += "1234567890abcdefghijklmnopqrstuvwxyz1234567890";
    cout << "\n\nstring1 is now: " << string1 << endl;
    printStatistics(string1);

    // add 10 elements to string1
    string1.resize(string1.size() + 10);
    cout << "\n\nStats after resizing by (length + 10):\n";
    printStatistics(string1);
    cout << endl;
}

// display string statistics
void printStatistics(const string& stringRef) {
    cout << "capacity: " << stringRef.capacity() << "\nmax size: "
         << stringRef.max_size() << "\nsize: " << stringRef.size()
         << "\nlength: " << stringRef.size()
         << "\nempty: " << stringRef.empty() << endl;
}
```

```text
Statistics before input:
capacity: 15
max size: 4294967294
size: 0
length: 0
empty: true

Enter a string: tomato soup
The string entered was: tomato
Statistics after input:
capacity: 15
max size: 4294967294
size: 6
length: 6
empty: false

The remaining string is: soup
capacity: 15
max size: 4294967294
size: 4
length: 4
empty: false

string1 is now: soup1234567890abcdefghijklmnopqrstuvwxyz1234567890
capacity: 63
max size: 4294967294
size: 50
length: 50
empty: false

Stats after resizing by (length + 10):
capacity: 63
max size: 4294967294
size: 60
length: 60
empty: false
```

**图 21.5**输出 `string` 的特性。

程序声明了一个空的 `string string1`（第 10 行），并将其传递给函数 `printStatistics`（第 13 行）。函数 `printStatistics`（第 41～46 行）接收一个 `const string` 的引用作为参数，并输出容量（使用成员函数 `capacity`）、最大大小（使用成员函数 `max_size`）、大小（使用成员函数 `size`）、长度（使用成员函数 `size`），以及 `string` 是否为空（使用成员函数 `empty`）。对 `printStatistics` 的初始调用表明，`string1` 的初始大小和长度值为 `0`。

大小和长度为 `0` 表明 `string` 中没有存储任何字符。请注意，大小和长度始终相同。在此实现中，最大大小为 4,294,967,294。对象 `string1` 是一个空的 `string`，因此函数 `empty` 返回 `true`。

第 17 行输入一个字符串。在本例中，输入的是 `"tomato soup"`。由于空格字符是分隔符，因此只有 `"tomato"` 被存储在 `string1` 中；但是，`"soup"` 仍保留在输入缓冲区中。第 21 行调用函数 `printStatistics`，输出 `string1` 的统计信息。请注意输出结果，其中长度为 `6`，容量为 `15`。

第 24 行从输入缓冲区读取 `"soup"`，并将其存储到 `string1` 中，从而替换 `"tomato"`。第 27 行将 `string1` 传递给 `printStatistics`。

第 29 行使用*重载的* `+=` 运算符，将一个长度为 46 个字符的字符串连接到 `string1`。第 31 行将 `string1` 传递给 `printStatistics`。容量增加到了 63 个元素，长度现在为 50。

第 34 行使用成员函数 `resize` 将 `string1` 的长度增加 10 个字符。新增元素被设置为空字符。输出结果显示，容量*没有*改变，而长度现在为 60。

## 21.7 在 `string` 中查找子字符串和字符

`string` 类提供用于在 `string` 中查找子字符串和字符的 `const` 成员函数。**图 21.6**演示了 `find` 函数。

```cpp
// Fig. 21.6: Fig21_06.cpp
// Demonstrating the string find member functions.
#include <iostream>
#include <string>
using namespace std;

int main() {
   string string1{"noon is 12 pm; midnight is not."};
   int location;

   // find "is" at location 5 and 24
   cout << "Original string:\n" << string1
        << "\n\n(find) \"is\" was found at: " << string1.find("is")
        << "\n(rfind) \"is\" was found at: " << string1.rfind("is");

   // find 'o' at location 1
   location = string1.find_first_of("misop");
   cout << "\n\n(find_first_of) found: " << string1[location]
        << " from the group \"misop\" at: " << location;

   // find 'o' at location 28
   location = string1.find_last_of("misop");
   cout << "\n\n(find_last_of) found: " << string1[location]
        << " from the group \"misop\" at: " << location;

   // find '1' at location 8
   location = string1.find_first_not_of("noi spm");
   cout << "\n\n(find_first_not_of) \"" << string1[location]
        << "\" is not contained in \"noi spm\" and was found at:"
        << location;

   // find ' ' at location 13
   location = string1.find_first_not_of("12noi spm");
   cout << "\n\n(find_first_not_of) " << string1[location]
        << " is not contained in \"12noi spm\" and was "
        << "found at: " << location << endl;

   // search for characters not in string1
   location = string1.find_first_not_of(
      "noon is 12 pm; midnight is not.");
   cout << "\n\n(find_first_not_of)(\"noon is 12 pm; midnight is not.\")"
        << " returned: " << location << endl;
}
```

