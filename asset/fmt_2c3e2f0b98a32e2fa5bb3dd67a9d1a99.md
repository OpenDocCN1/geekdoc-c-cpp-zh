
`cout` << "Allocation Failure\n";

return 1;

}

p->set(12387.87, "alice");

bal = p->get_bal();

`cout` << "balance is: " << bal << endl;

delete p;

}

//output

balance is: 12388

使用以下语法分配 `Balance` 对象：

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

### 使用单参数构造函数初始化数组

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

### 创建初始化和未初始数组

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

`Foo` 的数组声明：`Foo ar[9];` 将失败，因为数组中的每个对象都必须通过调用构造函数来实例化，而 `Foo` 没有适当的构造函数。只有当 `Foo` 也有一个无参数的构造函数时，编译才能成功。

我们可以通过重载 `Foo` 构造函数来指定任何处理初始化和未初始化对象的数组：

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

### 动态构建数组

假设我们动态创建一个包含五十个 `double` 值的数组。以下是在堆上分配此数组的语法：

```cpp
double* ptrMem = new double[50];
```

我们使用以下代码释放此内存分配：

```cpp
delete []ptrMem;
```

## C++ 指针

与变量指针一样，我们可以拥有指向对象的指针。给定一个对象的指针，我们使用箭头 (`->`) 运算符而不是点运算符 (`.`) 来访问对象的成员。以下程序说明了如何通过指针访问对象：

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

### 指针的递增

当指针递增时，它指向其所指类型的下一个元素。例如，整数指针将指向下一个整数。

通常，所有的指针运算都是相对于所指向对象的类型或原生类型的。

由于类型或类具有以字节为单位的大小，增加指针会将指针地址增加等于所指向类型或对象大小的字节数。

### 成员函数指针

假设我们有一个类 `Foo`，它包含一个公共成员函数 `add`，声明如下：`int add(int, int);`

那么，指向成员函数（如 `add`）的声明如下：

```cpp
return_type (Class_Name::* pointer_name)(Argument_List);
```

这表示 *pointer_name* 是指向指定类中某个成员函数的指针。

### this 指针

每个 C++ 对象都有一个 `this` 指针，它是指向对象本身的指针。该指针的值是对象的地址。

当调用非静态成员函数时，`this` 指针会自动作为隐式参数传递进去。

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

```cpp
return i*i;
```

注意，友元函数不是类的成员，因此它们不会被传递 *this* 指针。其次，静态成员函数没有 *this* 指针，因为它与任何实例化的对象没有唯一的关联。

# C++ 引用

C++ 包含一个与指针相关的重要特性，称为引用（references）。引用是一个隐式的指针变量，可以像操作它所指向的实际对象或变量一样对其操作。

创建引用变量的语法如下：

```cpp
#include <iostream>

int main() {
    int z = 5;
    int& x = z; // 或 int &x = z;
    std::cout << x << std::endl;
}
// 输出
5
```

在这里，`x` 是一个 `int` 类型变量的引用。引用变量在创建时必须初始化。引用变量在声明时，必须指向某个已初始化的变量。

像 `int& x = 5;` 这样的声明将无法编译，因为 5 是一个瞬时值，没有地址，因此无法被指向（这一点稍后将在右值相关的章节中详细讨论）。此外，字面量 5 一旦语句执行完毕就会消失。

使用引用变量有三种方式：作为函数参数、作为函数返回值以及作为独立变量。在之前的示例中，`x` 是一个独立的引用变量。

## 函数引用参数

引用变量最重要的用途是创建使用“引用传递”参数传递的函数。参数可以通过两种方式传递给函数：使用**值传递**（call by value）或使用**引用传递**（call by reference）。当使用值传递时，参数的拷贝会被传递给函数。而引用传递则将参数的地址传递给函数。

默认情况下，C++ 使用值传递来将参数传递给函数，但它也提供了两种通过引用传递参数的方法。首先，我们可以显式地将指针变量传递给函数。其次，我们可以指定函数接收一个引用参数。在大多数情况下，最佳实践是声明函数接收引用参数，而不是向函数传递指针。

下面的示例演示了如何使用指针实现引用传递。

```cpp
#include <iostream>
using namespace std;

// negative 函数的前向声明
void negative(int* i);

int main() {
    int x = 10;
    cout << "x is: " << x << endl;
    negative(&x);
}

void negative(int* i) {
    *i = -i;
    cout << "x in negative function is: " << *i << endl;
}

// 输出
x is: 10
x in negative function is: -10
```

