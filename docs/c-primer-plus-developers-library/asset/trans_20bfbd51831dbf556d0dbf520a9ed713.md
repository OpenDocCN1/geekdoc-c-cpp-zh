
删除了 allcaps() 返回的临时对象。（一个实在缺乏灵感的编译器甚至可能把 temp 复制到一个临时返回对象，删除 temp，然后再删除该返回对象。）关键在于，这里浪费了大量工作。由于临时对象被删除，如果编译器能把数据的所有权直接转移给 vstr_copy2，岂不是更好？也就是说，与其把 20,000,000 个字符复制到新位置再删除旧位置，不如让这些字符留在原处，并给它们附上 vstr_copy2 标签。这类似于把一个文件从一个目录移动到另一个目录时发生的情况：实际文件仍留在硬盘上的原处，只是更改了簿记信息。这种方法称为移动语义。有点矛盾的是，移动语义实际上避免了移动主要数据；它只是调整簿记信息。

要实现移动语义，我们需要一种方法让编译器知道何时需要执行真正的复制、何时不需要。右值引用就在这里发挥作用。我们可以定义两个构造函数。一个是常规复制构造函数，可以使用通常的 const 左值引用作为参数。这个引用将绑定到左值实参，例如语句 #1 中的 vstr。另一个称为移动构造函数，可以使用右值引用，并且可以绑定到右值实参，例如语句 #2 中 allcaps(vstr) 的返回值。复制构造函数可以执行通常的深复制，而移动构造函数只需调整簿记信息。移动构造函数在将所有权转移给新对象的过程中可能会修改其参数，这意味着右值引用参数不应为 const。

## 移动示例

让我们看一个示例，了解移动语义和右值引用如何工作。程序清单 18.2 定义并使用了 Useless 类，该类包含动态内存分配、常规复制构造函数，以及使用移动语义和右值引用的移动构造函数。为了说明所涉及的过程，构造函数和析构函数异常冗长，并且该类使用一个静态变量来跟踪对象数量。此外，一些重要方法（如赋值运算符）被省略了。（尽管有这些省略，也不应把 Useless 类与环保的 Use_Less 类混淆。）

程序清单 18.2  useless.cpp

```cpp
// useless.cpp -- an otherwise useless class with move semantics
#include <iostream>
using namespace std;

// interface
class Useless
{
private:
    int n;          // number of elements
    char * pc;      // pointer to data
    static int ct;  // number of objects
    void ShowObject() const;
public:
    Useless();
    explicit Useless(int k);
    Useless(int k, char ch);
    Useless(const Useless & f);     // regular copy constructor
    Useless(Useless && f);          // move constructor
    ~Useless();
    Useless operator+(const Useless & f)const;
    // need operator= in copy and move versions
    void ShowData() const;
};


// implementation
int Useless::ct = 0;

Useless::Useless()
{
    ++ct;
    n = 0;
    pc = nullptr;
    cout << "default constructor called; number of objects: " << ct << endl;
    ShowObject();
}

Useless::Useless(int k) : n(k)
{
    ++ct;
    cout << "int constructor called; number of objects: " << ct << endl;
    pc = new char[n];
    ShowObject();
}

Useless::Useless(int k, char ch) : n(k)
{
    ++ct;
    cout << "int, char constructor called; number of objects: " << ct
         << endl;
    pc = new char[n];
    for (int i = 0; i < n; i++)
        pc[i] = ch;
    ShowObject();
}

Useless::Useless(const Useless & f) : n(f.n)
{
    ++ct;
    cout << "copy const called; number of objects: " << ct << endl;
    pc = new char[n];
    for (int i = 0; i < n; i++)
        pc[i] = f.pc[i];
    ShowObject();
}

Useless::Useless(Useless && f): n(f.n)
{
    ++ct;
    cout << "move constructor called; number of objects: " << ct << endl;
    pc = f.pc;       // steal address
    f.pc = nullptr;  // give old object nothing in return
    f.n = 0;
    ShowObject();
}

Useless::~Useless()
{
    cout << "destructor called; objects left: " << --ct << endl;
    cout << "deleted object:\n";
    ShowObject();
    delete [] pc;
}

Useless Useless::operator+(const Useless & f)const
{
    cout << "Entering operator+()\n";
    Useless temp = Useless(n + f.n);
    for (int i = 0; i < n; i++)
        temp.pc[i] = pc[i];
    for (int i = n; i < temp.n; i++)
        temp.pc[i] = f.pc[i - n];
    cout << "temp object:\n";
    cout << "Leaving operator+()\n";
    return temp;
}

void Useless::ShowObject() const
{
    cout << "Number of elements: " << n;
    cout << " Data address: " << (void *) pc << endl;
}

void Useless::ShowData() const
{
    if (n == 0)
        cout << "(object empty)";
    else
        for (int i = 0; i < n; i++)
            cout << pc[i];

    cout << endl;
}

// application
int main()
{
    {
        Useless one(10, 'x');
        Useless two = one;          // calls copy constructor
        Useless three(20, 'o');
        Useless four (one + three);  // calls operator+(), move constructor
        cout << "object one: ";
        one.ShowData();
        cout << "object two: ";
        two.ShowData();
        cout << "object three: ";
        three.ShowData();
        cout << "object four: ";
        four.ShowData();
    }
}
```

