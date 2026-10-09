
另一种选择是将 `typedef` 放在类声明内部。通过将 `typedef` 明确地与另一个类关联，通常可以使其含义更加清晰。当你这样做时，你正在创建所谓的 *成员类型*（member type）。例如，我们可以向 `Pricable` 类添加一个成员类型 **sp**，以便更容易地引用指向 `Pricable` 的共享指针。然后，我们可以使用它来添加一个成员类型 **spVec**，这使得引用指向 `Pricable` 的共享指针的向量变得更加容易。这样，我们就能使用缩写 `Pricable::spVec` 在其他类中引用此类型，如下所示。

```cpp
class Pricable {
public:
    typedef shared_ptr<Pricable> sp;
    typedef vector< sp > spVec;
    // ... more code ...
};

class Portfolio {
private:
    Pricable::spVec securities;
    // ... more code ...
};
```
存在一种替代的表示法，有时是必要的，以帮助编译器确定像 `Pricable::spVec` 这样的项是指向静态成员变量还是成员类型。这种替代表示法仅仅是在前面加上 **typename** 一词。

```cpp
typename Pricable::spVec securities;
```
在处理模板时，包含 **typename** 是一种良好的实践，以确保你的代码可以无歧义地编译。

`SPPricable` 这样的类型命名约定与名为 **sp** 的成员类型约定之间，在实际使用中并没有太大差别。你应该遵循你正在参与的项目的约定。

成员类型在标准模板库中被大量使用。这并不是因为它们提供了便捷的缩写，而是因为它们让你更容易编写模板函数。

假设你想编写一个模板化的 **sumVector** 函数，该函数接受某种类型的数字向量并计算总和。我们希望我们的函数能够累加整数向量、实数向量、复数向量，甚至矩阵向量中的值。

我们的模板函数将有一个模板参数 **V**，它将是某种类型的向量类。我们的函数 **sumVector** 将接受一个类型为 **V** 的向量引用作为其参数。但是它的返回类型是什么？返回类型将取决于 **V** 的类型。对于复数向量，返回类型应该是复数；对于实数向量，它应该是实数。如果我们只知道 V，该如何推导返回类型？

解决方案是，C++ 中的向量具有一个成员类型 *value_type*，其中正好包含我们所需的信息。因此，我们的 sumVector 函数的返回类型应该是 V::*value_type*。由于可能的歧义可能会给编译器带来问题，在使用模板时，我们必须将其完整写为 *typename V::*value_type*。

我们的 sumVector 函数所需的完整代码如下：

```cpp
template <typename V>
typename V::value_type sumVector(const V& vector) {
    typename V::value_type total = 0;
    for (int i = 0; i < (int)vector.size(); i++) {
        total += vector[i];
    }
    return total;
}
```

## 18.2 auto

*auto* 关键字允许你在可以自动推导类型时避免输入类型的完整名称。例如，如果你想要将函数的返回值存储在相同类型的变量中，你可以使用 *auto*。在下图中，编译器可以推断出 *s* 必须是 *double* 类型，因此我们可以使用 *auto*。

```cpp
double d = 4.0;
auto s = sqrt(d);
```
你可以将 *auto* 与 *&* 和 *const* 结合使用，以指示你是想要数据的副本还是引用，以及你是否希望能够修改数据。以下是一些示例：

```cpp
vector<double> vec(10,0.0);
auto& dRef = vec[5];
dRef = -1.0;
ASSERT(vec[5] == -1.0);

auto d = vec[6];
d = -1.0;
ASSERT(vec[6] == 0.0);

const auto& dRef2 = vec[7];
ASSERT(dRef2 == 0.0);
```
在这个例子中，我们利用了向量上 [] 运算符实际上返回指向向量中单元格的引用这一事实。因此，**dRef** 包含一个引用，可用于修改向量。另一方面，**d** 包含向量中数据的副本，因此不能用于修改向量。最后，**dRef2** 是一个引用，但它是 *const* 的，因此只能用于对向量的只读访问。

这些例子显得有些人为凑巧，因为 *auto* 仅仅比输入 **double** 稍微快一点。然而，如下文所示，*auto* 关键字可以节省大量的打字和精神能量。你应该在代码中大量使用它。

## 18.3 使用迭代器处理向量

到目前为止，在这本书中，我们使用 *for* 循环通过增加整数索引 *i* 来遍历向量。

