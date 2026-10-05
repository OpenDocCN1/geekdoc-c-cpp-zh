

# 理解 begin() 和 end()

begin() 返回一个指向 vector 中第一个元素的迭代器。该迭代器可以通过递增迭代器来逐个访问 vector 中的元素。这个过程类似于使用指针访问数组元素的方式。end() 成员函数用于确定何时到达 vector 的末尾。

end() 并不返回指向容器中最后一个元素的迭代器。相反，它返回一个指向最后一个元素之后的的迭代器。因此，容器中的最后一个元素由 `p.end() - 1` 指向。

# 在 Vector 中插入和删除元素

除了将新元素放在 vector 的末尾，我们还可以使用 `insert` 函数在特定的索引位置插入元素。我们还可以使用 `erase` 移除元素。

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<char> v(10);
    vector<char> v2;
    char str[] = "<Vector>";

    size_t i;
    for (i=0; i < 10; i++) v[i] = 'a';

    // 将 str 中的字符拷贝到 v2
    for (i=0; str[i] != '\0'; i++) v2.push_back(str[i]);

    // 显示 vector v 的内容：
    cout << "Original contents of v:\n";
    for (i = 0; i < v.size(); i++) cout << v[i] << " ";
    cout << "\n";

    // 获取 vector v 的迭代器
    vector<char>::iterator p = v.begin();
    // 指向 v 的第3个元素
    p += 2;

    // 向 v 中插入10个 'X'
    v.insert(p, 10, 'X');

    // 显示插入 X 后的内容
    cout << "Size after inserting X's = " << v.size() << endl;
    cout << "Vector contents after insertion:\n";
    for(int i = 0; i < v.size(); i++) cout << v[i] << " ";
    cout << "\n";

    // 移除插入的元素
    p = v.begin();
    // 指向第3个元素
    p += 2;
    // 移除后续10个元素
    v.erase(p, p+10);

    // 显示删除后的内容
    cout << "Vector size after erase = " << v.size() << endl;
    cout << "Vector contents after erase:\n";
    for (int i = 0; i < v.size(); i++) cout << v[i] << " ";
    cout << "\n";

    // 将 v2 插入 v
    v.insert(p, v.begin(), v2.end());

    cout << "Size after v2's insertion into v = " << v.size() << endl;
    cout << "Contents of vector after insertion:\n";
    for (int i = 0; i < v.size(); i++) cout << v[i] << " ";
    cout << endl;
    return 0;
}
```

输出:
Original contents of v:
a a a a a a a a a a

Size after inserting X's = 20
Vector contents after insertion:
a a X X X X X X X X a a a a a a a a

Size after erase = 10
Vector contents after erase:
a a a a a a a a a a
Size after v2's insertion into v = 18
Contents of vector after insertion:
a a <Vector> a a a a a a a a

# 在 Vector 中存储类对象

任何类型的对象都可以存储在 Vector 中，包括我们创建的类对象，只要它们拥有构造函数并实现了 `>` 和 `==` 比较运算符。

```cpp
// 在 vector 中存储类对象。
#include <iostream>
#include <vector>
#include <cstdlib>

using namespace std;

class DailyTemperature {
    int temperature;
    public:
        // 构造函数
        DailyTemperature() { temperature = 0; }
        DailyTemperature(int x) { temperature = x; }
        DailyTemperature& operator=(int x) {
            temperature = x; return *this;
        }

        double get_temperature() { return temperature; }
};

bool operator<(DailyTemperature a, DailyTemperature b) {
    return a.get_temperature() < b.get_temperature();
}

bool operator==(DailyTemperature a, DailyTemperature b) {
    return a.get_temperature() == b.get_temperature();
}

