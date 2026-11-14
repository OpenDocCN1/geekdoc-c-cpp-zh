
此声明在函数和命名空间中有效，但在类中无效（在那里它会与其他 `using` 声明冲突）。术语“名称隐藏”应按字面意思理解，如以下示例所示：

单击此处查看代码图像

```
void f(string s) { ... } // # 1
namespace inner {
    void f(int i) { ... } // # 2
    f("from global"); // Error: #2 hides #1
}
```

如果在内部作用域中声明或定义一个函数，它不仅会隐藏具有相同签名的函数重载，还会隐藏外部作用域中的所有重载。实际上，任何名为 f 的实体（类、变量……）都会隐藏全局函数 f。要使其可用于函数调用，我们可以通过 `using` 声明使其可见：

单击此处查看代码图像

```
void f(string s) { ... } // # 1
namespace inner {
    void f(int i) { ... } // # 2
    using ::f;
    f("from global"); // now calls #1
}
```

在头文件中将名称导入命名空间会显著增加名称冲突的风险，因为该名称在编译单元的所有后续文件中都保持可见。函数内（即使在头文件中）的 `using` 不那么关键，因为导入的名称仅在函数结束前可见。同样，我们可以使用 `using` 指令导入整个命名空间：

```
void fun ( ... )
{
    using namespace c1::c2;
    cc x;
    ...
    cc y;
}
```

与之前一样，这可以在函数或另一个命名空间中完成，但不能在类作用域中完成。语句：

```
using namespace std;
```

通常是 `main` 函数中的第一条语句，甚至是在包含之后的第一条语句。在全局命名空间中导入 `std` 有很大的名称冲突潜力，例如，当我们也定义一个名为 `vector` 的类（在全局命名空间中）时。

## 建议

不要在头文件中导入名称或命名空间（函数外）。

当命名空间的名称太长时，尤其是嵌套命名空间，我们可以使用命名空间别名为其重命名：

![](img/5682e787fc967e93d7e33e8bac5f58a0_234_0.png)

```
namespace lname= long_namespace_name;
namespace dvector= algebra::vector::dense;
```

与之前一样，这应在适当的作用域中完成。

![](img/5682e787fc967e93d7e33e8bac5f58a0_234_1.png)

## C++17

使用相同的冒号分隔表示法，我们可以在 C++17 中打开一个嵌套命名空间：

![](img/5682e787fc967e93d7e33e8bac5f58a0_234_2.png)

```
namespace algebra::vector::dense {
    class vector3 { /* */ };
}
```

而不是编写单个命名空间的嵌套声明。

## 3.2.2 参数相关查找

参数相关查找（Argument-Dependent Lookup，简称 ADL）将函数名称的搜索扩展到其参数的命名空间中——但不包括它们各自的父命名空间。这使我们免除了函数的冗长命名空间限定。假设我们在谦逊的命名空间 `rocketscience` 中编写终极科学库：

![](img/5682e787fc967e93d7e33e8bac5f58a0_234_3.png)

```
namespace rocketscience {
struct matrix {};

template <typename LinOp>
void initialize(LinOp& A) { /* ... */ }

matrix operator+(const matrix& A, const matrix& B)
{
    matrix C;
    initialize(C); // not qualified, same namespace
    add(A, B, C);
    return C;
}
}
```

每次我们使用函数 `initialize`（该函数据称仅在 `rocketscience` 中定义），都可以省略命名空间 `rocketscience` 中所有类的限定：

单击此处查看代码图像

```
int main ()
{
    rocketscience::matrix A, B, C, D;
    rocketscience::initialize(B); // qualified
    initialize(C); // rely on ADL

    chez_herbert::matrix E, F, G; // qualification needed
    rocketscience::initialize(E); // qualification needed
    initialize(F); // Error: initialize not found
}
```

运算符也受 ADL 约束：

```
A = B + C + D;
```

想象没有 ADL 的前面表达式：

单击此处查看代码图像

```
A = rocketscience::operator+(rocketscience::operator+(B, C),
D);
```

