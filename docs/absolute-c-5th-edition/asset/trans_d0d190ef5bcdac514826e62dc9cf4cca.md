

# 第 8 章 运算符重载、友元与引用

## 显示 8.2 作为成员重载运算符（22 部分中的第 2 部分）

```cpp
private:
    int dollars; // 负数金额用负数表示
    //dollars 和
    int cents; // 负分。负 $4.50 表示为
    //-4 和 -50。

    int dollarsPart(double amount) const;
    int centsPart(double amount) const;
    int round(double number) const;

int main() {
    // 如果 main 函数与显示 8.1 中的相同，则屏幕对话
    // 将与显示 8.1 所示。

    const Money::operator+(const Money& operand) const {
        int allC1 = cents + dollars * 100;
        int allC2 = operand.cents + operand.dollars * 100;
        int sumAllCents = allC1 + allC2;
        int absAllCents = abs(sumAllCents);//Money 可以为负数。
        int finalDollars = absAllCents / 100;
        int finalCents = absAllCents % 100;
        if (sumAllCents < 0) {
            finalDollars = -finalDollars;
            finalCents = -finalCents;
        }
    }

const Money::operator-(const Money& operand) const {
    // 此定义的其余部分是自测练习 5。
}

bool Money::operator=(const Money& operand) const {
    return ((dollars == operand.dollars)
        && (cents == operand.cents));
}

const Money::operator() const {
    return Money(-dollars, -cents);
}

    // 所有其他成员函数的定义都与显示 8.1 相同。
```

# 提示：类可以访问其所有对象

在定义成员函数或运算符时，你可以访问调用对象的任何私有成员变量（或函数）。然而，你所拥有的权限甚至比此更多。你可以访问所定义类中任何对象的任何私有成员变量（私有成员函数）。
例如，考虑在显示 8.2 中 Money 类加法运算符定义中的以下几行：

```cpp
const Money::operator +(const Money& secondOperand) const {
    int allCents1 = cents + dollars*100;
    int allCents2 = secondOperand.cents + secondOperand.dollars
                               * 100;
}
```

在这种情况下，加法运算符被定义为成员运算符，而函数体第一行的变量 `cents` 和 `dollars` 是调用对象的成员变量（恰好是第一个操作数）。然而，通过名称访问对象 `secondOperand` 的成员变量是合法的，如下行所示：

```cpp
int allCents2 = secondOperand.cents + secondOperand.dollars * 100;
```

这是因为 `secondOperand` 是 Money 类的一个对象，并且该行位于 Money 类成员运算符的定义中。许多初级程序员错误地认为他们可以直接访问类对象的私有成员，而没有意识到他们可以访问所定义类的所有对象。

# 自测练习

- 5. 完成显示 8.2 中成员二元运算符的定义。

# 重载函数调用运算符 ( )

函数调用运算符 `()` 必须作为成员函数进行重载。它允许你像使用函数一样使用类的对象。如果 `AClass` 重载了函数调用以接受一个 `int` 类型参数，`anObject` 是 `AClass` 的一个对象，那么 `anObject (42)` 会调用重载的函数调用运算符 `()`，调用对象为 `anObject`，参数为 42。返回类型可以是 `void` 或任何其他类型。

函数调用运算符 `()` 的异常之处在于它允许任意数量的参数。因此，你可以定义多个版本的函数调用运算符 `()`。

## 陷阱：重载 &&、|| 和逗号运算符

`&&` 和 `||` 的预定义版本适用于 `bool` 的短路求值。然而，重载这些运算符时，它们会执行完全求值。这与大多数程序员的预期相悖，不可避免地会导致问题。最好的方法是不重载这两个运算符。

逗号运算符也存在问题。在正常使用中，逗号运算符保证从左到右求值。重载后，没有提供这种保证。逗号运算符是另一个最好避免重载的运算符。

# 8.2 友元函数与自动类型转换

信任你的朋友。

常见建议

