

```cpp
template<typename T>
struct EqualityComparable : HasEqual<T, T>
{
    EqualityComparable()
    {
        auto p = constraints;
    }

    static void constraints(T x, T y)
    {
        Convertible<decltype(x == y), bool>{};
        Convertible<decltype(x != y), bool>{};
    }
};
```

通过继承 *HasEqual*，借助初始化顺序，约束会在 *EqualityComparable* 约束类中的约束之前被检查。*EqualityComparable* 类在其内部应用了额外的约束。

这里，*Convertible* 约束被写成对临时对象的显式初始化。这会检查一个表达式的结果（*decltype* 运算符返回表达式的类型）能否转换为指定类型，此处为 *bool*。

对 != 也有类似的要求。*Convertible* 定义为：

```cpp
template<typename T, typename U>
struct Convertible
{
    Convertible()
    {
        static_assert(std::is_convertible<T, U>::
            value, "Not convertible");
    }
};
```

该约束通过对 *std::is_convertible* 类型特征进行静态断言来实现。*type trait*（类型特征）是一个类模板，用于评估其类型参数的某些属性。嵌套的 *value* 包含评估的结果。这里不需要约束函数，因为无需引入对象即可评估该特征。

## 问题 217 类型特征

提供一个类型特征 *is_same* 的类模板实现，使得仅当 X 和 Y 表示相同类型时，*is_same<X, Y>::value* 才为 true。结果值应是一个常量表达式，可由编译器在 *static_assert* 等上下文中求值。

### 问题 217 的解答

```cpp
template<typename T, typename U>
struct is_same
{
    static constexpr bool value = false;
};

template<typename T>
struct is_same<T, T>
{
    static constexpr bool value = true;
};
```

主模板（第一个声明）定义了 X 和 Y 为不同类型时的结果。特化版本定义了模板参数相同时的结果。

## 问题 218 advance 和 next

为输入迭代器和前向迭代器提供 STL 算法 advance 的实现，然后使用 advance 算法实现一个迭代器工具 next。

### 问题 218 的解答

```cpp
template<typename Iter>
void advance(Iter& first, int n)
{
    while(n > 0)
    {
        ++first;
        --n;
    }
}

template<typename Iter>
Iter next(Iter i, int n = 1)
{
    advance(i, n);
    return i;
}
```

## 问题 219 自定义 iota

定制化 STL 算法 iota 的递增/递减部分。

### 问题 219 的解答

为自定义步长重载 iota：

```cpp
template <typename ForwardIterator, typename T>
void iota(ForwardIterator first, ForwardIterator last,
          T value, T step = 1)
{
    for (; first != last; ++first, value += step)
        *first = value;
}

// 用法：
std::vector<int> vint(5);
std::vector<int> v_expected = {5, 10, 15, 20, 25};
iota(vint.begin(), vint.end(), // 目标范围
     5, // 起始值
     5); // 每次递增 5

assert(std::equal(vint.begin(), vint.end(),
                  v_expected.begin()));
```

以额外参数的形式为 iota 重载步长，需要修改实现以及既有的接口，这在某些情况下可能并不可行。另一方面，我们可以通过重载前置递增运算符轻松实现同样的输出，如下所示：

```cpp
template <typename InitialValue, typename StepSize>
struct step_helper
{
    step_helper(InitialValue val, StepSize step)
        : _val(val), _step(step) {}

    step_helper& operator++()
    {
        _val += _step; return *this;
    }

    operator InitialValue() { return _val; }
private:
    InitialValue _val;
    const StepSize _step;
};

template<typename InitialValue, typename StepSize =
    InitialValue>
step_helper<InitialValue, StepSize>
step(InitialValue val, StepSize s = 1)
{
    return step_helper<InitialValue, StepSize>(val,
        s);
}
// 用法：自定义递增为 10
std::array<int, 5> arr;
std::array<int, 5> arr_res = {5, 15, 25, 35, 45};
std::iota(arr.begin(), arr.end(), step(5, 10));
assert(std::equal(arr.begin(), arr.end(), arr_res.
    begin()));
```

## 问题 220 all_of 算法

使用 *find_if_not* 和 *find_if* 实现 STL 算法 *all_of*。

### 问题 220 的解答

```cpp
template<typename InputIterator, typename Predicate>
inline bool
all_of(InputIterator first, InputIterator last,
       Predicate pred)
{
    return last == std::find_if_not(first, last,
        pred);
}

template<typename InputIterator, typename Predicate>
inline bool
all_of(InputIterator first, InputIterator last,
       Predicate pred)
{
    return last == std::find_if(first, last, std::not1(pred));
}
```

## 问题 221 is_partitioned 算法

使用以下接口实现 STL 算法 *is_partitioned*

```cpp
template<typename InputIterator, typename Predicate>
bool is_partitioned(InputIterator first,
        InputIterator last, Predicate p);
```

它返回 true，如果：

- [first, last) 被一元谓词 p 划分，即所有满足 p 的元素都出现在不满足 p 的元素之前。或者，
- [first, last) 为空。

换句话说，序列中所有满足谓词的元素都位于序列的开头。

### 问题 221 的解答

该算法包含两个阶段：

1. 找到第一个不满足谓词的元素。算法 `std::find_if_not` 在这里非常合适。
2. 从上述找到的元素开始，不应有任何元素满足该谓词。`std::none_of` 可以轻松完成这项工作。

```cpp
template<typename InputIterator, typename Predicate>
bool is_partitioned(InputIterator first,
                    InputIterator last,
                    Predicate p)
{
    first = std::find_if_not(first, last, p);
    return std::none_of(first, last, p);
}
```

或者

```cpp
template<typename InputIterator, typename Predicate>
bool is_partitioned(InputIterator first,
                    InputIterator last,
                    Predicate p)
{
    while(first != last && p(*first))
        ++first;
    while(first != last && !p(*first))
        ++first;
    return (first == last);
}
```

## 索引

- 2D 数组旋转，126
- 邮局中的一个排队问题，129
- 访问默认模板实参，474, 475
- 访问虚函数，476
- ADL（实参依赖查找），336–339
- advance 和 next，500
- 别名模板，496
- 对齐，361
- 对齐说明符，441
- all_of 算法，502
- 替代欧几里得算法，278
- 祖先，184
- 近似计算一个数的平方根，4
- 数组与 sizeof，450
- 数组与 typedef，449, 450
- 属性，395
- auto 作为尾置返回类型，445
- auto 类型说明符，380, 416, 417
- auto 类型说明符与模板实参推导，417, 418
- using 声明的可用性，431
- 基类初始化器，483
- 基本查找，339–341
- constexpr 基础，398, 400
- 位域与并发，314
- 花括号初始化器列表与赋值，386, 387
- 花括号初始化器列表作为下标，368
- Bulterman 重排问题，151
- carries_dependency 属性，444
- 循环数组，158
- 类作用域变量，327, 328
- 类，464
- 逗号运算符与实参，387
- 编译器生成的成员函数，321, 322
- 完全二叉树，195
- 计算 a，274
- 计算函数，288
- 计算 GCD，276
- 仅使用加法和减法计算平方，280
- 计算子数组之和，176
- 计算乘积 a × b，275
- 计算商和余数，275
- 计算约束 GCD，277
- const/volatile 构造函数，477
- const/volatile 限定符，412, 413
- 常数时间范围查询，79
- constexpr，398
- constexpr 与构造函数，409
- constexpr 与字面类型，408
- constexpr 构造函数，387, 388, 402
- constexpr 函数，400, 401

