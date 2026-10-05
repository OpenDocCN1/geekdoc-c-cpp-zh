
# 546 C++ 导论

public:

```cppvoid set(const string& n, float s);
float get() const;
void show() const;
```

```cpp
void Employee::set(const string& n, float& s)
{
    name = n;
    sal = s;
}
```

```cpp
float Employee::get() const
{
    return sal;
}
```

```cpp
void Employee::show() const
{
    cout << "N:" << name << " S:" << sal << '\n';
}
```

```cpp
int main()
{
    int i, pos;
    float base, sal, max_sal;
    string name;
    Employee tmp;
    vector<Employee> empl;
    while (1)
    {
        cout << "\nName: ";
        getline(cin, name);
        cout << "\nSalary: ";
        cin >> sal;
        if(sal == -1)
            break;
        tmp.set(name, sal);
        empl.push_back(tmp); // 提取换行符。
    }
    cout << "\nEnter base: ";
    cin >> base;
    max_sal = -1;
    for(i = 0; i < empl.size(); i++)
    {
        sal = empl[i].get();
        if (sal > base)
            empl[i].show();
        if(sal > max_sal)
        {
            pos = i;
            max_sal = sal;
        }
    }
    if (max_sal != -1)
        empl[pos].show();
    return 0;
}
```

**注释：** 我们需要少量 set/get 函数来访问私有成员，并使用 show() 函数来显示数据。不需要向 set() 传递引用。我们可以通过值传递字符串的副本。正如我们所说的，我们使用引用是为了获得更好的性能。

## C.18 定义类 Rect，其私有成员 l 和 h 分别表示矩形的长度和宽度。同样定义类 Circle，其私有成员 r 表示圆的半径。每个类都必须包含一个适当的构造函数和一个公共函数 area()，该函数返回相应形状的面积。

- 定义一个模板函数 f()，接受类型为 Rect 或 Circle 的泛型参数并返回对象的面积。编写一个测试该函数的程序。

**答案：**

```cpp
#include <iostream>

class Rect {
private:
    float l;
    float h;
public:
    Rect(float a, float b) {l=a; h=b;};
    float area() const {return l*h};
};

class Circle {
private:
    float r;
public:
    Circle(float a) {r=a;};
    float area() const {return r*3.14};
};

template <typename T> float f(T t) {
    return t.area();
}

int main() {
    Rect r(1, 2);
    Circle c(3);

    std::cout << f(r) << ' ' << f(c) << '\n';
    return 0;
}
```

**注释：** 为了初始化私有成员，我们使用了构造函数。

b. 修改 f()，使得将 Rect 或 Circle 对象的指针作为参数传递并返回其面积。相应修改程序以测试该函数。

**答案：**

```cpp
template <typename T> float f(T* t)
{
    return t->area();
}

int main()
{
    Rect r(1, 2);
    Circle c(3);

    std::cout << f(&r) << ' ' << f(&c) << ' \n';
    return 0;
}
```

## C.17 完成 Lifo 类的公共部分，并编写一个程序测试该类的操作。Lifo 的目的是实现一个栈，类似于练习 C.J4.8，不同之处在于使用 vector 对象来存储 Node 元素，而不是链表。

```cpp
struct Node
{
    string name;
    float grd;
};
```

```cpp
class Lifo
{
private:
    vector<Node> vec_n;
public:
    /* 实现栈接口的函数。具体来说：
       push() 函数向栈中添加一个元素（即一个 Node 对象，在 vec_n 中）；
       pop() 使用一个参数返回栈中最后添加的元素，显示其数据并将其从栈中移除；
       show_all() 显示所有元素的数据；
       get_nodes() 返回栈中存储了多少个元素。选择哪些函数应为 const。 */
};
```

**答案：**

```cpp
#include <iostream>
#include <vector>
#include <string>
using std::cout;
using std::string;
using std::vector;

struct Node
{
    string name;
    float grd;
};
```

```cpp
class Lifo
{
private:
    vector<Node> vec_n;
public:
    void push(const Node& n);
    void pop(Node& n);
    void show_all() const;
    int get_nodes() const;
};
```

