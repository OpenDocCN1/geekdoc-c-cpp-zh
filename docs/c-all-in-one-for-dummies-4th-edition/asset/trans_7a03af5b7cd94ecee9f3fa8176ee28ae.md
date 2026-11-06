
| 头文件 | C++ 版本 | 简短说明 |
|---|---|---|
| `<functional>` |  | 提供函数对象、函数调用、绑定操作和引用包装器。 |
| `<initializer_list>` | C++ 11 及以上 | 提供初始化除数组以外的容器（如 vector、list 和 map）的方法。 |
| `<optional>` | C++ 17 及以上 | 一个可能包含也可能不包含对象的变量的包装器。 |
| `<source_location>` | C++ 20 及以上 | 标识源代码的位置。 |
| `<tuple>` | C++ 11 及以上 | 允许创建元组。 |
| `<type_traits>` | C++ 11 及以上 | 获取编译时类型信息。 |
| `<typeindex>` | C++ 11 及以上 | 提供 type_info 对象的包装器，以便在关联和无序关联容器中用作索引。 |
| `<typeinfo>` |  | 获取运行时信息。 |
| `<utility>` |  | 基本实用函数。 |
| `<variant>` | C++ 17 及以上 | 提供对变体类型变量的支持。 |
| `<version>` | C++ 20 及以上 | 提供依赖于实现的库信息。 |

## 使用哈希解析字符串

哈希是当今应用程序的一项重要安全要求。哈希会为传入的任何字符串创建一个唯一的数值等价物。理论上，您无法通过使用另一个字符串来复制哈希所创建的数字。哈希不可逆——它与加密和解密不同。

哈希的一个常见用途是将密码从客户端发送到服务器。客户端将用户的密码转换为数字哈希，并将该数字发送到服务器。该数字每天都会根据客户端和服务器都知道的某种公式而变化。服务器验证的是数字，而不是密码。即使有人正在监听，他们也无法从数字中确定密码；因此，他们无法窃取密码用于目标应用程序。哈希的其他使用示例包括：

-   将文件的哈希与之前保存的哈希值进行校验，以确保无人修改过该文件。
-   比较两个文件，以确保它们极有可能相同。
-   使字典搜索变得快速。

Code::Blocks 对哈希提供了出色的支持。但是，要使用它，必须使用第 1 册第 5 章“使用范围”一节中的方法启用对 C++11 扩展的支持。启用所需支持后，您可以创建此处所示的 HashingStrings 示例来演示哈希的用法。

```cpp
#include <iostream>
#include <unordered_map>

using namespace std;

int main() {
  hash<const char*> MyHash;
  cout << "The hash of \"Hello World\" is:" << endl;
  cout << MyHash("Hello World") << endl;
  cout << "while the hash of \"Goodbye Cruel World\" is:"
       << endl;
  cout << MyHash("Goodbye Cruel World") << endl;
  return 0;
}
```

该示例首先创建一个哈希函数对象 MyHash。您可以使用此函数对象将输入文本转换为哈希值。该函数对象的工作方式与任何其他函数一样，因此您可以将输入文本作为 MyHash("Hello World") 提供。对于特定输入，哈希始终输出完全相同的值。因此，您应该会从此示例中看到以下输出。

```text
The hash of "Hello World" is:
4952133
while the hash of "Goodbye Cruel World" is:
4952192
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_789_0.png)

哈希除了满足安全要求之外还有其他用途。例如，您可以创建一个依赖哈希来更容易定位特定值的容器。在这种情况下，您使用 `unordered_map<>` 在哈希映射中使用键值对。接下来展示的 HashMap 示例演示了如何创建哈希映射：

```cpp
#include <iostream>
#include <unordered_map>
#include <string.h>

using namespace std;

struct eqstr {
    bool operator()(const char* s1, const char* s2) const
    {
        return strcmp(s1, s2) == 0;
    }
};