在这个示例中，我们向函数 `negative` 传递了一个指针，并通过解引用指针打印了 `x` 的值。

要指定函数参数为引用变量，我们在参数名称前加上一个 `&`。例如，这里是如何将 `i` 声明为引用参数来指定 `negative`：

```cpp
void negative(int& i); // 或 void negative(int &i)
```

`i` 是一个隐式的指针变量，但可以像操作它指向的变量一样对其操作。一旦 `i` 变成引用，就不再需要（甚至不再允许）对其应用 `*` 指针解引用运算符了。`i` 是所指向变量的别名。也就是说，`i` 可以像变量本身一样被操作。此外，在调用 `negative` 时，不再需要（也不被允许）在参数名称前加上 `&` 地址操作符。我们传递实际变量 `x`。编译器静静地向函数传递一个隐式指针。

这里是上述程序的引用变量版本：

```cpp
#include <iostream>
using namespace std;

// negative 函数的前向声明
void negative(int& i);
int main() {
    int x = 10;
    cout << "x is: " << x << endl;
    negative(x);
    cout << "x after the call to negative is: " << x << endl;
}

void negative(int& i) {
    i = -i;
    cout << "i in negative function is: " << i << endl;
}

// 输出
x is: 10
i in negative function is: -10
x after the call to negative is: -10
```

注意，在 `negative` 内部更改引用参数 `i` 的值会改变 `x` 的值。这是因为 `negative` 隐式地接收了 `x` 的指针。

在 `negative` 函数内部，无法改变引用参数 `i` 所指向的内容。类似这样的语句：

`i++`:

在 `negative` 内部，`i++` 会增加变量 `i` 的值。它不会导致 `i` 指向新的位置。

## 将引用传递给对象

默认情况下，对象被传递给函数时，传递的是该对象的位拷贝。当函数结束时，拷贝的析构函数会被调用。如果我们不希望在函数结束时调用析构函数，可以传递对象的函数指针，或者通过引用传递对象。当我们通过引用传递对象时，不会创建对象的拷贝，而是向函数传递一个指向该对象的隐式指针。这意味着通过引用传递的对象在函数结束时不会被销毁。

在下面的示例中，对象 `bar` 被按值传递给对象 `foo` 内部的 `negative` 函数：

```cpp
#include <iostream>
using namespace std;

class Foo {
public:
    int x;
    Foo(int val) : x(val) {}
    ~Foo() { cout << "Foo destructor" << endl; }
};

void negative(Foo f) {
    f.x = -f.x;
}

int main() {
    Foo bar(10);
    cout << "before negative: " << bar.x << endl;
    negative(bar);
    cout << "after negative: " << bar.x << endl;
    return 0;
}
```

值为 5 的内存位置在语句执行完成后将不再存在。

以下展示了操作独立引用变量的示例：

```cpp
#include <iostream>
int main() {
    int a = 10;
    // 对 a 的独立引用
    int &r = a;

    // a 和 r 具有相同的值
    std::cout << "a: " << a << " ref: " << r << "\n";

    // 修改 r 的值会改变 a
    r = 100;
    std::cout << "a: " << a << " ref: " << r << "\n";

    // 将变量 b 的值赋给 r
    int b = 19;
    r = b;
    std::cout << "b: " << b << " a: " << a << " r: " << r << "\n";

    // 递减 r 也会递减 b
    r--;
    std::cout << "b: " << b << " r: " << r << "\n";

    // 输出
    a: 10 r: 10
    a: 100 r: 100
    b: 19 r: 19
    a: 18 r: 18
}
```

### 引用的限制

引用存在若干限制条件：

- 禁止空引用（隐式指针不能指向空）

- 我们不能引用一个引用。换句话说，我们无法获取引用的地址。

- 我们不能创建指向引用的指针

独立引用变量在声明时必须进行初始化。

### 悬空引用

悬空引用是指指向不存在或没有可寻址内存位置的引用变量。在下面的示例中，该函数返回了一个指向栈上局部值的引用：

```cpp
#include <iostream>
int& foo() {
    int x = 5;
    return x;
}
int main() {
    int& ret = foo();
    std::cout << ret << std::endl;
}
// 错误：返回了局部变量 x 的引用。
```

此程序将无法编译。返回值存在于栈上，并在函数返回后将消失。

### 从类成员函数返回常量引用

考虑以下程序：