同样丑陋且更加繁琐的是流式 I/O，当必须限定命名空间时。由于用户代码不应位于命名空间 std 中，因此类的 operator<< 最好定义在该类的命名空间中。这允许 ADL 为每种类型找到正确的重载，例如：

```
std::cout << A << E << B << F << std::endl;
```

没有 ADL，我们需要以冗长的表示法限定每个运算符的命名空间。这将把前面的表达式变为：

单击此处查看代码图像

```
std::operator<< (chez_herbert::operator<< (
rocketscience::operator<< (chez_herbert::operator<< (
rocketscience::operator<< (std::cout, A), E), B),
F), std::endl);
```

ADL 机制也可用于在类分布于多个命名空间时选择正确的函数模板重载。线性代数中的 L₁ 范数（也称为曼哈顿范数）既定义于矩阵也定义于向量，我们希望为两者提供模板实现：

单击此处查看代码图像

```
template <typename Matrix>
double one_norm(const Matrix& A) { ... }

template <typename Vector>
double one_norm(const Vector& x) { ... }
```

编译器如何知道我们为每种类型偏好哪个重载？一种可能的解决方案是为矩阵和向量分别引入一个命名空间，以便由 ADL 选择正确的重载：

单击此处查看代码图像

```
namespace rocketscience {
 namespace mat {
 struct sparse_matrix {};
 struct dense_matrix {};
 struct über_matrix⁶ {};

 template <typename Matrix>
 double one_norm(const Matrix& A) { ... }
 }
 namespace vec {
 struct sparse_vector {};
 struct dense_vector {};
 struct über_vector {};
 template <typename Vector>
 double one_norm(const Vector& x) { ... }
 }
}
```

ADL 机制仅在参数类型声明的命名空间中搜索函数，而不在它们各自的父命名空间中搜索：

单击此处查看代码图像

```
namespace rocketscience {
...
namespace vec {
struct sparse_vector {};
struct dense_vector {};
struct über_vector {};
}
template <typename Vector>
double one_norm(const Vector& x) { ... }
}
int main ()
{
rocketscience::vec::über_vector x;
double norm_x = one_norm(x); // Error: not found by
ADL
}
```

- 6. 当然，我们使用 über 的原始德语拼写——有时甚至出现在美国论文中。请注意，某些编译器（例如 g++-9）对非 ASCII 字符存在问题。

同样，当我们将名称导入另一个命名空间时，该命名空间中的函数也不会被 ADL 考虑：

单击此处查看代码图像

```
namespace rocketscience {
...
using vec::über_vector;
template <typename Vector>
double one_norm(const Vector& x) { ... }
}
int main ()
{
    rocketscience::über_vector x;
    double norm_x = one_norm(x);   // Error: not found by
ADL
}
```

仅依赖 ADL 来选择正确的重载有其局限性。当我们使用第三方库时，可能会发现我们在自己的命名空间中也实现了相同的函数和运算符。这种歧义可以通过仅使用 `using` 导入单个函数而不是整个命名空间来减少（但不能完全避免）。

多参数函数的歧义概率会进一步增加，尤其是当参数类型来自不同的命名空间时，例如：

单击此处查看代码图像

```
namespace rocketscience {
    namespace mat {
        ...
        template <typename Scalar, typename Matrix>
        Matrix operator*(const Scalar& a, const Matrix& A) {
            ...
        }
    }
    namespace vec {
        ...
        template <typename Scalar, typename Vector>
        Vector operator*(const Scalar& a, const Vector& x) {
            ...
        }
        ...
        template <typename Matrix, typename Vector>
        Vector operator*(const Matrix& A, const Vector& x) {
            ...
        }
    }
}
int main(int argc, char* argv[])
{
    rocketscience::mat::über_matrix A;
    rocketscience::vec::über_vector x, y;
    y = A * x;   // which overload is
selected?
}
```

这里的意图很明确。嗯，对于人类读者来说是这样。对于编译器来说则不那么明确。`A` 的类型定义在 `rocketscience::mat` 中，而 `x` 的类型定义在
