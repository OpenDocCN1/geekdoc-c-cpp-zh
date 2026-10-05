

# 对象数组

对象数组是一个元素为对象的数组。例如，在程序 C.17.1 中，语句：

`Student s[10];` 将 s 声明为包含十个元素的数组，其中每个元素都是一个 Student 对象。创建的每个对象都会调用默认构造函数，也就是说，调用了十次。通常情况下，我们可以使用相同或不同的构造函数来初始化数组。例如：

```cpp
#include <iostream> // 示例 17.13
```

```cpp
class Test {
public:
    int a, b;
    Test() {a=b=1};
    Test(int i, int j) {a=i; b=j};
};
```

```cpp
int main() {
    int i;
    Test t[10] = {Test(1, 2), Test(), Test(5, 6)};

    for(i = 0; i < 10; i++)
        std::cout << t[i].a << ' ' << t[i].b << '\n';

    return 0;
}
```

第二个构造函数被 t[0] 和 t[2] 调用，而默认构造函数被 t[1] 调用。由于初始化列表短于元素个数，剩余七个对象将调用默认构造函数。如果缺少该构造函数，编译器将显示错误信息。该程序显示了每个对象成员的值。

如果我们写：`Test *p = new Test[3];`，会调用哪个构造函数？默认构造函数。调用多少次？三次，每个对象一次。如果缺少默认构造函数呢？在这种情况下，我们应该使用构造函数。这是一个初始化示例：

```cpp
Test *p = new Test[3]{{1, 2}, {3, 4}, {5, 6}}; /* 第一个对象的 a 和 b 分别变为 1 和 2。另外两个对象也是如此。 */
```

当我们写 `delete[p];` 时，会调用哪个函数？默认析构函数，同样调用了三次。按什么顺序？正如我们所说的，析构函数是按照构造顺序的反序调用的，也就是说 p[2] 先被销毁，p[0] 最后销毁。

或者，正如我们所知，可以使用元素类型为 Test 的 vector 对象。例如：

```cpp
int main() {
    int i;
    std::vector<Test> v;
    Test t1(2
for(i = 0; i < v.size(); i++)
    std::cout << v[i].a << ' ' << v[i].b << '\n';
return 0;
}
```

# 类常量

在声明类时，我们可能想要使用一些常数。我们可以使用全局变量，但由于它们只在类内部使用，符合封装理念的做法是将它们定义在类内部。例如，假设我们想用一个常量指定数组的大小。因为这个常量对于所有对象都是相同的，它会被创建一次并由所有对象共享。例如，我们会写类似：

```cpp
class T
private:
    const int SIZE = 10;
    int arr[SIZE]; // 错误。
...;
```

其中 SIZE 变量将由所有 T 对象创建并共享。然而，这是不允许的，因为类的声明并没有创建对象来为 SIZE 及其值预留内存，它描述的是类的结构。我们可以做什么呢？在类中定义常量的一种方法是声明一个枚举。例如：

```cpp
class T
private:
    enum {SIZE = 10};
    int arr[SIZE];
...;
```

枚举并没有创建类的成员。枚举并不包含在类类的每一个对象中。简单来说，SIZE 是一个符号名称，每当编译器在类作用域内遇到它时，就会将其替换为 10。
另一种方法是使用静态常量（static constant）。事实上，静态成员通常用于定义常量。这是有意义的，因为不需要在每次创建对象时都创建一个相同常量变量的副本。通过将其定义为静态，只会创建一个该常量的实例，并在对象之间共享。正如我提到的，我倾向于用大写字母写常量，以便它们在程序中脱颖而出。

```cpp
#include <iostream> // 示例 17.14
class T
public:
    static int SIZE = 10; // 错误，它不是 const。
    static const int SIZE = 10; // OK。我们也可以用 constexpr 代替 const.*
    int arr[SIZE];
    void f();
;
```

```cpp
void T::f()
{
    for(int i = 0; i < SIZE; i++)
        arr[i] = i+SIZE;
    std::cout << arr[SIZE-1] << '\n';
}
```

```cpp
int main()
{
    T t;
    t.f();
    std::cout << SIZE << '\n'; // 错误，超出作用域。
    return 0;
}
```

现在，只创建了一个名为 SIZE 的常量，它被所有 T 对象共享。正如我们在下一节看到的，SIZE 并不存储在每个对象中，而是存储在类作用域内 SIZE 可见的同一块内存区域，并且 f() 输出 19。注释说，如果你尝试在类外使用它，编译器将显示错误信息。如果你在该处使用作用域运算符或 T::SIZE，则没有问题。

关于初始化，有一些限制。例如，静态常量的类型必须是整数、枚举或 constexpr 表达式，且初始值必须是常量。

```cpp
class T
{
    static const int PI = 3; // OK。
    static const float PI = 3.14; // 错误。
    static constexpr float PI = 3.14; // OK。
}
```

初始化规则在 C++17 和内联变量（inline variables）引入后得到了简化。它允许我们无视类型初始化变量。例如，我们可以写：

```cpp
class T
{
    static inline const float PI = 3.14; // OK，从 C++17 起。
}
```

static、inline 和 const 关键字的顺序并不重要。

# 静态成员变量

当我们要在类中声明一个被类所有对象共享的变量时，我们将其声明为静态（static）。静态成员创建一次并被所有对象共享。它属于整个类，而不是某个特定的对象。为了向你展示一个示例，让我们声明 test.h：

```cpp
#ifndef TEST_H
#define TEST_H

class T
{
private:
    int v;
    double d;
public:
    static int num; // 声明静态变量。
    void set() {v = num};
}

#endif
```

```cpp
#include <iostream> // 示例 17.15
#include "test.h"

int T::num = 5; // 定义静态变量。
```

```cpp
int main() {
    T t[10];

    t[2].num = 20; // 另一种方法是 T::num = 20;
    std::cout << t[5].num << '\n';
    return 0;
}
```

此类静态变量的内存在程序开始时预留，就像全局变量一样。因此，即使没有创建对象，num 也会被定义并为其预留内存。如果你不给它分配初始值，int T::num 将变为 0。类成员（例如 set()）可以直接访问静态变量，无需使用 :: 运算符。

我们也看到静态变量不是对象的独立成员，可以使用对象（如 t[2]，或指针或对象引用）来访问它。为了清楚该变量是静态的，我倾向于使用类和 :: 运算符的语法（例如 T::num）。

正如我们所说，静态常量可以在类内初始化。这对于非常量静态变量是不允许的，尽管它必须在类外定义。C++17 通过引入内联变量放宽了这一要求并简化了定义。特别是，