int main() {
    unordered_map<const char*, int,
    hash<const char*>, eqstr> Colors;
    Colors["Blue"] = 1;
    Colors["Green"] = 2;
    Colors["Teal"] = 3;
    Colors["Brick"] = 4;
    Colors["Purple"] = 5;
    Colors["Brown"] = 6;
    Colors["LightGray"] = 7;
    cout << "Brown = " << Colors["Brown"] << endl;
    cout << "Brick = " << Colors["Brick"] << endl;
    // This key isn't in the hash map, so it returns a
    // value of 0.
    cout << "Red = " << Colors["Red"] << endl;
}
```

无序（哈希）映射需要四个输入：

-   键类型
-   数据类型
-   哈希函数
-   相等性键

前三个输入很直接。在本例中，代码使用字符串作为键类型，使用整数值作为数据类型，并使用 `hash<const char*>` 作为哈希函数。您已经从本节前面的示例中了解了哈希函数的工作方式。

相等性键类要稍微复杂一些。您必须为哈希映射提供一种确定相等性的方法。在本例中，代码将输入字符串与作为键存储的字符串进行比较。`eqstr` 结构执行将输入字符串与键进行比较的任务。该结构必须返回布尔值，因此代码将 `strcmp` 函数与 0 进行比较。当两者相等时，即字符串相等时，`eqstr` 返回 true。

该示例接着检查三种颜色，其中只有两种出现在哈希映射 Colors 中。在前两种情况下，您会看到预期的值。在第三种情况下，您会看到 0，这表明 Colors 不包含所需的键。使用哈希映射时，请始终保留 0 作为错误指示符，因为即使哈希映射不包含所需的键，它也总会返回一个值。此示例的输出为

![](img/128ab511de4e7360e167e3b15cdd5dd0_790_0.png)

```text
Brown = 6
Brick = 4
Red = 0
```

## 使用随机访问迭代器获取信息

大多数容器允许您对其包含的数据执行随机访问。例如，RandomAccess 示例表明，您可以创建一个迭代器，然后对当前偏移量进行增加或减少，以获取该迭代器所支持容器内的值：

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {
  vector<string> Words;
  Words.push_back("Blue");
  Words.push_back("Green");
  Words.push_back("Teal");
  Words.push_back("Brick");
  Words.push_back("Purple");
  Words.push_back("Brown");
  Words.push_back("LightGray");
  // Define a random iterator.
  vector<string>::iterator Iter = Words.begin();
  // Access random points.
  Iter += 5;
  cout << *Iter << endl;
  Iter -= 2;
  cout << *Iter << endl;
  return 0;
}
```

在本例中，vector（即 Words）包含一个由七个项组成的列表。代码为 Words 创建了一个名为 Iter 的迭代器。然后对迭代器偏移量进行增加或减少，并将输出显示在屏幕上。运行此示例时，您将看到以下内容：

```text
Brown
Brick
```

有时您需要使用随机访问迭代器执行特殊任务。例如，您可能想创建一个特殊函数来对 vector 的成员或 vector 内某个范围内的成员求和。在这种情况下，必须创建一个专用函数来执行如下任务，因为标准库并未包含任何可为您完成此任务的函数，如 RandomAccess2 示例所示：

```cpp
#include <iostream>
#include <vector>

using namespace std;

template <class RandomAccessIterator>
float AddIt(RandomAccessIterator begin,
            RandomAccessIterator end) {
  float Sum = 0;
  RandomAccessIterator Index;
  // Make sure that the values are in the correct order.
  if (begin > end)
  {
    RandomAccessIterator temp;
    temp = begin;
    begin = end;
    end = temp;
  }
  for (Index = begin; Index != end; Index++)
    Sum += *Index;
  return Sum;
}

int main() {
  vector<float> Numbers;
  Numbers.push_back(1.0);
  Numbers.push_back(2.5);
  Numbers.push_back(3.75);
  Numbers.push_back(1.26);
  Numbers.push_back(9.101);
  Numbers.push_back(11.3);
  Numbers.push_back(1.52);

  // Sum the individual members.
  float Sum;
  Sum = AddIt(Numbers.begin(), Numbers.end());
  cout << Sum << endl;
  Sum = AddIt(Numbers.end(), Numbers.begin());
  cout << Sum << endl;

  // Sum a range.
  vector<float>::iterator Iter = Numbers.begin();
  Iter += 5;
  Sum = AddIt(Iter, Numbers.end());
  cout << Sum << endl;
  return 0;
}
```

该示例建立在前一个示例的基础上。您仍然创建一个 vector（即 Numbers），并用数据填充它。但是，在本例中，您创建一个输出变量 Sum，它包含 Numbers 中所含元素的求和结果。

AddIt() 是一个特殊函数，接受两个 RandomAccessIterator 值作为输入。这两个输入表示 vector 内您希望以某种方式操作的一个范围。该示例只是将它们相加，但您可以执行任何想要的任务。输出是一个包含求和结果的 float。