关键定义是两个复制/移动构造函数的定义。首先，去掉输出语句后，复制构造函数如下：

```cpp
Useless::Useless(const Useless & f): n(f.n)
{
    ++ct;
    pc = new char[n];
    for (int i = 0; i < n; i++)
        pc[i] = f.pc[i];
}
```

它执行通常的深复制，并且是下面语句所使用的构造函数：

```cpp
Useless two = one;          // calls copy constructor
```

引用 f 指向左值对象 one。

接下来，同样去掉输出语句后，移动构造函数如下：

```cpp
Useless::Useless(Useless && f): n(f.n)
{
    ++ct;
    pc = f.pc;       // steal address
    f.pc = nullptr;  // give old object nothing in return
    f.n = 0;
}
```

它通过让 pc 指向该数据来取得现有数据的所有权。此时，pc 和 f.pc 都指向同一数据。当调用析构函数时，这会很麻烦，因为程序不应针对同一地址调用两次 delete []。为避免这个问题，构造函数随后把原指针设为空指针，因为对空指针应用 delete [] 并不是错误。这种取得所有权的做法通常称为“窃取”。代码还把原对象中的元素计数设为 0。这不是必需的，但它使我们示例的输出看起来更自洽。注意，对 f 对象的修改要求在参数声明中不使用 const。

下面的语句使用的正是这个构造函数：

```cpp
Useless four (one + three);   // calls move constructor
```

表达式 one + three 调用 Useless::operator+()，而右值引用 f 绑定到该方法返回的右值临时对象。

下面是使用 Microsoft Visual C++ 2010 编译该程序时的输出：

```
int, char constructor called; number of objects: 1
Number of elements: 10 Data address: 006F4B68
copy const called; number of objects: 2
Number of elements: 10 Data address: 006F4BB0
int, char constructor called; number of objects: 3
Number of elements: 20 Data address: 006F4B98
Entering operator+()
int constructor called; number of objects: 4
Number of elements: 30 Data address: 006F4C48
temp object:
Leaving operator+()
move constructor called; number of objects: 5
Number of elements: 30 Data address: 006F4C48
destructor called; objects left: 4
deleted object:
Number of elements: 0 Data address: 00000000
object one: xxxxxxxxxx
object two: xxxxxxxxxx
object three: oooooooooooooooooooooooo
object four: xxxxxxxxxxxxxxxxxxxxxxxxxxxxx
destructor called; objects left: 3
```
