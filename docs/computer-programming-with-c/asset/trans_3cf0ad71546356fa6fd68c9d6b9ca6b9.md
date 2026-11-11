
如果程序员打算对对象执行复杂的数学运算，运算符重载会给他们带来极大的便利。

## 13.5 重载简写运算符：示例

回想第 3 章，`+=`、`-=`、`*=`、`/=` 和 `%=` 在 C++ 中称为简写算术运算符。例如，让我们重载简写运算符 `+=`，以执行用户自定义类型对象的加法。考虑两个基本类型变量，比如 `a` 和 `b`，那么 `a += b` 将执行 `a` 与 `b` 的加法，并将结果存回变量 `a`。这意味着运算符左侧变量的值总是会被覆盖，以便它包含简写运算的结果。我们将编写一个 C++ 程序，展示如何扩展简写运算符的能力，使其能够处理对象。

让我们创建一个类 `Weight`，它有两个整型成员 `kilogram` 和 `gram`。这意味着我们打算以千克和克的形式表示所有重量。让我们使用 `+=` 执行两个 `Weight` 对象 `w1` 和 `w2` 的加法，以理解简写运算符的重载。这意味着现在应该能够对 `Weight` 类的对象编写以下语句：

```cpp
w1 += w2;
```

该语句将执行两个 `Weight` 对象 `w1` 和 `w2` 的加法，并将加法结果存回对象 `w1`。在这种情况下，由于要重载运算符 `+=`，我们将函数 `operator+=` 作为类 `Weight` 的成员函数包含进来，如代码所示。此外，我们知道当运算符与对象一起使用时，编译器会使用运算符左侧的对象调用运算符函数，并将运算符右侧的对象作为参数传递。在编译语句 `w1 += w2` 时，将执行以下步骤。

- **步骤 1：** 将使用对象 `w1` 调用函数 `operator+=`，因为它在语句中位于 `+=` 的左侧。这意味着可以在运算符函数内直接以 `kilogram` 和 `gram` 访问对象 `w1` 的成员，如图 13.10 所示。
- **步骤 2：** 对象 `w2` 将作为参数传递给运算符函数，因为它位于右侧。这意味着 `operator+=` 函数必须设计为接受一个 `Weight` 类型的参数，如图 13.10 所示。这意味着在运算符函数的作用域内，可以通过 `t.kilogram` 和 `t.gram` 访问对象 `w2` 的成员。
- **步骤 3：** 运算符函数不需要返回任何值，因为我们需要将加法结果存储在调用该函数的同一对象中（本例中为 `w1`），并且我们已在步骤 1 中说明，在 `operator+=()` 函数中可以直接访问 `w1` 的成员。

总之，编译器在内部将语句 `w1 += w2` 转换为

```cpp
w1.operator+=(w2);
```

```cpp
void operator+=(Weight t)
{
    kilogram += t.kilogram;
    gram += t.gram;
    while (gram >= 1000)
    {
        gram = gram - 1000;
        kilogram++;
    }
}

void output()
{
    cout << kilogram << " kgs and " << gram << " grams" << endl;
}
};

void main()
{
    // create Weight objects
    Weight w1(50, 800);
    Weight w2(20, 300);

    // execute operation += with objects
    w1 += w2;

    // print the result of addition
    cout << "The result Weight :";
    w1.output();
}
```

### 输出

结果重量为：71 千克和 100 克

以下 `operator+=()` 中的两条语句将把 `w1` 的成员 `kilogram` 和 `gram` 与 `w2` 的成员 `t.kilogram` 和 `t.gram` 相加，并将结果存回 `w1`。

```cpp
kilogram += t.kilogram;
gram += t.gram;
```

执行这些语句后，`w1.kilogram` 的值被设置为 50 + 20 = 70 千克，`w1.gram` 被设置为 800 + 300 = 1100 克，如图 13.11 所示。

对象 `w1` 的千克值和克值必须重新格式化，因为克值似乎已经超过 1000，这可以很容易地换算并用千克表示。因此，与其说成 70 千克

![](img/57c0d966bb33c67a5a188e6bf39e4e02_730_0.png)

表达式

```cpp
w1 > w2
```

将使用对象 `w1` 调用 `operator>()` 函数，并将 `w2` 作为参数传递。这是因为 `w1` 出现在运算符左侧，而 `w2` 出现在右侧。

我们知道比较结果始终必须是布尔值（即 0 或 1）。因此，每个运算符函数的返回类型都设置为 `int`。如果两个对象之间的关系为真，运算符函数返回 1，否则返回 0。由于 `Weight` 是我们自己的类，我们可以定义自己的规则来比较其对象。在这里，每个 `Weight` 对象都以千克和克表示；因此，要比较两个 `Weight` 对象 `w1` 和 `w2`，必须先将它们转换为同一单位。运算符函数将两个重量完全转换为克，然后相互比较转换后的值。设 `g1` 和 `g2` 分别为重量 `w1` 和 `w2` 完全转换后的克值；那么 `g1` 和 `g2` 可计算如下

