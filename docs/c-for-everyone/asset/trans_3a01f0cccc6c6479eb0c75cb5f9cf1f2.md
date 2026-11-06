

## 14.3 映射

映射在键和值对象之间建立关联。

映射是一种数据类型，用于维护*键*与*值*之间的关联。映射中的每个键都有一个唯一的值，但一个值可以与多个键关联。图 11 给出了一个典型示例：一个将姓名与颜色关联起来的映射。这个映射可能描述了不同人最喜欢的颜色。

使用标准库中的map类，你可以用`[]`运算符来关联键和值。下面是一个示例：

```cpp
map<string, double> scores;
scores["Tom"] = 90;
scores["Diana"] = 86;
scores["Harry"] = 100;
```

你可以用同样的表示法读取分数：

```cpp
cout << "Tom's score: " << scores["Tom"];
```

要判断映射中是否存在某个键，请使用`find`成员函数。它会返回一个迭代器，指向具有给定键的条目；如果键不存在，则指向容器末尾之后的位置。

键类型为`K`、值类型为`V`的`map<K, V>`的迭代器会生成`pair<K, V>`类型的元素。`pair`类是一个在`<utility>`头文件中定义的简单类，用于存储一对值。它有两个公共（！）数据成员 first 和 second。

![](img/5e58fb4c840712efd6ed6fa82bb97f57_616_0.png)

**图 11**  一个映射

### ch14/tele.cpp

```cpp
#include <iostream>
#include <map>
#include <utility>
#include <string>
#include <vector>

using namespace std;

/**
TelephoneDirectory maintains a map of name/number pairs
and an inverse multimap of numbers and names.
*/
class TelephoneDirectory
{
public:
/**
Adds a new name/number pair to database.
@param name the new name
@param number the new number
*/
void add_entry(string name, int number);

/**
Finds the number associated with a name.
@param name the name being searched
@return the associated number, or zero
if not found in database
*/
int find_entry(string name);

/**
Finds the names associated with a number.
@param number the number being searched
@return the associated names
*/
vector<string> find_entries(int number);

/**
Prints all entries.
*/
void print_all();
private:
map<string, int> database;
multimap<int, string> inverse_database;
};

void TelephoneDirectory::add_entry(string name, int number)
{
    database[name] = number;
    inverse_database.insert(make_pair(number, name));
}

int TelephoneDirectory::find_entry(string name)
{
    map<string, int>::iterator p = database.find(name);
    if (p == database.end())
    {
        return 0; // Not found
    }
    else
    {
        return p->second;
    }
}

vector<string> TelephoneDirectory::find_entries(int number)
{
    multimap<int, string>::iterator lower
        = inverse_database.lower_bound(number);
    multimap<int, string>::iterator upper
        = inverse_database.upper_bound(number);
    vector<string> result;

    for (multimap<int, string>::iterator pos = lower;
         pos != upper; pos++)
    {
        result.push_back(pos->second);
    }
    return result;
}

void TelephoneDirectory::print_all()
{
    for (map<string, int>::iterator pos = database.begin();
         pos != database.end(); pos++)
    {
        cout << pos->first << ": " << pos->second << endl;
    }
}

int main()
{
    TelephoneDirectory data;
    data.add_entry("Fred", 7235591);
    data.add_entry("Mary", 3841212);
    data.add_entry("Sarah", 3841212);
    cout << "Number for Fred: " << data.find_entry("Fred") << endl;
    vector<string> names = data.find_entries(3841212);
    cout << "Names for 3841212: ";
    for (int i = 0; i < names.size(); i++)
    {
        cout << names[i] << " ";
    }
    cout << endl;
    cout << "All names and numbers:" << endl;
    data.print_all();
    return 0;
}
```

### 程序运行

```text
Number for Fred: 7235591
Names for 3841212: Mary Sarah
All names and numbers:
Fred: 7235591
Mary: 3841212
Sarah: 3841212
```

![](img/5e58fb4c840712efd6ed6fa82bb97f57_620_0.png)

- 11. 定义并初始化一个映射，将英文单词“one”到“five”分别映射到数字 1 到 5。
- 12. 编写一个循环，打印你在自测题 11 中定义的映射的所有值。
- 13. 自测题 12 中的值按什么顺序打印？
- 14. 一本书的索引指明每个词出现在哪些页码。你可以使用哪种 C++ 数据结构来建模这样的索引？
- 15. 假设你要构建一本书的索引。完成以下函数，将单词添加到给定页码：

    ```cpp
    void Index::add_word(string word, int page)
    {
        if (...) { word_pages[word] = set<int>(); }
        word_pages[word].insert(page);
    }
    ```

**动手练习** 现在你可以尝试本章末尾的这些练习：R14.14、P14.1、P14.5。

### 专题 14.2 — 常量迭代器

![](img/5e58fb4c840712efd6ed6fa82bb97f57_620_1.png)

如果你仔细查看tele.cpp程序的源代码，你会注意到查找和打印目录条目的成员函数并未标记为const。如果你正确地将其实现为常量成员函数，编译器会抱怨迭代器不是常量的。这是一个合理的问题，因为你可以通过迭代器修改容器。

每种迭代器类型都有一个对应的常量迭代器类型，类似于常量指针。下面是find_entry函数的一个const正确的实现：

```cpp
int TelephoneDirectory::find_entry(string name) const
{
    map<string, int>::const_iterator p = database.find(name);
    if (p == database.end())
    {
        return 0; // Not found
    }
    else
    {
        return p->second;
    }
}
```

## 14.4 优先队列

> 从优先队列中移除元素时，获取的是优先级最高的元素。

我们将研究的最后一个容器是优先队列。*优先队列*是一种针对一个特殊任务优化的容器：快速定位优先级最高的元素。优先级是一种比排序更弱的条件。在优先队列中，其余元素的顺序无关紧要；只有优先级最高的元素才是重要的。

