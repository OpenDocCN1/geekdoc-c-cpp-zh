
```cpp
}
}
return *this;
}
```

## R13.9 What is the error in the assignment operator for this class?

```cpp
class String
{
public:
    String(const char s[]);
    String& operator=(const String& other);
private:
    char* buffer;
    int len;
};
```

```cpp
String::String(const char s[])
{
    len = strlen(s);
    buffer = new char[len];
    for (int i = 0; i < len; i++)
    {
        buffer[i] = s[i];
    }
}
```

```cpp
String& String::operator=(const String& other)
{
    if (this != &other)
    {
        delete[] buffer;
        len = other.len;
        char* buffer = new char[len];
        for (int i = 0; i < len; i++)
        {
            buffer[i] = other[i];
        }
    }
    return *this;
}
```

## R13.10 What output will be printed by the following program?

```cpp
class Base
{
public:
    Base();
    ~Base();
};

Base::Base()
{
    cout << "Constructing Base" << endl;
}

Base::~Base()
{
    cout << "Destroying Base" << endl;
}
```

```cpp
void set(Employee* t)
```

to set it, and

```cpp
Employee* get() const
```

to get it. As an internal representation, use a Boolean data member and a data member of type `Employee*`. Provide the necessary memory management functions to ensure that the data member is recovered when the enclosing object (for example, the instance of `Department`) is deleted.

- **E13.16** In Exercise E13.16, implement an `Optional` class template so that the secretary can be defined as `Optional<Employee>`.

- **E13.17** In Exercise E13.16, implement an `Optional` class template so that the secretary can be defined as `Optional<Employee>`.

- **E13.18** Add a swap member function to the `Pair` class of Section 13.3.2 that swaps the first and second elements.

- **E13.19** Add a sort member function to the `Pair` class of Section 13.3.2 that sorts the two elements.

- **E13.20** Turn the minmax function in Section 13.3.2 into a template.

- **E13.21** Rewrite the selection sort algorithm described in Section 12.1 as a template function, using the less than operator to compare two elements.

- **E13.22** Rewrite the merge sort algorithm described in Section 12.4 as a template function.

- **E13.23** Rewrite the binary search algorithm described in Section 12.6.2 as a template function.

## PROGRAMMING PROJECTS

- **P13.1** Define a class Money with two integer data members, dollars and cents. Overload arithmetic operators, comparison operators, and input and output operators for your class. Should you overload the `*` and `/` operators? What argument types should they accept? Overload the `%` operator so that if `n` is a floating-point value, `n % m` yields `n` percent of the money amount `m`.

- **P13.2** Define a class Complex for complex numbers. Provide implementations for addition, subtraction, multiplication, and the stream input and output operators. Implement the compound assignment operators, such as `+=`, for each of the supported binary arithmetic operations.

- **P13.3** Define a class BigInteger that stores arbitrarily large integers by keeping their digits in a vector<int>. Supply a constructor `BigInteger(string)` that reads a sequence of digits from a string. Overload the `+`, `-`, and `*` operators to add, subtract, and multiply the digit sequences. Overload the `<<` operator to send the big integer to a stream. For example,

    ```cpp
    BigInteger a("123456789");
    BigInteger b("987654321");
    cout << a * b;
    ```

    prints 121932631112635269.

- **P13.4** Implement a class for polynomials. Store the coefficients in a vector of floating-point values. Then provide operators for addition, subtraction, multiplication, and output.

### 3.1 贝叶斯决策论

贝叶斯决策论是概率框架下实施决策的基本方法。对分类任务来说，在所有相关概率都已知的理想情形下，贝叶斯决策论考虑如何基于这些概率和误判损失来选择最优的类别标记。下面我们以多分类任务为例来解释其基本原理。

假设有 $N$ 种可能的类别标记，即 $\mathcal{Y}=\{c_1, c_2, \ldots, c_N\}$，$\lambda_{ij}$ 是将一个真实标记为 $c_j$ 的样本误分类为 $c_i$ 所产生的损失。基于后验概率 $P(c_i \mid \boldsymbol{x})$ 可获得将样本 $\boldsymbol{x}$ 分类为 $c_i$ 所产生的期望损失，即在样本 $\boldsymbol{x}$ 上的“条件风险”

