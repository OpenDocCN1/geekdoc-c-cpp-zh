

## 5.7.2 类 `DollarAmount`

**图 5.8** 定义了类 `DollarAmount`，其数据成员 `amount`（第 41 行）表示整数形式的美分数。

```cpp
// Fig. 5.8: DollarAmount.h
// DollarAmount class stores dollar amounts as whole numbers of pennies
#include <string>
#include <cmath>

class DollarAmount {
public:
    // initialize amount from an int64_t value
    explicit DollarAmount(int64_t value): amount{value} { }

    // add right's amount to this object's amount
    void add(DollarAmount right) {
        // can access private data of other objects of the same class
        amount += right.amount;
    }

    // subtract right's amount from this object's amount
    void subtract(DollarAmount right) {
        // can access private data of other objects of the same class
        amount -= right.amount;
    }

    // uses integer arithmetic to calculate interest amount,
    // then calls with the interest amount
    void addInterest(int rate, int divisor) {
        // create DollarAmount representing the interest
        DollarAmount interest{
            (amount * rate + divisor / 2) / divisor
        };

        add(interest); // add interest to this object's amount
    }

    // return a string representation of a DollarAmount object
    std::string toString() const {
        std::string dollars{std::to_string(amount / 100)};
        std::string cents{std::to_string(std::abs(amount % 100))};
        return dollars + "." + (cents.size() == 1 ? "0" : "") + cents;
    }

private:
    int64_t amount{0}; // dollar amount in pennies
};
```

图 5.8 `DollarAmount` 类以整数美分存储美元金额。

### C++11 类型 `int64_t`

11

我们希望数据成员 `amount` 能够存储从少量美分到较大美元金额的值，以便我们的 `DollarAmount` 可以用于所有可能的货币应用。在大多数计算机上，`int` 的取值范围为 −2,147,483,647 到 2,147,483,647。对于以美分存储的金额，这将把 `DollarAmount` 限制在大约 ±2100 万美元——对于许多货币应用来说太小了，所以我们需要大得多的范围。C++11 的 `long long` 类型作为*最小值*支持 −9,223,372,036,854,775,808 到 9,223,372,036,854,775,807 范围内的值。这将使 `DollarAmount` 的值达到 ±92 千万亿美元，对于所有已知的货币应用来说很可能绰绰有余。

11

`long long`（以及 C++ 的其他整数类型）的范围可能因平台而异。为了可移植性，我们希望在所有平台上使用*相同*的类型。为此，C++11 引入了新的整数类型名称，以便你可以为程序选择适当的值范围。对于类 `DollarAmount`，我们选择了 `int64_t`，它支持*精确的*范围 −9,223,372,036,854,775,808 到 9,223,372,036,854,775,807。有关 C++11 其他新整数类型名称的列表，请参阅头文件 `<cstdint>`。

### `DollarAmount` 构造函数

为简单起见，类 `DollarAmount` 的构造函数（图 5.8，第 9 行）接收一个整数美分数，并使用该值初始化数据成员 `amount`。在练习 5.30 中，你将定义一个 `DollarAmount` 构造函数，该构造函数接收两个参数，分别代表整数美元数和整数美分数，然后使用这些值计算并存储相应的美分数。（练习 5.30–5.34 与增强和使用类 `DollarAmount` 相关。）

### `DollarAmount` 成员函数 `add` 和 `subtract`

`add` 成员函数（第 12–15 行）接收另一个 `DollarAmount` 对象作为参数，并将其值添加到调用 `add` 的 `DollarAmount` 对象上。第 14 行使用 += 运算符将 `right.amount`（即参数对象中的 `amount`）加到当前对象的 `amount` 上，从而修改该对象。表达式 `right.amount` 访问对象 `right` 中的 `private amount` 数据成员。这是同类对象之间的一种特殊关系——类的成员函数既可以访问调用该函数的对象的 `private` 数据，也可以访问传递给该函数的同类其他对象的 `private` 数据。`subtract` 成员函数（第 18–21 行）的工作方式与 `add` 类似，但使用 -= 运算符从当前对象的 `amount` 中减去 `right.amount`。

### `DollarAmount` 成员函数 `addInterest`

