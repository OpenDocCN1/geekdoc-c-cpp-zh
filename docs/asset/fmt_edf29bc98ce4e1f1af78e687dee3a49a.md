
## C 和 C++ 之间的相似之处

- 两种语言都具有相似的语法。
- 两种语言的代码结构相似。
- 两种语言的编译方式相似。
- 它们共享相同的基本语法。几乎所有 `C` 的运算符和关键字在 `C++` 中都存在，且功能相同。
- `C++` 的语法比 `C` 略有扩展，但基础语法是相同的。
- 两者的基本内存模型都非常接近硬件。
- 两种语言都存在栈、堆、文件作用域和静态变量的概念。

## C 和 C++ 之间的差异

| C | C++ |
| :--- | :--- |
|  |  |

### 示例 3：创建可变变量的 C++ 程序

```cpp
#include<iostream>
using namespace std;
class test
{
    mutable int a;
    int b;
public:
    test(int x,int y)
    {
        a=x;
        b=y;
    }
    void square_a() const
    {
        a=a*a;
    }
    void display() const
    {
        cout<<"a = "<<a<<endl;
        cout<<"b = <<b<<endl;
    }
};
int main()
{
    const test x(2,3);
    cout<<"Initial value"<<endl;
    x.display();
    x.square_a();
    cout<<"Final value"<<endl;
    x.display();
    return 0;
}
```

程序中定义了一个类 `test`。它包含一个可变数据成员 `a`。创建了类 `test` 的常量对象 `x`，并使用用户定义的构造函数初始化数据成员的值。由于 `b` 是普通数据成员，其值在初始化后无法更改。然而由于 `a` 是可变的，其值可以被更改，这通过调用 `square_a()` 方法实现。`display()` 方法用于显示数据成员的值。

```
Initial value
a = 2
b = 3
Final value
a = 4
b = 3
```

## 静态存储类声明语法

```
static datatype var_name1 [= value];
```

示例：

```
static int x = 101;
static float sum;
```

### 寄存器存储类 Register
寄存器存储将变量分配在 CPU 寄存器而非主内存中。它的生命周期和可见性与自动变量相同。创建寄存器变量目的是提高访问速度并使程序运行更快。如果寄存器中没有空间，这些变量将存储在主内存中，作用类似于自动存储类变量。因此，只有需要快速访问的变量才应该设为寄存器。

## 寄存器存储类声明语法

```
register datatype var_name [= value];
```

示例：

```cpp
register int id;
register char a;
```

### 存储类示例

示例 2：创建自动、全局、静态和寄存器变量的 C++ 程序。

```cpp
#include<iostream>
using namespace std;
int g; //全局变量，初始值为 0
void test_function()
{
    static int s; //静态变量，初始值为 0
    register int r; //寄存器变量
    r=5;
    s=s+r*2;
    cout<<"Inside test_function"<<endl;
    cout<<"g = "<<g<<endl;
    cout<<"s = "<<s<<endl;
    cout<<"r = "<<r<<endl;
}
int main() {
    int a; //自动变量
    g=25;
    a=17;
    test_function();
    cout<<"Inside main"<<endl;
    cout<<"a = "<<a<<endl;
    cout<<"g = "<<g<<endl;
    test_function();
    return 0;
}
```
