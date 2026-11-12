
标准模板库，或称 STL。STL 是一组可在程序中使用的数据类型。这些数据类型并非官方 C++ 语言的一部分，但已被添加到内置数据类型中。A.9 节讨论了诸如 STL 之类的库及其有用性。

要在程序中使用 vector，必须以以下语句开头：

```cpp
#include <vector>
using namespace std;
```

可以用三种方式声明 vector：

- 如果知道要在 vector 中包含多少个元素，可以将其持有的数据类型放在尖括号中，将元素个数放在圆括号中：

```cpp
vector<double> firstVector(10); // Vector to hold 10 doubles
vector<string> myVector(12); // Vector to hold 12 strings
```

声明 vector 时指定的大小仅为其初始大小。如您将看到，添加条目时，vector 可以增长。

- 声明 vector 时，可以通过编写第二个参数来放入初始值：

```cpp
vector<int> intVector(5, -1); // Vector to hold 5 integers, initialized to -1
```

分配 vector 中的元素时，它们会被赋予第二个参数的值。

- 也可以通过省略大小和圆括号来创建空 vector（即不含元素的 vector）：

```cpp
vector<char> letterVector; // An empty vector of characters
```

### 使用 [] 访问 vector 条目，就像访问数组一样

可以使用 [] 运算符存储或访问 vector 中的项，就像使用数组时一样。与数组一样，标识 vector 中元素的下标从 0 开始，到 s - 1 结束，其中 s 是 vector 的当前大小。以下语句是访问 vector 中现有值并更改现有条目值的示例：

```cpp
double x = firstVector[5]; // Places sixth entry in x
myVector[3] = "This is a sample string."; // Sets fourth entry's value
```

### size 返回 vector 中的元素数量

通过调用 size 方法，可以确定 vector 是否已满。这是 vector 相对于数组的一项重要优势。

如果 vector 已满或没有元素——也就是说，如果它是像之前的 letterVector 那样不带元素创建的——仍然可以使用 push_back 方法添加新值。push_back 方法接受一个参数，并将其添加到 vector 最后一个元素之后。换句话说，它将值推入 vector 的末尾。

### push_back 将其参数放入 vector 末尾的新元素中

此前，我们声明了一个可容纳 double 类型数据的十元素 vector firstVector。如果该 vector 已满，并且需要添加额外值 2.3 和 3.4，可以使用 push_back 方法：

```cpp
firstVector.push_back(2.3); // Grow vector and store value
firstVector.push_back(3.4); // Grow vector and store value
```

此时，调用 size 方法将返回 12，因为已向 vector 添加了两个额外元素。

### pop_back 从 vector 中移除最后一个元素

还可以通过移除 vector 的最后一个元素或所有元素来减小其大小。若仅移除最后一个元素，可以使用 pop_back 方法。该方法会缩短 vector，但不会返回被移除元素中的条目。必须在调用 pop_back 之前保存该条目。例如，以下语句确定 vector myVector 的当前大小，保存最后一个元素中的值，然后从 vector 中移除最后一个元素：

```cpp
int length = myVector.size(); // Find the current number of elements
string last = myVector[length - 1]; // Get the string in the last element
myVector.pop_back(); // subscripts start at 0
// Reduce the number of elements
```

随后调用 myVector.size() 将返回 length - 1，因为最后一个元素已被移除。

要移除 vector 中的所有元素并使其为空，请使用 clear 方法：

```cpp
myVector.clear(); // myVector is now an empty vector
```

vector 被清除后，必须使用 push_back 方法来添加新条目。

C++ 间奏曲 7 提供了关于 vector 的更多信息，包括这些方法和其他方法。

### clear 移除 vector 中的所有元素，使其大小为 0

## A.7 字符串

此前，您已看到 C++ 提供诸如下面这样的字符串字面量：

> "这是一个字符串。"

可以声明并使用包含此类字符串的变量，然后使用熟悉的运算符像操作整数一样自然地操作字符串。我们的介绍仅包含字符串可能操作中的一部分。

C++ 标准库提供了 string 数据类型。要使用此库，请在程序中包含以下语句：

```cpp
#include <string>
using namespace std;
```

在您的程序中。

可以声明一个名为 title 的 string 变量，并通过编写以下内容将其初始化为空字符串：

```cpp
string title;
```

声明 string 变量时，可以通过编写以下内容将其初始化为字符串字面量：

```cpp
string title = "Walls and Mirrors";
```

随后可以使用类似以下的赋值语句将另一个字符串赋给 title：

```cpp
title = "J Perfect's Day";
```

在上述每个示例中，title 的长度均为 17。可以使用 length 或 size 方法来确定字符串的当前长度。因此，title.length() 和 title.size() 均为 17。

可以使用与数组相同的索引表示法来引用字符串中的单个字符。因此，在上述示例中，title[0] 包含字符 J，title[16] 包含字符 y。

可以使用熟悉的比较运算符来比较字符串。不仅可以判断两个字符串是否相等，还可以发现两个字符串中哪一个排在前面。

两个字符串的排序类似于字母顺序排序，但使用的是 ASCII 表而非字母表。因此，以下关系均为真：

- "dig" < "dog"
- "Star" < "star"（因为 'S' < 's'）
- "start" > "star"
- "d" > "abc"

可以使用 + 运算符将两个字符串连接起来形成另一个字符串。也就是说，将一个字符串放在另一个字符串后面，形成另一个字符串。例如，如果

```cpp
string str1 = "Com";
```

以下语句

```cpp
string str2 = str1 + "puter";
str1 += "puter";
```

将字符串 "Computer" 赋给 str2 和 str1。同样，可以将单个字符追加到字符串，如

```cpp
str1 += 's';
```

可以使用 `substr(position, length)` 方法来操作字符串的一部分。

```cpp
substr(position, length)
```

第一个参数指定子字符串的起始位置（请记住，0 是字符串中第一个字符的位置）。第二个参数是子字符串的长度。例如，

```cpp
title.substr(2, 7)
```

是字符串 "Perfect"。

要对 C++ 字符串执行输入和输出，必须通过编写以下语句包含 iostream 库：

```cpp
#include <iostream>
```

在您的程序中。例如，随后可以通过执行以下内容显示字符串变量的内容：

```cpp
title = "Walls and Mirrors";
cout << title << "\n";
```

结果是 Walls and Mirrors。运算符 << 写入整个字符串，包括空格。

可以将一串字符读入字符串变量。例如，当语句

```cpp
cin >> title;
```

读取数据行

```
Jamie Perfect's Diary
```

它将字符串 "Jamie" 赋给 title。输入行中的空白字符会终止字符串的读取操作。要读取整行输入（包括其空白字符），请编写

```cpp
getline(cin, title);
```