`addInterest` 成员函数（第 25–32 行）使用其 `rate` 和 `divisor` 参数执行利息计算，然后将利息加到 `amount` 上。利息计算通常会产生需要舍入的小数结果。这里我们只进行整数算术计算，得出整数结果，因此完全避免了 `double` 的表示误差，但正如你将看到的，仍然需要进行舍入。

在本例中，我们使用*四舍五入*。首先，考虑将浮点值 0.75 和 0.25 舍入到最接近的整数。使用四舍五入时，.5 及更高的值应向上舍入，其他值应向下舍入，因此 0.75 向上舍入为 1，0.25 向下舍入为 0。

现在，让我们考虑对整数利息计算的结果进行舍入。假设我们要计算 $10.75 的 5% 利息。在整数算术中，我们将 10.75 视为 1075，要计算 5% 的利息，我们先乘以 5，再除以 100。在利息计算中，我们首先将 1075 乘以 5，得到整数值 5375，它表示 53 个整美分和 75 个百分之一美分。在这种情况下，这 75 个百分之一美分应向上舍入为一个整美分，结果是 54 个整美分。更一般地：

-   50 到 99 个百分之一美分应向上舍入到下一个更高的整美分
-   1 到 49 个百分之一美分应向下舍入到下一个更低的整美分

如果用 5375 除以 100 来完成利息计算，结果是 53，这是不正确的——请记住，整数算术会截断计算的小数部分。为了解决这个问题，我们必须向 5375 加上一个量，使得除以 100 后得到 54 个整美分。加上 50 可以确保 50 到 99 个百分之一美分向上舍入。例如：

-   5350 + 50 得到 5400——除以 100 得到 54
-   5375 + 50 得到 5425——除以 100 得到 54
-   5399 + 50 得到 5449——除以 100 得到 54

类似地：

-   5301 + 50 得到 5351——除以 100 得到 53
-   5325 + 50 得到 5375——除以 100 得到 53
-   5349 + 50 得到 5399——除以 100 得到 53

`addInterest` 中的第 27–29 行使用以下计算的结果初始化 `DollarAmount interest`，该计算执行了上述四舍五入：

```text
(amount * rate + divisor / 2) / divisor
```

这里，我们不是将 50 加到 `amount * rate` 的结果上，而是加上 `divisor / 2`。当 `divisor` 为 100 时，加上 50 是正确的，但对于其他除数，这将无法舍入到正确的数字位。考虑 $10.75 的 5.25% 利息。在整数算术中，我们将 10.75 视为 1075，要计算 5.25% 的利息，我们乘以 525，然后除以 10000。我们首先将 1075 乘以 525，得到整数值 564375，它表示 56 个整美分和 4375 个*万分之一*美分。这应向下舍入为 56 个整美分。为了正确舍入，在这种情况下，我们需要加上 5000——即除数 10000 的一半。

利息计算完成后，第 31 行调用成员函数 `add`，将新的 `DollarAmount` 对象 `interest` 作为参数传入——这会更新调用 `addInterest` 的 `DollarAmount` 对象中的 `amount`。请注意，类的任何成员函数都可以直接调用其他任何成员函数，以对类的同一对象执行操作。

### 成员函数 `toString`

`toString` 成员函数（第 35–39 行）返回 `DollarAmount` 对象美元金额的 `string` 表示。首先，第 36 和 37 行分别使用除法和取余运算符获取 `amount` 的美元和美分部分。我们将每个整数传递给 C++ 标准库函数 `to_string`（来自头文件 `<string>`），它将数值转换为 `string` 对象。第 37 行还使用 C++ 标准库函数 `abs`（来自头文件 `<cmath>`）获取美分的绝对值。这确保了美分始终表示为正数，因此减号不会出现在小数点的右侧。

第 38 行使用 + 运算符“相加”字符串字面量和 `string` 对象来生成要返回的 `string`——这称为**字符串拼接**。生成的 `string` 包含美元数、小数点和美分数。为了确保小数点右侧始终有两位数字，我们在 `string` `cents` 上调用 `string` 成员函数 `size`——该函数返回 `string` `cents` 中的字符数。如果结果为 `1`，我们就在美分数前拼接一个前导 `0`。

