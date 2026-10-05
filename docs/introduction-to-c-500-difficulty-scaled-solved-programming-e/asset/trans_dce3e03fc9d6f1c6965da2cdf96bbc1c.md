
另一方面，当传递结构体的地址时，函数可能会改变其成员的值。例如，让我们修改 `test()`，以便修改 `st` 的成员：

```
void test(Student *ptr);

int main() {
  ...
  test(&st);
  std::cout << st.name << ' ' << st.code << ' ' << st.grd << '\n';
}
```

```
void test(Student *ptr) {
  ptr->name = "new";
  ptr->code = 30;
  ptr->grd = 7;
}
```

当调用 `test()` 时，`ptr = &st`。因此，由于 `ptr` 指向 `st` 的地址，函数可能会改变其成员的值。结果，程序显示：`new 30 7`

当将结构体传递给函数时，它的成员会被复制到相应参数的成员中。请注意，如果结构体很大或函数被调用多次，这种复制操作可能会增加内存需求并增加时间开销。另一方面，当通过指针或引用传递结构体的地址时，成员不会被复制。

> 为了获得更好的性能，请传递结构体的地址而不是结构体本身，即使函数不会改变其成员的值。

为了防止函数改变成员的值，我们将指针或引用声明为 `const`。例如：

```
void test(const Student *ptr);
```

现在，`test()` 无法修改由 `ptr` 指向的结构体的成员。

# 练习题

**C.13.1** 以下程序的输出是什么？

```
#include <iostream>

struct Student {
  char name[50];
  int code;
  float grd;
};
```

Student *test(), st;

```
int main()
{
    Student stud = {"somebody", 1111, 7.5}, *ptr = &stud;

    *ptr = *test();
    std::cout << ' ' << ptr->name << ' ' << ptr->code << ' ' << ptr->grd << ' '\n';
    return 0;
}
```

```
Student *test()
{
    return &st;
}
```

**答案：** 由于 `test()` 返回了 `st` 的地址，因此 *test() 等于 st*。由于 `ptr` 指向 `stud` 的地址，因此 **ptr 等于 stud*。因此，表达式 `*ptr = *test();` 等同于 `stud = st;`。由于全局变量初始化为零，程序输出：`0 0`。

**C.13.2** 定义结构体 `City`，成员为：`name`、`country name` 和 `population`。编写一个程序使用该类型读取 100 个城市的数据并将其存储在数组中。该程序应该读取一个国家名称和一个数字，并显示人口大于输入数字的城市。读取每个城市的数据，编写一个使用以下变量的循环：

```
int main()
{
    City *ptr, cities[SIZE];
    ...
}
```

**答案：**

```cpp
#include <iostream>
#include <string>
using std::cout;
using std::cin;
using std::string;

const int SIZE = 100;

struct City
{
    string name;
    string cntr;
    int pop;
}
```

```cpp
int main()
{
    bool found;
    int i, pop;
    string cntr;
    City *ptr, cities[SIZE];

    for(ptr = cities; ptr < cities+SIZE; ptr++) { /* 当 ptr 增加到数组的下一个元素（即下一个结构体）时 */
    {
        cout << "\nCity: ";
        getline(cin, ptr->name);

        cout << "Country: ";
        cin >> ptr->cntr;

        cout << "Population: ";
        cin >> ptr->pop;
        cin.get();
    }
    cout << "\ncountry to search: ";
    getline(cin, cntr);

    found = 0; for(i = 0; i < SIZE; i++) {
        if((cities[i].cntr == cntr) && (cities[i].pop > pop)) {
            found = 1;
            cout << cities[i].name << ' ' << cities[i].pop << '\n';
        }
    }
    if(found == 0)
        cout << "\nNo city found\n";
    return 0;
}
```

**C.13.3** 定义结构体 `Time`，成员为：`hours`、`minutes` 和 `seconds`。编写一个函数，接收一个整数指针作为参数并将其转换为小时、分钟和秒。这些值应该存储在 `Time` 结构体的成员中。编写一个程序读取秒数，调用该函数并显示返回结构体的成员。

```
#include <iostream>

struct Time {
    int hours;
    int mins;
    int secs;
};

Time mk_time(const int *ptr);

int main() {
    int secs;
    Time t;

    std::cout << "Enter seconds: ";
    cin >> secs;

    t = mk_time(&secs);
    std::cout << "\NH:" << t.hours << " M:" << t.mins << " S:" << t.secs << '\n';

    return 0;
}
```

```
Time mk_time(const int *ptr)
{
    Time tmp;

    tmp.hours = *ptr/3600;
    tmp.mins = (*ptr%3600)/60;
    tmp.secs = *ptr%60;
    return tmp;
}
```

**注释：** 为了避免复制 `mk_time()` 返回的结构体，我们可以传递结构体的地址。例如，我们可以将返回类型改为 `void`并将 `t` 的地址传递给 `mk_time()`。这样，函数就会修改调用函数的结构体，而不是返回一个新的结构体。

```
void mk_time(const int *ptr, Time *tmp)
{
    tmp->hours = *ptr/3600;
    tmp->mins = (*ptr%3600)/60;
    tmp->secs = *ptr%60;
}
```

**C.13.4** 定义结构体 `Book`，成员为：`code`。编写一个 `void` 函数，接收指向 `Book` 类型结构体的指针并返回 `code` 较大的结构体。检查 `code` 相同的情况并打印相关消息。编写程序读取并存储书籍数据到数组中。

**C.13.5** 定义结构体 `Product`，成员为：`name`、`code` 和 `price`。编写一个函数，接收 `Product` 结构体向量和 `code`。该函数应检查向量中是否存在该 `code` 的产品，如果是，则返回其指针；否则返回 `nullptr`。编写一个程序使用 `Product` 类型读取数据并存储在向量中。如果用户对 `price` 输入负值，则停止数据输入。然后，程序使用该函数显示产品的名称和价格。