$$R(c_i \mid \boldsymbol{x}) = \sum_{j=1}^{N} \lambda_{ij} P(c_j \mid \boldsymbol{x})$$

我们的任务是寻找一个判定准则 $h: \mathcal{X} \rightarrow \mathcal{Y}$ 以最小化总体风险

$$R(h) = \mathbb{E}_{\boldsymbol{x}}[R(h(\boldsymbol{x}) \mid \boldsymbol{x})]$$

显然，对每个样本 $\boldsymbol{x}$，若 $h$ 能最小化条件风险 $R(c \mid \boldsymbol{x})$，则总体风险 $R(h)$ 也将被最小化。这就产生了贝叶斯判定准则

$$h^{*}(\boldsymbol{x}) = \arg\min_{c \in \mathcal{Y}} R(c \mid \boldsymbol{x})$$

此时，$h^{*}$ 称为贝叶斯最优分类器，与之对应的总体风险 $R(h^{*})$ 称为贝叶斯风险。$R(h^{*})$ 反映了分类器所能达到的最好性能，即通过机器学习所能产生的模型精度的理论上限。

```cpp
}

Fraction::Fraction(int n)
{
    numerator = n;
    denominator = 1;
}

Fraction::Fraction(int n, int d)
{
    int g = gcd(n, d); // The greatest common divisor
    if (g == 0)
    {
        numerator = 0;
        denominator = 1;
    }
    else if (d > 0)
    {
        numerator = n / g;
        denominator = d / g;
    }
    else
    {
        numerator = -n / g;
        denominator = -d / g;
    }
}

Fraction Fraction::operator+(Fraction other) const
{
    return Fraction(numerator * other.denominator
        + denominator * other.numerator,
        denominator * other.denominator);
}

Fraction Fraction::operator*(Fraction other) const
{
    return Fraction(numerator * other.numerator,
        denominator * other.denominator);
}

Fraction operator*(int n, Fraction f)
{
    return f * n;
}

Fraction operator-(Fraction f)
{
    return f * -1;
}

Fraction operator-(Fraction f, Fraction g)
{
    return f + g * -1;
}

Fraction Fraction::inverse() const
{
    return Fraction(denominator, numerator);
}
```

```cpp
}
else
{
    buffer = nullptr;
}
}

String& String::operator=(const String& other)
{
    cout << "Assigning \"" << other << "\" to \""
    << *this << "\"" << endl;
    if (this != &other)
    {
        delete[] buffer;
        len = other.len;
        if (len > 0)
        {
            buffer = new char[len];
            for (int i = 0; i < len; i++)
            {
                buffer[i] = other.buffer[i];
            }
        }
        else
        {
            buffer = nullptr;
        }
    }
    return *this;
}

String::~String()
{
    cout << "Destroying \"" << *this << "\"" << endl;
    delete[] buffer;
}

int String::length() const
{
    return len;
}

String String::substr(int start, int length) const
{
    String result;
    if (length > 0)
    {
        result.len = length;
        result.buffer = new char[length];
        for (int i = 0; i < length; i++)
        {
            result.buffer[i] = buffer[start + i];
        }
    }
    return result;
}

String String::operator+(const String& other) const
{
```

## CHAPTER 14
## LINKED LISTS, STACKS, AND QUEUES

![](img/d61019b035dd82beb581604273c0ee6b_720_0.png)

© andrea laurita/iStockphoto.

## CHAPTER GOALS

- To become familiar with the list, stack, and queue data types
- To understand the implementation of linked lists
- To understand the efficiency of vector and list operations
- To study applications of stacks and queues

## CHAPTER CONTENTS

- **14.1 USING LINKED LISTS** 454
- **14.2 IMPLEMENTING LINKED LISTS** 459
  - WE1 Implementing a Linked List Template 472
- **14.3 THE EFFICIENCY OF LIST, ARRAY, AND VECTOR OPERATIONS** 472
- **14.4 STACKS AND QUEUES** 476
- **14.5 IMPLEMENTING STACKS AND QUEUES** 479
- **14.6 STACK AND QUEUE APPLICATIONS** 484
  - ST1 Reverse Polish Notation 492
