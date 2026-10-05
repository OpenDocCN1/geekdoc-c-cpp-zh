

int main()
{
    Balance *p;
    double bal;

    try {
        p = new Balance;
    } catch (bad_alloc& xa) {
        cout << "Allocation Failure\n";
        return 1;
    }

    p->set(12387.87, "alice");
    bal = p->get_bal();
    cout << "balance is: " << bal << endl;
    delete p;
}

//output
balance is: 12388

使用以下语法分配 Balance 对象：

p = new Balance;

删除该对象的语法为：

delete p;

## C++ 数组

在 C++ 中，可以拥有对象数组。声明和使用对象数组的语法与任何其他类型的数组相同。在接下来的示例中，我们创建了一个包含三个 *Foo* 类型类型对象的数组：

```cpp
#include <iostream>
using namespace std;

class Foo
{
    int i;
public:
    void set(int j) { i=j; }
    int get() { return i; }
};

int main() {
    Foo foo[3];
    int i;

    for (i = 0; i < 3; i++) foo[i].set(i+1);
    for (i = 0; i < 3; i++)
        cout << foo[i].get() << " ";
}

// output
1 2 3
```

## 使用单参数构造函数初始化数组

如果类 *Foo* 包含一个单参数构造函数，那么 *Foo* 对象数组可以按如下方式初始化：

```cpp
#include <iostream>
using namespace std;

class Foo
{
    int i;
public:
    Foo(int j) { i=j; } // 单参数构造函数
    int get() { return i; }
};

int main() {
  Foo obj[3] = {1, 2, 3}; // 初始化列表
  int i;

  for(i = 0; i < 3; i++)
    cout << obj[i].get() << " ";

  return 0;
}
```

如果类构造函数有两个或更多参数，我们必须使用以下初始化语法：

```cpp
#include <iostream>
using namespace std;

class Foo {
  int h;
  int i;
public:
  // 带有2个参数的构造函数
  Foo(int j, int k) { h=j; i=k; }
  int get_i() { return i; }
  int get_h() { return h; }
};

int main() {
  Foo obj[3] = {
    Foo(1, 2), // 构造函数的初始化列表
    Foo(3, 4),
    Foo(5, 6)
  };

  int i;
  for (i = 0; i < 3; i++) {
    cout << obj[i].get_h();
    cout << ", ";
    cout << obj[i].get_i() << "\n";
  }
}

// output
1, 2
3, 4
5, 6
```

## 创建初始化和未初始数组

当我们想要同时创建初始化和未初始对象数组时，就会出现特殊情况。考虑以下类：

```cpp
class Foo
{
    int i;
public:
    Foo(int j) { i=j }
    int get() { return i; }
};
```

Foo 的数组声明：`Foo ar[9];` 将失败，因为数组中的每个对象都必须通过调用构造函数来实例化，而 Foo 没有适当的构造函数。只有当 Foo 也有一个无参数的构造函数时，编译才能成功。

我们可以通过重载 Foo 构造函数来指定任何处理初始化和未初始化对象的数组：

```cpp
class Foo
{
    int i;
public:
    // 用于未初始化数组的构造函数
    Foo() { i = 0; }

    // 用于初始化数组的构造函数
    Foo(int j) { i = j; }
    int get_i() { return i; }
};
```

给定该类声明，以下是有效的对象实例化：

```cpp
Foo a[3] = {3, 5, 6};      // 初始化数组
Foo b[34];                   // 未初始化数组
```

## 动态构建数组

假设我们动态创建一个包含五十个 double 值的数组。以下是在堆上分配此数组的语法：

```cpp
double* ptrMem = new double[50];
```

我们使用以下代码释放此内存分配：

```cpp
delete []ptrMem;
```

## C++ 指针

与变量指针一样，我们可以拥有指向对象的指针。给定一个对象的指针，我们使用箭头 (->) 运算符而不是点运算符 (.) 来访问对象的成员。以下程序说明了如何通过指针访问对象：

```cpp
#include <iostream>
class Foo {
    int i;
public:
    Foo(int j) { i=j; }
    int get() { return i; }
};

int main() {
    // p 是指向 Foo 对象的指针
    Foo* p;
    Foo obj(77);

    // 获取 obj 的地址
    p = &obj;

    // 使用 -> 调用 get()
    std::cout << p->get() << std::endl;
    return 0;
}

// output
```

## 指针的递增

当指针递增时，它指向其所指类型的下一个元素。例如，整数指针将指向下一个整数。

通常，所有的指针运算都是相对于所指向对象的类型或原生类型的。

由于类型或类具有以字节为单位的大小，增加指针会将指针地址增加等于所指向类型或对象大小的字节数。

## 成员函数指针

假设我们有一个类 Foo，它包含一个公共成员函数 add，声明如下：`int add(int, int);`

那么，指向成员函数（如 add）的声明如下：

```cpp
return_type (Class_Name::* pointer_name)(Argument_List);
```

这表示 *pointer_name* 是指向指定类中某个成员函数的指针。

## this 指针

每个 C++ 对象都有一个 this 指针，它是指向对象本身的指针。该指针的值是对象的地址。

当调用非静态成员函数时，this 指针会自动作为隐式参数传递进去。

考虑以下程序：

```cpp
#include <iostream>

class Foo {
    int i;
public:
    Foo(int x) { i = x; } // 隐式传递 this 指针
    int square() {
        return this->i*this->i;
    }
};

int main() {
    Foo foo(5);
    std::cout << foo.square() << std::endl;
}

// output
25
```

