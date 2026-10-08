

```cpp
template<typename In, typename T>
// requires Input_iterator<In>() && Number<T>()
T accumulate(In first, In last, T init)
{
  while (first!=last) {
    init = init + *first;
    ++first;
  }
  return init;
}
```

给定一个初始值 **init**，它仅仅将 [**first**: **last**) 序列中的每个值相加并返回总和。用于计算总和的变量 **init** 通常被称为*累加器*。例如：

```cpp
int a[] = { 1, 2, 3, 4, 5 };
cout << accumulate(a, a+sizeof(a)/sizeof(int), 0);
```

这将打印 **15**，即 $0+1+2+3+4+5$（其中**0**是初始值）。显然，**accumulate()** 可用于各种类型的序列：

```cpp
void f(vector<double>& vd, int* p, int n)
{
  double sum = accumulate(vd.begin(), vd.end(), 0.0);
  int sum2 = accumulate(p, p+n, 0);
}
```

结果（即总和）的类型是 **accumulate()** 用于持有累加器的变量的类型。这种灵活性在某些情况下非常重要。例如：

```cpp
void g(int* p, int n)
{
  int s1 = accumulate(p, p+n, 0);        // 累加到 int 中
  long sl = accumulate(p, p+n, long(0)); // 将 int 累加到 long 中
  double s2 = accumulate(p, p+n, 0.0);   // 将 int 累加到 double 中
}
```

在某些计算机上，**long** 的有效位数比 **int** 多。**double** 可以表示比 **int** 更大（或更小）的数值，但精度可能会降低。我们将在第 24 章重新审视数值计算中范围和精度的作用。

将希望得到结果的变量用作初始化器，是指定累加器类型的一种常用惯用写法：

```cpp
void f(vector<double>& vd, int* p, int n)
{
    double s1 = 0;
    s1 = accumulate(vd.begin(), vd.end(), s1);
    int s2 = accumulate(vd.begin(), vd.end(), s2);    // 糟糕
    float s3 = 0;
    accumulate(vd.begin(), vd.end(), s3);              // 糟糕
}
```

请记住初始化累加器，并将 `accumulate()` 的结果赋值给该变量。在这个例子中，`s2` 在未自身初始化之前就被用作初始化器；因此结果是未定义的。我们将 `s3` 传给了 `accumulate()`（按值传递；参见 §8.5.3），但结果从未被赋值到任何地方；该编译仅仅是浪费时间的行为。

### 21.5.2 泛化 accumulate()

因此，基本的三参数 `accumulate()` 执行加法运算。然而，还有许多其他有用的操作，例如乘法和减法，我们可能希望对序列执行这些操作，因此 STL 提供了第二个四参数版本的 `accumulate()`，在其中我们可以指定要使用的操作：

```cpp
template<typename In, typename T, typename BinOp>
// requires Input_iterator<In> && Number<T>
//     & Binary_operator<BinOp,Value_type<In>,T>
T accumulate(In first, In last, T init, BinOp op)
{
    while (first!=last) {
        init = op(init, *first);
        ++first;
    }
    return init;
}
```

任何接受两个累加器类型参数的二元操作都可以在这里使用。例如：

```cpp
vector<double> a = { 1.1, 2.2, 3.3, 4.4 };
cout << accumulate(a.begin(),a.end(), 1.0, multiplies<double>());
```

这将打印 **35.1384**，即 `1.0*1*2.2*3.3*4.4`（其中**1.0**是初始值）。这里提供的二元运算符 `multiplies<double>` 是一个执行乘法运算的标准库函数对象；`multiplies<double>` 对**双精度浮点数**进行乘法，`multiplies<int>` 对**整数**进行乘法，等等。还有其他二元函数对象：`plus`（执行加法）、`minus`（执行减法）、`divides`（执行除法）和 `modulus`（取模运算）。它们都定义在 `<functional>` 中（§B.6.2）。

请注意，对于浮点数的乘积，明显的初始值是 **1.0**。

与 `sort()` 示例（§21.4.2）一样，我们通常感兴趣的不仅仅是简单的内置类型，而是类对象中的数据。例如，如果我们已知单价和数量，我们可能想要计算项目的总成本：

