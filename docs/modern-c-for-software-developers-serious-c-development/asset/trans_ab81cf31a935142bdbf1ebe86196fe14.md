

```cpp
cout << "Original a, b: " << a << ' ' << b << '\n';

// 调用显式重载的 swaparaps()
swaparaps(i, j);
// 调用通用的 swaparaps()
swaparaps(x, y);
// 调用通用的 swaparaps()
swaparaps(a, b);

cout << "Swapped i, j: " << i << ' ' << j << '\n';
cout << "Swapped x, y: " << x << ' ' << y << '\n';
cout << "Swapped a, b: " << a << ' ' << b << '\n';

return 0;

// 输出
Original i, j: 20 10
Original x, y: 10.1 23.3
Original a, b: z x
Inside swaparaps for int specialization.
Inside template swaparaps.
Swapped i, j: 20 10
Swapped x, y: 23.3 10.1
Swapped a, b: z x
```

在上例中，由于显式的函数定义 `void swaparaps(int &&, int &b)`，编译器知道当 `swaparaps` 有两个参数时，它必须用显式特化的版本来重写通用函数。

我们可以通过以下三种方式之一声明显式 `swaparaps` 函数来指示显式特化：

```cpp
template<> void swaparaps<int, int>(int &a, int &b) {
or

void swaparaps<int, int>(int &a, int &b) {
or

void swaparaps(int&, int&) {...} // 普通函数
```

`template<>` 声明告知编译器正在进行显式声明。

# 函数模板的重载

我们可以根据函数参数的数量对函数模板进行重载：

```cpp
// 重载函数模板声明
#include <iostream>
using namespace std;

// func() 模板的第一个重载版本。
template <class Ttype>
void func(Ttype a)
{
    cout << "Inside func(Ttype a)";
}

// func() 模板的第二个重载版本。
template <class Ttype1, class Ttype2>
void func(Ttype1 a, Ttype2 b)
{
    cout << "Inside func(Ttype1 a, Ttype2 b)";
}
```

```cpp
int main()
{
    func(10);      // 调用 func(X)
    func(10, 20);  // 调用 func(X, Y)
    return 0;
}
```

```cpp
// 输出
Inside func(Ttype a)
Inside func(Ttype1 a, Ttype2 b)
```

# 在函数模板中使用普通参数

我们可以在函数模板中将普通参数与通用参数混合：

```cpp
// 在函数模板中使用普通参数
#include <iostream>
using namespace std;
```

```cpp
template<class Ttype>
void print(Ttype data, int val)
{
  if (val > 10) {
    cout << data << "\n";
  } else {
    cout << "invalid value" << "\n";
  }
}

int main() {
  print("This is a test", 11);
  return 0;
}
```

// 输出
This is a test

# C++ 模板：泛型类

类模板是一类类，其中类中处理的数据的实际类型被指定为通用参数。

当类使用可以泛化的逻辑时，类模板非常有用。例如，维护整数队列的算法对于字符队列也同样适用。

当我们创建一个类模板时，它可以为任何类型的数据执行执行我们定义的操作，例如维护一个队列或链表。编译器将根据我们在实例化对象时指定的类型，在编译时自动创建正确类型的对象。

类模板声明的通用形式为：

```cpp
template <Ttype>
class class-name {
.
}
```

这是一个声明，而不是定义。由于参数的类型 `Type` 是一个通用类型，因此此声明声明了一个由 `Type` 参数化的类族。定义则使用特定的模板类型来实例化对象。

当指定了特定的 `Type`（模板类型）时，就会实例化一个特定的类。如有必要，我们可以在模板声明中使用用逗号分隔的模板类型列表来指定多个泛型数据类型。

一旦我们定义了一个泛型类（模板类），就可以使用以下语法创建该类的特定实例：

```cpp
class-name<type> obj;
```

在这里，**type** 是类将要操作的数据类型。**class-name<type>** 决定了将要实例化对象类型。

泛型类的成员函数本身自动是泛型的。我们不需要像在类声明中那样使用函数模板来显式指定它们。

在下面的程序中，声明了一个栈模板类：

```cpp
#include <iostream>
using namespace std;

const int SIZE = 10;

// 声明一个栈模板类
template <class Ttype>
class Stack {
    Ttype my_stack[SIZE]; // 栈
    int num_el; // 栈中的元素数量
public:
    Stack() : num_el = 0; } // 构造函数
    void push(Ttype obj); // 入栈操作
    Ttype pop(); // 出栈操作
};

// 入栈函数
template <class Ttype>
void Stack<Ttype>::push(Ttype obj) {
    if (num_el == SIZE) {
        cout << "Stack is full.\n";
        return;
    }
    my_stack[num_el] = obj;
    num_el++;
}

// 出栈函数
template <class Ttype>
Ttype Stack<Ttype>::pop() {
  if (num_el == 0) {
    cout << "Stack is empty.\n";
    return Ttype();
  }
  num_el--;
  return my_stack[num_el];
}

int main() {
  // 使用两个栈进行演示。
  Stack<char> s1, s2;
```