友元函数是具有成员函数所有特权的非成员函数。在我们详细讨论友元函数之前，我们先讨论通过构造函数进行自动类型转换，因为这有助于解释将运算符（或任何函数）重载为友元函数的优势之一。

# 用于自动类型转换的构造函数

如果你的类定义包含适当的构造函数，系统将自动执行某些类型转换。例如，如果你的程序包含了显示 8.1 中或显示 8.2 中给出的 Money 类，你可以在程序中使用以下内容：

```cpp
Money baseAmount(100, 60), fullAmount;
fullAmount = baseAmount + 25;
fullAmount.output( );
```

输出将是

```
$125.60
```

之前的代码看起来可能简单且自然，但有一个微妙的点。`25`（在表达式 `baseAmount + 25` 中）并不是相应的类型。在显示 8.1 中，我们只重载了 `+` 运算符，使其能够与两个 `Money` 值使用。我们没有重载 `+` 以便它可以与一个 `Money` 值和一个整数使用。常量 `25` 可以被视为 `int` 类型，但除非类定义以某种方式告诉系统将整数转换为 `Money` 值，否则 `25` 不能用作 `Money` 的值。系统知道 `25` 的唯一方法是由于包含了一个接受 `int` 类型单个参数的构造函数。当系统看到表达式



```cpp
baseAmount + 25
```

它首先检查是否为 `Money` 值和整数的组合重载了运算符 `+`。由于没有这种重载，系统接着查找是否存在接受整数作为单个参数的构造函数。如果它找到一个接受单个参数的构造函数，它将使用该构造函数将 `25` 转换为 `Money` 值。单参数构造函数表示 `25` 应该转换为一个代表 $25.00 的 `Money` 对象。

注意，除非有合适的构造函数，否则这种类型转换将不起作用。如果类不包含一个带有 `int` 类型（或其他类型，如 `long`）参数的构造函数，则该类型转换无法工作。在显示 8.1 中，我们只重载了 `+` 运算符，使其能够与两个 `Money` 值使用。我们没有重载 `+` 以便它可以与一个 `Money` 值和一个整数使用。常量 `25` 可以被视为 `int` 类型，但除非类定义以某种方式告诉系统将整数转换为 `Money` 值，否则 `25` 不能用作 `Money` 的值。系统知道 `25` 的唯一方法是由于包含了一个接受 `int` 类型单个参数的构造函数。当系统看到表达式

```cpp
baseAmount + 25
```

它首先检查是否为 `Money` 值和整数的组合重载了运算符 `+`。由于没有这种重载，系统接着查找是否存在接受整数作为单个参数的构造函数。如果它找到一个接受单个参数的构造函数，它将使用该构造函数将 `25` 转换为 `Money` 值。单参数构造函数表示 `25` 应该转换为一个代表 $25.00 的 `Money` 对象。

注意，除非有合适的构造函数，否则这种类型转换将不起作用。如果类不包含一个带有 `int` 类型（或其他类型，如 `long`）参数的构造函数，则该类型转换无法工作。在显示 8.1 中，我们只重载了 `+` 运算符，使其能够与两个 `Money` 值使用。我们没有重载 `+` 以便它可以与一个 `Money` 值和一个整数使用。常量 `25` 可以被视为 `int` 类型，但除非类定义以某种方式告诉系统将整数转换为 `Money` 值，否则 `25` 不能用作 `Money` 的值。系统知道 `25` 的唯一方法是由于包含了一个接受 `int` 类型单个参数的构造函数。当系统看到表达式

```cpp
baseAmount + 25
```

它首先检查是否为 `Money` 值和整数的组合重载了运算符 `+`。由于没有这种重载，系统接着查找是否存在接受整数作为单个参数的构造函数。如果它找到一个接受单个参数的构造函数，它将使用该构造函数将 `25` 转换为 `Money` 值。单参数构造函数表示 `25` 应该转换为一个代表 $25.00 的 `Money` 对象。

