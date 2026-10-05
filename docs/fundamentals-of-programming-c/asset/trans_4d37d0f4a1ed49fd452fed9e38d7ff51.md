

## 18.2. 类模板

```cpp
/*
 * 析构函数释放列表持有的内存
 */
~List() {
  clear(); // 释放列表节点占据的空间
}

/*
 * insert(elem)
 * 将元素插入到列表末尾。
 * elem 是要插入的元素。
 */
void insert(const T elem) {
  head = insert(head, elem); // 将工作交给私有辅助方法
}

/*
 * print()
 * 打印链表的内容。
 * 将实际工作交给私有的 
 * 重载 print 方法。
 */
void print() const {
  print(head); // 将工作交给私有辅助方法
}

/*
 * 返回链表的长度。
 * 将实际工作交给私有的 
 * 重载 length 方法。
 */
int length() const {
  return length(head); // 将工作交给私有辅助方法
}

/*
 * clear()
 * 移除链表中的所有元素。
 * 私有的 dispose 函数处理核心工作。
 */
void clear() {
  dispose(head); // 为所有节点释放空间
  head = nullptr; // 头指针为空表示列表为空
}
```

注意，在列表 18.9 (list) 中，链式元素具有泛型类型 T。仔细观察，T 参数出现在代码中。列表 18.10 (templatelistmain.cpp) 显示了客户端如何为整数元素实例化 LList 模板。列表 18.10 (templatelistmain.cpp) 中的代码与列表 16.8 (list.cpp) 中的两行代码相比只有微小的变化。

## 列表 18.10: templatelistmain.cpp

```cpp
// templatelistmain.cpp
```

## 18. 类模板

```cpp
#include "llist.h" // 原为 #include "intlist.h"
#include <iostream>

using namespace std;

int main() {
    bool done = false;
    char command;
    int value;
    LList<int> list; // 原为 IntList list;

    while (!done) {
        cout << "Insert <item> P)rint L)length E)rase Q)uit >>";
        cin >> command;
        switch (command) {
            case 'I': // 向列表插入一个新元素
            case 'i':
                if (cin >> value)
                    list.insert(value);
                else
                    done = true;
                break;
            case 'P': // 打印列表内容
            case 'p':
                list.print();
                break;
            case 'L': // 打印列表长度
            case 'l':
                cout << "Number of elements: " << list.length() << endl;
                break;
            case 'E': // 清除列表
            case 'e':
                list.clear();
                break;
            case 'Q': // 退出循环（并程序）
            case 'q':
                done = true;
                break;
        }
    }
}
```

语句

`LList<int> list;`

实例化了一个实际类，其中 T 的所有出现处都变成了 int。它还声明 list 为该实例化类的一个对象。

正如我们在同一个程序中使用多个不同类型来实例化函数模板一样，我们也可以对类模板做同样的事情。列表 18.9 (llist.h) 中的类模板 LList 生成了以下客户端代码：

```cpp
LList<int> intlist;
LList<string> strlist;
```

## 18.3. 迭代器

```cpp
intlist.insert(5);
strlist.insert("Wow");
intlist.print();
strlist.print();
```

这段代码片段同时管理整数列表和字符串对象列表。

此时你可能已经怀疑 `std::vector` 是一个类模板的事实。**vector** 类模板比我们简单的 `LList` 模板复杂得多，但其设计的基本机制——类模板是相同的。

11.2 和附录 F 中的扩展信息演示了我们如何使用指针来访问数组中的元素。vector 是一个管理原始数组的对象，该类的开发者设计 vector 在视觉和感受上尽可能像数组。他们采用了方括号 `[]` 运算符来访问元素。他们还设计了让程序员使用类指针的对象来访问 vector 内的元素。这些类指针的对象被称为*迭代器*（iterators）。

迭代器是一种对象，允许以一种独立于实现的方式遍历和访问数据结构的元素。C++ 提供了两个全局函数 **begin** 和 **end**，它们产生用于向前向后移动的迭代器。

为了表现得像指针，迭代器提供了以下方法：

- `operator*`：访问当前位置的元素。
- `operator++`：移动到下一个元素。
- `operator==`：确定两个迭代器是否引用同一个元素。

列表 18.11 (simpleiterator.cpp) 显示了如何使用这些方法。

## 列表 18.11: simpleiterator.cpp

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    // 创建一个 vector
    vector<int> vec = {10, 20, 30, 40, 50};
    // 初始化指向第一个元素的迭代器
    vector<int>::iterator iter = vec.begin();
    // 打印元素
    while (iter != vec.end()) {
        cout << *iter << " ";
        iter++;
    }
    cout << endl;
    return 0;
}
```

