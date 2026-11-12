
```cpp
struct A
{
    int m;

    A(int i) : m(i)
    {
        std::cout << "A("
            << m << ")" << std::endl;
    }

    ~A()
    {
        std::cout << "~A()" << std::endl;
    }

    operator bool()
    {
        return m != 0;
    }
};

void func()
{
    int i = 10;

    while(A a = i)
    {
        i = 0;
    }
}

int main()
{
    func();
}
```

### 问题94的解答

程序的输出是：

```
A(10)
~A()
A(0)
~A()
```

在条件中创建的变量会在循环的每次迭代中被销毁并重新创建。

在while循环中，构造函数和析构函数各被调用两次：一次用于条件成功时，一次用于条件失败时。

### \*\*\* 问题95：模拟while循环

模拟前一个程序中的while循环。

### 问题95的解答

### 程序8.76：模拟while循环

```cpp
#include <iostream>

struct A
{
    int m;

    A(int i) : m(i)
    {
        std::cout << "A("
                  << m << ")" << std::endl;
    }

    ~A()
    {
        std::cout << "~A()" << std::endl;
    }

    operator bool()
    {
        return m != 0;
    }
};

void func_simulate()
{
    int i = 10;

label:
    {
        A a = i;

        if (a)
        {
            i = 0;
            goto label;
        }
    }
}

int main()
{
    func_simulate();
}
```

### \* 问题96：范围for循环

给定如下整数数组，编写一个使用范围for循环打印其内容的程序：

```cpp
int array[5] = { 1, 2, 3, 4, 5 };
```

### 问题96的解答

```cpp
for (int& x : array)
    std::cout << x << std::endl;
```

### \*\*\* 问题97：模拟范围for循环

使用简单的for循环语句模拟范围for循环。范围for语句有两种：

- 1. for ( for-range-declaration : expression ) statement
- 2. for ( for-range-declaration : braced-init-list ) statement

### 问题97的解答

这两种都可以像下面这样模拟：

```cpp
{
    auto && range = range-init;

    for ( auto begin = std::begin(range),
               end = std::end(range);
          begin != end; ++begin )
    {
        for-range-declaration = *begin;
        statement
    }
}
```

### \* 问题98：返回花括号初始化列表

下面的程序有效吗？

### 程序8.77：返回花括号初始化列表

```
1 #include <utility>
2 #include <string>
3
4 std::pair<std::string, int>
5 func(const char* p, int x)
6 {
7     return {p, x};
8 }
```

### 问题98的解答

是的。

使用花括号初始化列表的返回语句会通过复制列表初始化，从指定的初始化器列表初始化要从函数返回的对象或引用。

### \* 问题99：属性

下面的程序有效吗？

### 程序8.78：指定属性

```
1 [[noreturn, nothrow]] void f [[noreturn]] ();
```

### 问题99的解答

是的。

### \*\* 问题100：typedef与const

在下面的程序中，pointer_to_char是什么？

- char* const，还是
- const char*

```
typedef char* pointer_to_char;
void func(const pointer_to_char);
```

### 问题100的解答

pointer_to_char 是 char* const。

### \*\* 问题101：存储类说明符

可用的存储类说明符有多少种？

### 问题101的解答

存储类说明符包括：

- 1. register
- 2. static
- 3. thread_local
- 4. extern
- 5. mutable

### \*\*\* 问题102：内联函数

什么是内联函数？

### 问题102的解答

- 带有inline说明符的函数声明声明了一个内联函数。
- inline说明符向实现表明，在调用点对函数体进行内联替换应优先于通常的函数调用机制。实现并不要求在调用点执行这种内联替换。
- 在类定义中定义的函数是内联函数。inline说明符不能出现在块作用域的函数声明上。
- 如果在友元声明中使用了inline说明符，那么该声明将是一个定义，或者该函数先前已被声明为inline。
- 内联函数在其被odr使用的每个翻译单元中都有定义，并且在每种情况下都具有完全相同的定义。
- 如果具有外部链接的函数在一个翻译单元中被声明为inline，那么它在所有出现该函数的翻译单元中都被声明为inline。
- 具有外部链接的内联函数在所有翻译单元中应具有相同的地址。
- 外部内联函数中的静态局部变量始终引用同一个对象。
- 外部内联函数体中的字符串字面量在不同翻译单元中是同一个对象。
- 在外部内联函数体内定义的类型在每个翻译单元中是相同的类型。

## 第9章

## 常量表达式

### \*\*\* 问题103：constexpr基础

constexpr 可以应用于以下哪些情况？

- 1. 类声明
- 2. 类定义
- 3. 对象的定义
- 4. 函数声明
- 5. 函数定义
- 6. 函数参数
- 7. 函数模板的声明
- 8. 函数模板的定义
- 9. 字面量类型的静态数据成员的声明

### 问题103的解答

- 1. 不可以

  下面的代码是错误的，因为A是类型A的声明。

  ```cpp
  constexpr struct A;
  ```

- 2. 不可以

  下面的代码是错误的，因为A是类型A的定义。

  ```cpp
  constexpr struct A {};
  ```

- 3. 可以

  ```cpp
  constexpr A a;
  constexpr int i = 10;
  ```

- 4. 可以

  ```cpp
  constexpr void func();
  struct A
  {
      constexpr void g();
  };
  ```

- 5. 可以

  ```cpp
  constexpr void func() {}
  ```

- 6. 不可以

  下面的代码是错误的，因为constexpr被应用于函数*func*的整数参数i。

  ```cpp
  void func(constexpr int i) {}
  ```

- 7. 可以
- 8. 可以
- 9. 可以

### 问题106的解答

在非构造函数的函数声明中使用的constexpr说明符将该函数声明为constexpr函数。

- constexpr函数隐式地是内联的。
- 它不能是虚函数。
- 它的返回类型是字面量类型或对字面量类型的引用。
- 它的每个参数类型都是字面量类型或对字面量类型的引用。
- 它的函数体是：

  ```cpp
  { return constant-expression ; }
  ```

### \*\*\* 问题107：constexpr函数的使用

以下哪些是有效的*constexpr函数*？

- 1.

  ```cpp
  constexpr int square(int x)
  {
      return x * x;
  }
  ```

- 2.

  ```cpp
  constexpr long long_max()
  {
      return 2147483647;
  }
  ```

- 3.

  ```cpp
  constexpr int abs(int x)
  {
      return x < 0 ? -x : x;
  }
  ```

- 4.

  ```cpp
  constexpr void f(int x) {}
  ```

- 5.

  ```cpp
  constexpr int prev(int x)
  {
      return --x;
  }
  ```

- 6.

  ```cpp
  constexpr int func(int x)
  {
      int y = x;
      return y;
  }
  ```

### 问题107的解答

- 1. 正确
- 2. 正确
- 3. 正确
- 4. 错误，因为返回类型是void。
- 5. 错误，因为使用了递减操作
- 6. 错误，因为函数体不仅仅包含return表达式。

### \*\*\* 问题108：constexpr构造函数

什么是*constexpr构造函数*？

### 问题108的解答

在构造函数声明中使用的constexpr说明符将该构造函数声明为constexpr构造函数。

- constexpr构造函数隐式地是内联的。
- 它的每个参数类型都是字面量类型或对字面量类型的引用。
- 它的函数体不能是函数try块。

