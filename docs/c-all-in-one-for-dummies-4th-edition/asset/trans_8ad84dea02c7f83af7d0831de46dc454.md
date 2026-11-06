
```cpp
LISTING 6-4: (continued)

int main() {
    map<string, string> marriages;
    marriages["Tom"] = "Suzy";
    marriages["Harry"] = "Harriet";

    cout << marriages["Tom"] << endl;
    cout << marriages["Harry"] << endl;
    return 0;
}
```

要使用 map，你需要声明一个 map 类的变量，并提供两个模板参数：键类和值类，在示例中二者都是 string。要存储 map 值，你把键放在方括号内，并将其设置为一个值：

```
marriages["Tom"] = "Suzy";
```

要获取特定项，你在方括号中提供键：

```cpp
cout << marriages["Tom"] << endl;
```

运行此示例时，你会看到以下两个字符串作为输出：

```
Suzy
Harriet
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_663_0.png)

**记住**

即使键可以是任何类型或类，你在设置 map 时也必须指定所使用的类型或类。完成设置后，该特定 map 就只能使用该类型。因此，如果你说键将是 string，那么之后就不能使用整数作为键，例如 `marriages[3] = "Suzy";`。

### 包含实例、指针或引用

当人们开始讨论如何使用容器模板时，你遇到的最常见讨论之一就是：应该把实例、指针还是引用放入容器。例如，下面哪一种应该由你来写？

```cpp
vector<MyClass>
vector<MyClass *>
vector<MyClass &>
```

换句话说，你是希望容器存储实际实例（无论那可能意味着什么）、对实际实例的引用，还是指向实例的指针？为了探讨这个想法，请看清单 6-5 中的 Maps2 示例。在这里，你将尝试用不同方式把内容存储到 map 中：实例、指针和引用。

### **清单 6-5：** 做出决定：哦，该存储什么？

```cpp
#include <iostream>
#include <map>

using namespace std;

class StoreMe {
    public:
        int Item;
};

bool operator < (const StoreMe & first,
const StoreMe & second) {
    return first.Item < second.Item;
}

int main() {
    // First try storing the instances
    map<StoreMe, StoreMe> instances;
    StoreMe key1 = {10}; // braces notation!
    StoreMe value1 = {20};
    StoreMe key2 = {30};
    StoreMe value2 = {40};
    instances[key1] = value1;
    instances[key2] = value2;

    value1.Item = 12345;
    cout << instances[key1].Item << endl;
    instances[key1].Item = 34567;
    cout << instances[key1].Item << endl;

    // Next try storing pointers to the instances
    map<StoreMe*, StoreMe*> pointers;
    StoreMe key10 = {10};
    StoreMe value10 = {20};
    StoreMe key11 = {30};
    StoreMe value11 = {40};
```

*（续）*

```cpp
pointers[&key10] = &value10;
pointers[&key1] = &value11;

value10.Item = 12345;
cout << (*pointers[&key10]).Item << endl;

// Finally try storing references to the instances.
// Commented out because it causes an error.)
// map<StoreMe&, StoreMe&> pointers;
return 0;
}
```

要创建 StoreMe 的实例，你使用花括号记法。在没有构造函数时，你可以这样做。因此，下面这一行

```cpp
StoreMe key1 = {10};
```

会创建一个 StoreMe 实例，并将 10 放入 Item 属性中。要创建单个 instances 条目，你需要一个键实例和一个值实例，二者都是 StoreMe。然后，你使用键为存储在 map 中的值提供一个名称。因此，instances 包含两个条目，每个条目由两个 StoreMe 对象组成。运行应用程序时，你会看到：

```text
20
34567
12345
```

这个输出与预期并不完全一致，因为代码更改了 value1 中的 Item 属性：

```cpp
value1.Item = 12345;
```

当代码输出 instances[key1].Item 的值时，你会看到输出为 20，而不是 12345。这意味着存储在 map 中的值是副本，而不是原始值。然而，当代码像这样更改 instances 中的值时：

```cpp
instances[key1].Item = 34567;
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_665_0.png)

instances 条目的值部分确实会改变。你会看到输出 34567。因此，在使用 map 实例时，你必须直接修改 map 条目。

它试图声明一个持有引用的 map，但代码反而产生编译器错误。试着取消注释被注释掉的那一行，看看错误消息。以下是你可能看到的示例（完成后请务必把注释加回去）：

```
error: conflicting declaration 'std::map<StoreMe&, StoreMe&> pointers'
error: 'pointers' has a previous declaration as
  std::map<StoreMe*, StoreMe*> pointers
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_667_0.png)

**记住**

引用完全不可行，因为 map 会复制你放入其中的所有内容。

### 处理副本

所有 C++ 容器（不仅仅是 map）通常都会复制你放入其中的任何内容，如上一节所示。清单 6-6 中展示的 Vectors3 示例复制了清单 6-5 中展示的 Maps2 示例的基本功能。

### **清单 6-6：** Maps2 示例的 vector 版本

```cpp
#include <iostream>
#include <vector>

using namespace std;

class StoreMe {
public:
  int Item;
};

int main() {
  vector<StoreMe> instances;
  StoreMe value1 = {20};
  StoreMe value2 = {40};
  instances.push_back(value1);
  instances.push_back(value2);

  value1.Item = 12345;
  cout << instances[0].Item << endl;
  instances[0].Item = 34567;
  cout << instances[0].Item << endl;
```

```cpp
vector<StoreMe*> pointers;
StoreMe value10 = {20};
StoreMe value11 = {40};
pointers.push_back(&value10);
pointers.push_back(&value11);

value10.Item = 12345;
cout << (*pointers[0]).Item << endl;
return 0;
}
```

奇怪的是，这个示例的输出与 Maps2 示例完全相同，原因也相同。容器是 vector 还是 map 并不重要；二者都会保存你所提供对象或指针的副本。因此，你可以记住以下两条关于删除原始对象的规则：

- **当容器保存实例时：** 如果你把实例放入容器，可以在添加之后删除原始实例。这没问题，因为容器拥有这些实例自己的副本。
- **当容器保存指针时：** 如果你把指针放入容器，就不应删除原始实例，因为容器中的指针仍然指向这些实例。

哪种方法更好由你决定。但有几件事需要考虑：

- **保留实例：** 如果你不想让实例闲置在手边，可以把实例放入容器，容器会制作副本。
- **可复制性：** 有些类，例如充满指向其他类的指针的类，或者体积巨大的类，复制效果不好。在这种情况下，你可能希望把指针放入容器。

### 比较实例

当你使用包含其他类的类（例如 vector）时，你需要为该类提供一种比较两个对象的方法。以下各节描述在使用容器时如何提供比较能力。

### 执行比较

上一节详细说明了比较对象时必须解决的两个问题。以下是解决这两个问题的方法：如果你处理的是自己的类，那么除了设置容器类之外，还要提供一个比较你自己类的两个实例的函数。你的比较函数可以判断两个实例是否相等、第一个是否小于第二个，或者第一个是否大于第二个。

![](img/128ab511de4e7360e167e3b15cdd5dd0_670_1.png)

起初，小于和大于如何适用于 Employee 类之类的事物可能并不明显。但小于和大于背后的想法是，为容器类提供一种确定排序顺序的方法。例如，你可能会选择以下方式之一对 Employee 类进行排序：

- 社会安全号码
- 姓，名
- 名，姓
- 员工 ID
- 地址
- 组织部门