```cpp
g1 = w1.kilogram * 1000 + w1.gram;
g2 = w2.kilogram * 1000 + w2.gram;
```

如果 `g1 > g2`，则意味着重量对象 `w1` 大于 `w2`。因此，如果 `g1 > g2`，`operator>()` 函数返回 1，否则返回 0。

`main()` 函数并不关心运算符函数内部如何进行比较。`main()` 函数只包含一个 `if` 块，如下所示比较两个重量 `w1` 和 `w2`：

```cpp
if (w1 > w2)
{
    cout << "Condition w1>w2 is TRUE" << endl;
}
else
{
    cout << "Condition w1>w2 is FALSE" << endl;
}
```

为了计算条件 `w1 > w2`，将调用 `operator>()` 函数，如图 13.13 所示；该函数分别计算重量 `w1` 和 `w2` 的克值 `g1` 和 `g2`。注意，`w1` 的成员可以在运算符函数内直接访问，因为它是调用该函数的对象。`w2` 的成员通过 `t.kilogram` 和 `t.gram` 访问，因为 `w2` 作为参数传递并初始化给 `t`。对象 `w1` 和 `w2` 通过调用带两个参数的构造函数创建，如下：

```cpp
Weight w1(50, 800);
Weight w2(20, 300);
```

因此，

```cpp
w1 = 50 kilogram and 800 grams
w2 = 20 kilogram and 300 grams
```

![](img/57c0d966bb33c67a5a188e6bf39e4e02_733_0.png)

因此，运算符函数计算出 **g1 = 50,800** 和 **g2 = 20,300**。由于 `g1 > g2`，运算符函数返回 1，表示重量 `w1` 实际上大于重量 `w2`。运算符函数执行完毕后，控制权返回 `main()`，并且由于运算符函数返回了 1，条件 `w1 > w2` 被判定为真。这会将控制权转入 `if` 块，从而在计算机屏幕上打印以下消息：

```text
Condition w1>w2 is TRUE
```

注意，变量 `g1` 和 `g2` 的数据类型是 `long`，以支持超出整数范围的值。

以下是重载 `>` 和 `<=` 以比较 `Weight` 对象的完整源代码：

```cpp
#include<iostream.h>
class Weight
{
private:
    int kilogram;
    int gram;
public:
    Weight()
    {
        kilogram = 0;
        gram = 0;
    }

    Weight(int p, int q)
    {
        kilogram = p;
        gram = q;
    }

    int operator>(Weight t)
    {
        long g1 = kilogram * 1000 + gram;
        long g2 = t.kilogram * 1000 + t.gram;
        if (g1 > g2)
        {
            return 1;
        }
        else
        {
            return 0;
        }
    }

    int operator<=(Weight t)
    {
        long g1 = kilogram * 1000 + gram;
        long g2 = t.kilogram * 1000 + t.gram;
        if (g1 <= g2)
        {
            return 1;
        }
        else
        {
            return 0;
        }
    }

    void output()
    {
        cout << kilogram << " kgs and " << gram << " grams" << endl;
    }
};

void main()
{
    // create Weight objects
    Weight w1(50, 800);
    Weight w2(20, 300);
    Weight w3(110, 100);
    Weight w4(25, 450);

    if (w1 > w2)
    {
        cout << "Condition w1>w2 is TRUE" << endl;
    }
    else
    {
        cout << "Condition w1>w2 is FALSE" << endl;
    }

    if (w3 <= w4)
    {
        cout << "Condition w3<=w4 is TRUE" << endl;
    }
    else
    {
        cout << "Condition w3<=w4 is FALSE" << endl;
    }
}
```

### 输出

```text
Condition w1>w2 is TRUE
Condition w3<=w4 is FALSE
```

类似地，下一个 `if` 块使用 `<=` 运算符比较两个对象 `w3` 和 `w4`。因此，编译器将使用对象 `w3` 调用函数 `operator<=`，并将 `w4` 作为参数传递。在这种情况下，由于条件 `w3 <= w4` 为假，`operator<=` 函数将返回 0。因此，这次执行控制将转入 `else` 块，从而在计算机屏幕上打印以下消息：

```text
Condition w3<=w4 is FALSE
```

## 13.7 重载自增/自减运算符：示例

现在让我们重载自增运算符（`++`），以便将其用于类的对象。重载自减运算符（`--`）也可以采用相同的方法。回想第 3 章，C++ 中的自增/自减运算符有两种形式：前缀形式和后缀形式。当自增/自减运算符以前缀形式（`++variableName`）使用时，变量的值先更新，然后在表达式中使用新值；而在后缀形式（`variableName++`）中，先使用变量的当前值参与表达式，随后再更新变量以反映新值。本节将学习如何以前缀形式和后缀形式重载自增运算符（`++`）。
