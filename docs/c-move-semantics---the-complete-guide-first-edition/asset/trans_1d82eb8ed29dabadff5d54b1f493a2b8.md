
#### 2.3.3 对象对自身的移动赋值

被移动后的对象处于有效但未指定状态的规则，通常也适用于直接或间接自移动之后的对象。

例如，在执行以下语句后，对象 x 通常是有效的，但其值未知：

```cpp
x = std::move(x);    // afterwards x is valid but has an unclear value
```

同样，C++标准库对其对象保证了这一点。[^1] 用户定义类型通常也应提供这一保证，但有时你必须实现一些内容来修正默认生成的被移动后状态。

### 2.4 通过不同引用进行重载

引入右值引用之后，我们现在有三种主要的按引用调用方式：

- `void foo(const std::string& arg)` 将实参作为 const 左值引用接收。
    
    这意味着你对传入的实参只有读访问权限。注意，如果类型匹配，你可以将一切内容传给这样声明的函数：
    - 可修改的具名对象
    - const 具名对象
    - 没有名称的临时对象
    - 用 `std::move()` 标记的对象
    
    语义含义是，我们给予 `foo()` 对传入实参的读访问权限。该参数就是我们所说的*输入*参数。

- `void foo(std::string& arg)` 将实参作为非 const 左值引用接收。
    
    这意味着你对传入的实参有写访问权限。注意，即使类型匹配，你也不能再将一切内容传给这样声明的函数。你只能传入：
    - 可修改的具名对象
    
    对于所有其他实参，调用无法编译。
    
    语义含义是，我们给予 `foo()` 对传入实参的读/写访问权限。该参数就是我们所说的*输出*或*输入/输出*参数。

- `void foo(std::string&& arg)` 将实参作为非 const 右值引用接收。
    
    这也意味着你对传入的实参有写访问权限。然而，你同样对可以传入的内容有限制。你只能传入：
    - 没有名称的临时对象
    - 用 `std::move()` 标记的非 const 对象
    
    语义含义是，我们给予 `foo()` 对传入实参的写访问权限，以夺取其值。它是一个*输入参数*，附加约束是调用方不再需要该值。
    
    注意，右值引用绑定到的实参与非 const 左值引用不同。因此，我们不得不引入一种新语法，而不能仅将移动语义实现为修改传入实参的函数的另一种方式。

#### 2.4.1 `const` 右值引用

从技术上讲，还有第四种按引用调用方式：

- `void foo(const std::string&& arg)` 将实参作为 const 右值引用接收。
    
    这也意味着你对传入的实参有读访问权限。这里的限制将是，你只能传入：
    - 没有名称的临时对象
    - 用 `std::move()` 标记的 const 或非 const 对象
    
    然而，这种情况没有有用的语义含义。作为右值引用，允许夺取值，但由于是 const，我们禁止对传入实参进行任何修改。这本身就是矛盾。

尽管如此，创建具有此行为的对象相当容易：只需用 `std::move()` 标记一个 const 对象：

```cpp
const std::string s{"data"};
...
foo(std::move(s));        // would call a function declared as const rvalue reference
```

当声明一个函数以 const 返回值时，这可能间接发生：

```cpp
const std::string getValue();
...
foo(getValue());          // would call a function declared as const rvalue reference
```

从语义上讲，这种情况通常由函数的 const 左值引用重载来覆盖，以提供读访问。针对这种情况的具体实现是可能的，但通常没有意义（C++标准库类 `std::optional<>` 使用了 const 右值引用）。

### 2.5 按值传递

如果你声明一个函数按值接收实参，移动语义也可能（自动）被使用。例如：

```cpp
void foo(std::string str);  // takes the object by value
...
std::string s{"hello"};
...
foo(s);                      // calls foo(), str becomes a copy of s
foo(std::move(s));           // calls foo(), s is moved to str
foo(returnStringByValue());  // calls foo(), return value is moved to str
```

如果调用方表示它不再需要传入实参的值（通过使用 `std::move()` 或传入没有名称的临时对象），则参数 `str` 会用从传入实参移动而来的值初始化。

这意味着，借助移动语义，如果传入的是临时对象，或者传入的实参用 `std::move()` 标记，按值调用可能会突然变得廉价。注意，就像按值返回局部对象一样，这种移动可以被优化掉。然而，如果没有被优化掉，现在可以保证该调用是廉价的（如果移动语义本身廉价）。

注意以下区别：

```cpp
void fooByVal(std::string str);        // takes the object by value
void fooByRRef(std::string&& str);     // takes the object by rvalue reference
...
std::string s1{"hello"}, s2{"hello"};
...
fooByVal(std::move(s1));               // s1 is moved
fooByRRef(std::move(s2));              // s2 might be moved
```

这里，我们比较两个函数：一个按值接收字符串，另一个将字符串作为右值引用接收。在两种情况下，我们都用 `std::move()` 传入一个字符串。

- 按值接收字符串的函数将使用移动语义，因为会用传入实参的值创建一个新字符串。
- 将字符串作为右值引用接收的函数**可能**使用移动语义。传入实参不会创建新字符串。传入实参的值是否被夺取/修改取决于函数的实现。

因此：

- 声明为支持移动语义的函数**可能不会**使用移动语义。
- 声明为按值接收实参的函数**会**使用移动语义。

再次注意，移动语义的效果并不保证会发生任何优化，也不保证任何优化的效果是什么。我们只知道，传入的对象随后处于有效但未指定的状态。

### 2.6 总结

- 右值引用用 `&&` 声明，且不带 `const`。
- 它们可以由没有名称的临时对象或用 `std::move()` 标记的非 const 对象初始化。
- 右值引用延长了按值返回的对象的生命周期。
- `std::move()` 是对相应右值引用类型的 `static_cast`。这允许我们将具名对象传给右值引用。
- 用 `std::move()` 标记的对象也可以传给按 `const` 左值引用接收实参、但不按非 const 左值引用接收实参的函数。
- 用 `std::move()` 标记的对象也可以传给按值接收实参的函数。在这种情况下，会使用移动语义初始化参数，这可以使按值调用相当廉价。
- `const` 右值引用是可能的，但针对它们实现通常没有意义。
- 被移动后的对象应处于*有效但未指定*的状态。C++标准库对其类型保证了这一点。只要不对其值作任何假设，你仍然可以（重新）使用它们。

本页有意留空

## 第3章：类中的移动语义

本章展示类如何从移动语义中受益。它演示普通类如何自动从移动语义中受益，以及如何在类中显式实现移动操作。

### 3.1 普通类中的移动语义

假设你有一个相当简单的类，其成员类型中移动语义可能带来差异：

`basics/customer.hpp`

```cpp
#include <string>
#include <vector>
#include <iostream>
#include <cassert>

class Customer {
private:
    std::string name;       // name of the customer
    std::vector<int> values; // some values of the customer
public:
    Customer(const std::string& n)
      : name{n} {
        assert(!name.empty());
    }

    std::string getName() const {
        return name;
    }

    void addValue(int val) {
```

[^1]: 被移动后的库对象的保证已通过*库工作组问题*2839得到澄清（参见 http://wg21.link/lwg2839）。