int main() {
    vector<DailyTemperature> v;
    size_t i;
    for(i = 0; i < 7; i++)
        v.push_back(DailyTemperature(60 + rand()%30));

    cout << "Fahrenheit temperatures:\n";
    for ( i = 0; i < v.size(); i++)
        cout << v[i].get_temperature() << " ";
    cout << endl;

    // 从华氏度转换为摄度
    for (i = 0; i < v.size(); i++)
        v[i] = (v[i].get_temperature() - 32) * 5 / 9;
    cout << "Centigrade temperatures:\n";

    for (i = 0; i < v.size(); i++)
        cout << v[i].get_temperature() << " ";

    return 0;
}
```

输出:
Fahrenheit temperatures:
73 76 87 85 83 85 76
Centigrade temperatures:
22 24 30 29 28 29 24

# List 容器

list 容器实现了一个双向线性链表。与具有随机访问能力的 vector 不同，list 只能顺序访问。由于 list 是双向的，因此可以通过从头到尾或从尾到头进行访问。list 的插入和删除速度非常快，但访问速度比 vector 慢。

list 模板的声明：

```cpp
template <class T, class Allocator = allocator<T>> class list;
```

在这里，T 是 list 中存储的数据类型。分配器由 Allocator 指定，默认使用标准分配器。

我们按照如下方式实例化 list：

```cpp
#include <list>

list<int> alist;             // 创建一个空的整数列表
list<Foo> foo;              // 创建一个空的 Foo 列表
```

以下是 list 函数：

- `clear()`: 移除 list 中的所有元素。
- `empty()`: 如果列表为空则返回 true，否则返回 false。
- `begin()`: 返回指向列表第一个元素的迭代器。
- `end()`: 返回指向最后一个元素之后的迭代器。
- `erase(iterator)`: 移除由迭代器指向的元素。
- `insert(iterator, T)`: 在迭代器指向的元素之前插入元素。
- `front()`: 返回列表第一个元素的引用。
- `back()`: 返回列表最后一个元素的引用。
- `pop_back()`: 移除列表最后一个元素。
- `pop_front()`: 移除列表第一个元素。
- `push_back(T)`: 在列表末尾添加元素。
- `push_front(T)`: 在列表头部添加元素。
- `size()`: 返回列表中元素的数量。

STL 实现了比较运算符：
`==`, `<=`, `>`。

以下是 list 构造函数：

- `list()`: 创建空列表。
- `list(size_type n, const T& val)`: 创建包含 `n` 个 `val` 元素的列表。
- `list(InputIt first, InputIt last)`: 根据范围范围创建列表。
- `list(const list& other)`: 创建另一个列表的拷贝。

# 在 List 中存储类对象

这是一个使用 list 存储 Foo 类型对象的示例。注意 `<`, `>`, 和 `!=` 针对 Foo 对象进行了重载。list 在搜索、排序或合并元素时需要一种比较方式。

```cpp
// 在 list 中存储类对象。
#include <iostream>
#include <list>
#include <cstring>

using namespace std;

class Foo {
    int a, b;
    int sum;
public:
    Foo() { a = b = 0; sum = 0; }
    Foo(int i, int j) {
        a = i;
        b = j;
        sum = a + b;
    }

    int getsum() { return sum; }

    friend bool operator<(const Foo& o1, const Foo& o2);
    friend bool operator==(const Foo& o1, const Foo& o2);
    friend bool operator!=(const Foo& o1, const Foo& o2);
};

int main() {
    list<Foo> lst;
    lst.push_back(Foo(10, 20));
    lst.push_back(Foo(30, 40));
    lst.push_front(Foo(5, 5));

    cout << "List size: " << lst.size() << endl;
    for (auto it = lst.begin(); it != lst.end(); ++it) {
        cout << "Sum: " << it->getsum() << " ";
    }
    cout << endl;

    return 0;
}

bool operator<(const Foo& o1, const Foo& o2) {
    return o1.sum < o2.sum;
}

bool operator==(const Foo& o1, const Foo& o2) {
    return o1.sum == o2.sum;
}

bool operator!=(const Foo& o1, const Foo& o2) {
    return o1.sum != o2.sum;
}
```