```cpp
void Lifo::push(const Node& n)
{
    vec_n.push_back(n);
}
```

```cpp
void Lifo::pop(Node& n)
{
    int size = vec_n.size();
    if(size > 0) {
        n = vec_n[size-1];
        vec_n.erase(vec_n.end() - 1);
    }
    else
        cout << "Stack is empty\n";
}
```

```cpp
void Lifo::show_all() const
{
    int size = vec_n.size();
    if(size > 0) {
        for (int i = 0; i < size; i++)
            cout << "N:" << vec_n[i].name << " G:" << vec_n[i].grd << '\n';
    }
    else
        cout << "Stack is empty\n";
}
```

```cpp
int Lifo::get_nodes() const
{
    return vec_n.size();
}
```

```cpp
int main()
{
    int i;
    Node node[] = {"Alpha", 1}, {"Beta", 2}, {"Epsilon", 3};
    Lifo lifo;
    for(i = 0; i < 3; i++)
        lifo.push(node[i]);
    lifo.show_all();
    lifo.pop(node);
    cout << "N:" << node.name << " G:" << node.grd << '\n';
    cout << "Nodes:" << lifo.get_nodes() << '\n';
    return 0;
}
```

## C.17.9 定义 Time 类，其私有成员 hr, min, sec 分别表示小时、分钟和秒。同样，该类应包含一个构造函数来初始化成员，以及一个公共函数 show()，该函数显示时间。为了防止私有成员被意外访问，我们需要少量 set/get 函数。不需要向 set() 传递引用。我们可以通过值传递字符串的副本。正如我们所说的，使用引用是为了获得更好的性能。连续使用 . 运算符意味着左侧必须有一个对象。因此，函数必须返回一个对象，特别是该对象的引用，因为对成员的修改必须在对象本身进行，而不是在其副本上。也就是说，看看你是否理解了上面的句子，如果我们将三个函数的返回类型从 Time& 改为 Time，将将显示？



..11., min, sec 成员的 Time 类，并定义 、 sec 成员的分钟、秒。同样，该类应包含一个构造函数来初始化成员，以及一个公共函数 show()，该函数显示时间。以如下方式定义函数，使得以下程序运行：

```cpp
int main()
{
    Time t(23, 59, 59);

    t.inc_hour().inc_min().inc_sec();
t.show(); // 显示 24:0:0
    return 0;
}
```

**答案：**

```cpp
#include <iostream>

class Time {
private:
    int hr;
    int min;
    int sec;
public:
    Time(int h = 0, int m = 0, int s = 0);
    Time& inc_hour();
    Time& inc_min();
    Time& inc_sec();
    void show() const;
};

Time::Time(int h, int m, int s)
{
    hr = h;
    min = m;
    sec = s;
}
```

```cpp
Time& Time::inc_hour()
{
    hr++;
    return *this;
}
```

```cpp
Time& Time::inc_min()
{
    min++;
    if(min == 60) {
        min = 0;
        hr++;
    }
    return *this;
}
```

```cpp
Time& Time::inc_sec()
{
    sec++;
    if(sec == 60) {
        sec = 0;
        inc_min();
    }
    return *this;
}
```

```cpp
void Time::show() const
{
    std::cout << hr << ': ' << min << ': ' << sec << '\n';
}
```

**注释：** 连续使用 . 运算符意味着左侧必须有一个对象。因此，函数必须返回一个对象，特别是该对象的引用，因为对成员的修改必须在对象本身进行，而不是在其副本上。也就是说，看看你是否理解了上面的句子，如果我们将三个函数的返回类型从 Time& 改为 Time，程序将显示什么？不知道，自己找吧。

## C.17.11 完成以下类的公共部分，并编写一个程序，读取并将学生数据存储在包含 student 类型元素的 vector 中。如果用户输入负数成绩，则数据输入应终止。然后，程序应该调用一个排序函数，该函数接受 vector 作为参数并对其元素进行升序。排序元素时使用 C.12.5 中的选择排序算法。此外，该类应包含一个 show() 函数来显示学生数据。限制总共只能定义三个函数。

```cpp
class Student {
private:
    string name;
    float grd;
public:
    ...
};
```