还有另一种遍历向量元素的方法，它对于标准模板库中的所有数据存储类都同样有效。这种方法就是使用 *迭代器*（iterator）。

当你在向量上调用 *begin()* 时，它会返回一个称为迭代器的对象。迭代器是表现得非常像指针的类，你通过诸如 *, ++ 和 == 等运算符来操作它们。下面是一个使用迭代器对向量中所有元素求和的示例。

```cpp
vector<double> v({ 1.0, 2.0, 3.0 });

double sum = 0.0;
vector<double>::iterator i = v.begin();
while (i != v.end()) {
  sum += *i;
  i++;
}

ASSERT(sum == 6.0);
```
这段代码 *看起来* *begin* 返回指向向量第一个元素的指针，而 *end* 返回指向最后一个元素之后位置的指针。我们使用 * 访问迭代器引用的数据，正如我们使用指针时所做的那样。我们使用 ++ 递增迭代器，正如我们处理指针时所做的那样。我们通过将指针与 *end* 比较来决定何时终止循环，就像我们在第 16 章处理指针时所做的那样。唯一的线索表明我们实际上并不是在处理指针，是类型声明 vector<double>::iterator。

使用迭代器的优点在于，它们可以与标准模板库中的所有类一起使用。这意味着你为一个容器编写的代码可以与其他容器一起使用。这使得使用模板编写可以适用于任何容器的通用算法成为可能。

你可以使用向量上的迭代器来修改数据，如下例所示。此函数使用迭代器将向量的每个元素设置为零。

```cpp
void setZero(vector<double>& v) {
 vector<double>::iterator i = v.begin();
 while (i != v.end()) {
 *i=0;
 i++;
 }
}
```
如果你只想查看数据，可以使用 const_iterator 代替，如下例所示。

```cpp
double sumVector( const vector<double>& v ) {
 double sum = 0.0;
 vector<double>::const_iterator i = v.begin();
 while (i != v.end()) {
 sum += *i;
 i++;
 }
 return sum;
}
```
如果你在 const 引用上调用 begin，它将返回一个 const_iterator。因此，在上面的代码中，指定 i 的类型为 const_iterator 是必不可少的，否则代码将无法编译。

迭代器和 const_iterator 之间的区别有点令人困惑，记住它确实非常繁琐。这正是 auto 发挥作用的地方。下面的代码与最后一个示例等效，但它既更容易理解，又更快书写。

```cpp
double sumWithAuto(const vector<double>& v) {
 double sum = 0.0;
 auto i = v.begin();
 while (i != v.end()) {
 sum += *i;
 i++;
 }
 return sum;
}
```

## 18.4 循环和容器

容器只是一个存储数据并遵循标准库约定的类。至少，它应该提供 `begin` 和 `end` 方法，就像 `vector` 那样返回迭代器。

这意味着我们已经编写了一个容器！第 16 章中的类 **Matrix** 具有 `begin` 和 `end` 函数，它们返回指针。指针定义了 `++`、`=` 和 `*` 等操作符，因此它们算作迭代器。

C++ 包含用于遍历容器元素的一种特殊语法。例如，以下代码计算所有 **Matrix** 元素的和。

```cpp
Matrix matrix("1,3;2,4");
double total = 0.0;
for (auto d : matrix) {
    total += d;
}
ASSERT_APPROX_EQUAL(total, 10.0, 0.001);
```
这种 for 循环语法意味着对于矩阵中的每个元素，我们将把该值赋给 `d`，然后执行循环体。这种语法通常比使用迭代器编写循环更方便，尽管最终结果本质上是相同的。

拥有 `begin` 和 `end` 函数只是容器的最低要求。人们应该遵循标准模板库中使用的所有适用于你的容器的约定。

因此，我们在 **Matrix** 类中添加了一些成员类型，它们具有与 `vector` 中对应成员完全相同的名称。

```cpp
typedef double value_type;
typedef double* iterator;
typedef const double* const_iterator;
```
如果我们的容器类遵循相同的命名约定，就可以编写能同样适用于向量和我们的 **Matrix** 类的函数。例如，下面是一个模板函数，可用于计算 `vector` 或 **Matrix** 中元素的和。

```cpp
template <typename C>
typename C::value_type sumContainer(const C& c) {
    typename C::value_type total = 0;
}