```cpp
struct Record {
    double unit_price;
    int units;      // 销售数量
    // ...
};
```

我们可以让 `accumulate` 的运算符从 `Record` 元素中提取 `units`，并将其与累加器值相乘：

```cpp
double price(double v, const Record& r)
{
    return v + r.unit_price * r.units;    // 计算价格并累加
}

void f(const vector<Record>& vr)
{
    double total = accumulate(vr.begin(), vr.end(), 0.0, price);
    // ...
}
```

我们“偷懒”使用了函数而不是函数对象来计算价格——只是为了展示我们也可以这样做。我们通常更倾向于使用函数对象：
- 如果它们需要在调用之间存储值，或者
- 如果它们足够短，以至于内联可能会带来差异（最多只是少数几个基本操作）

在这个例子中，我们可能出于第二个原因选择函数对象。

# **试一试**

定义一个 **vector<Record>**，用你选择的四条记录对其进行初始化，并使用上述函数计算它们的总价格。

### 21.5.3 内积

取两个向量，将具有相同下标的每对元素相乘，然后将所有这些乘积相加。这就是这两个向量的*内积*，在许多领域（例如物理和线性代数；参见 §24.6）中都是一个非常实用的操作。如果你更喜欢代码而非文字，以下是 STL 版本：

```cpp
template<typename In, typename In2, typename T>
    // requires Input_iterator<In> && Input_iterator<In2>
    //      && Number<T> (§19.3.3)
T inner_product(In first, In last, In2 first2, T init)
    // 注意：这是我们将两个向量相乘（产生标量）的方式
{
    while(first!=last) {
        init = init + (*first) * (*first2);    // 将成对的元素相乘
        ++first;
        ++first2;
    }
    return init;
}
```

这将内积的概念推广到任何类型的序列和任何类型的元素。作为一个例子，考虑一下股票市场指数。其工作原理是选取一组公司，并为每家分配一个“权重”。例如，在我们最后一次查看道琼斯工业平均指数时，Alcoa 的权重为 2.4808。为了获取指数的当前值，我们将每家公司的股价与其权重相乘，并将所有得到的加权价格相加。显然，这就是价格与权重的内积。例如：

```cpp
    // 计算道琼斯工业平均指数：
    vector<double> dow_price = {        // 每家公司的股价
        81.86, 34.69, 54.45,
        // . . .
    };

    list<double> dow_weight = {          // 每家公司的指数权重
        5.8549, 2.4808, 3.8940,
        // ...
    };

    double dji_index = inner_product(    // 将（权重，价值）对相乘并求和
                  dow_price.begin(), dow_price.end(),
                  dow_weight.begin(),
                  0.0);

    cout << "DJI value " << dji_index << '\n';
```

请注意，`inner_product()` 接受两个序列。然而，它只接受三个参数：只提到了第二个序列的开始位置。第二个序列必须至少拥有与第一个序列相同数量的元素。如果没有，就会发生运行时错误。就 `inner_product()` 而言，第二个序列拥有的元素多于第一个序列是可以的；那些“多余的元素”将 simply 不会被使用。

这两个序列不需要是同一类型，也不需要具有相同的元素类型。为了说明这一点，我们使用了一个 **vector** 来保存价格，使用了一个 **list** 来保存权重。

### 21.5.4 泛化 `inner_product()`

`inner_product()` 可以像 `accumulate()` 那样进行泛化。不过，对于 `inner_product()`，我们需要两个额外的参数：一个用于将累加器与新值结合，完全类似于 `accumulate()`；另一个用于结合元素值对：

```cpp
template<typename In, typename In2, typename T, typename BinOp,
          typename BinOp2>
  //    requires Input_iterator<In> && Input_iterator<In2> && Number<T>
  //        && Binary_operation<BinOp,T, Value_type<In>>
  //        && Binary_operation<BinOp2,T, Value_type<In2>>
  T inner_product(In first1, In last, In2 first2, T init, BinOp op, BinOp2 op2)
  {
      while(first1!=last) {
          init = op(init, op2(*first1, *first2));
          ++first1;
          ++first2;
      }
      return init;
  }
```

