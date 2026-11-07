
## **9.14**（标准库类 complex）

C++ 通过来自 `<complex>` 头文件的类型 complex 支持复数。创建以下复数：

```cpp
std::complex<double> x{2, 4};
std::complex<double> y{5, -1};
```

然后，使用这些复数演示：

- a) 使用 + 运算符将两个复数相加。
- b) 使用 - 运算符将两个复数相减。
- c) 使用 `std::cout` 打印复数。
- d) 将复数传递给函数 `std::real` 以获取实部。
- e) 将复数传递给函数 `std::imag` 以获取虚部。

## **9.15**（组合：Circle“有一个”位于其圆心的 Point）

圆有一个位于其圆心的点。创建一个表示 (x-y) 坐标对的 Point 类，并提供：

- a) 私有 int 数据成员 `m_x` 和 `m_y`，默认值为 0。
- b) 公有的 set 和 get 函数。
- c) 一个构造函数接收 x 和 y 坐标值以初始化 Point。
- d) 一个 move 函数，接收 x 和 y 坐标值并设置 Point 的新位置。
- e) 一个 `toString` 函数，返回 Point 的字符串表示。

创建一个 Circle 类，提供：

- a) 私有 Point 数据成员 `m_center`。
- b) 私有 double 数据成员 `m_radius`。
- c) 一个构造函数，接收表示 Circle 圆心的 Point 和表示 Circle 半径的 double。
- d) 一个 `toString` 函数，返回 Circle 的字符串表示，包括其圆心和半径。
- e) 一个 move 函数，接收 x 和 y 坐标值，并通过调用组合的 Point 对象的 move 函数为 Circle 设置新位置。

通过创建一个 Circle 对象、显示其字符串表示、移动该 Circle 并再次显示其字符串表示，来测试你的 Circle 类。

## **9.16**（Fraction 类）

创建一个名为 Fraction 的类，用于执行分数运算。编写一个程序来测试你的类。使用整型变量表示该类的私有数据——`m_numerator` 和 `m_denominator`。提供一个构造函数，使该类的对象在声明时能够被初始化。该构造函数应包含默认值，以防未提供初始化器，并应以约分形式存储分数。例如，分数

```
1/2
```

将在对象中存储为 `m_numerator` 中的 1 和 `m_denominator` 中的 2。提供执行以下各项任务的公有成员函数：

- a) `add`——将两个 Fraction 相加。结果应以约分形式存储。
- b) `subtract`——将两个 Fraction 相减。以约分形式存储结果。
- c) `multiply`——将两个 Fraction 相乘。以约分形式存储结果。
- d) `divide`——将两个 Fraction 相除。结果应以约分形式存储。
- e) `toString`——返回 Fraction 的字符串表示，形式为 a/b，其中 a 是分子，b 是分母。
- f) `toDouble`——以 double 形式返回 Fraction。

在第 11 章中，你将学习如何重载 +、-、*、/ 和 <<，以便编写诸如 a + b、a - b、a * b、a / b 和 `cout << a` 这样的表达式，来对 Fraction 进行加、减、乘、除和输出。

## **9.17** *（增强 Time 类）*

修改图 9.10–9.11 中的 Time 类，使其包含一个 tick 成员函数，该函数将 Time 对象中存储的时间增加一秒。编写一个程序，在循环中测试 tick 成员函数，在循环的每次迭代中按标准格式打印时间，以说明 tick 成员函数工作正常。确保测试以下情况：

- a) 增加到下一分钟。
- b) 增加到下一小时。
- c) 增加到下一天（即，11:59:59 PM 到 12:00:00 AM）。

## **9.18** *（增强 Date 类）*

修改图 9.19–9.20 中的 Date 类，对数据成员 `m_month`、`m_day` 和 `m_year` 的初始化值执行错误检查。此外，提供一个成员函数 `nextDay`，将日期增加一天。在循环中测试函数 `nextDay`，在每次迭代中打印日期，以说明 `nextDay` 工作正常。确保测试以下情况：

- a) 增加到下个月。
- b) 增加到下一年。

## **9.19** *（组合 Time 类和 Date 类）*

将练习 9.17 中修改后的 Time 类和练习 9.18 中修改后的 Date 类组合成一个名为 DateAndTime 的类。修改 tick 函数，使其在时间增加到下一天时调用 nextDay 函数。修改函数 `toStandardString` 和 `toUniversalString`，使它们各自返回包含日期和时间的字符串。编写一个程序来测试新类 DateAndTime。具体来说，测试将时间增加到下一天。

## **9.20** *（从 Time 类的 set 函数返回错误指示）*

修改图 9.10–9.11 中 Time 类的 set 函数，以便在尝试将 Time 类对象的数据成员设置为无效值时返回适当的错误值。编写一个程序来测试你新版本的 Time 类。当 set 函数返回错误值时显示错误消息。

## **9.21** *（Rectangle 类）*

创建一个 Rectangle 类，其属性为 `m_length` 和 `m_width`，二者均默认为 1。提供计算矩形周长和面积的成员函数。此外，为 `m_length` 和 `m_width` 属性提供 set 和 get 函数。set 函数应验证 `m_length` 和 `m_width` 均大于 0.0 且小于 20.0。

## **9.22** *（SavingsAccount 类）*

创建一个 SavingsAccount 类。使用静态数据成员 `m_annualInterestRate` 存储每个储户的年利率。每个账户都有一个私有数据成员 `m_savingsBalance`，表示存款金额。提供成员函数 `calculateMonthlyInterest`，通过将 `m_savingsBalance` 乘以 `m_annualInterestRate` 再除以 12 来计算月利息；该利息应加到 `m_savingsBalance` 中。提供一个静态成员函数 `modifyInterestRate`，将静态 `m_annualInterestRate` 设置为新值。编写一个驱动程序来测试 `SavingsAccount` 类。实例化 `SavingsAccount` 类的两个不同对象 saver1 和 saver2，余额分别为 $2000.00 和 $3000.00。将 `m_annualInterestRate` 设置为 3%。然后计算月利息，并为每个储户打印新余额。然后将 `m_annualInterestRate` 设置为 4%，计算下个月的利息，并为每个储户打印新余额。

## **9.23** *（IntegerSet 类）*

创建 `IntegerSet` 类，其每个对象可以保存 0 到 100 范围内的整数。在内部将该集合表示为 bool 值 vector。如果整数 i 在集合中，则元素 `m_boolSet[i]` 为 true。如果整数 j 不在集合中，则元素 `m_boolSet[j]` 为 false。默认构造函数将集合初始化为所谓的“空集”，即所有元素都包含 false 的集合。

- a) 为常见集合操作提供成员函数。例如，提供一个 `unionOfSets` 成员函数，创建一个第三个集合，它是两个现有集合的集合论并集（即，如果某个元素在现有集合的任一或两者中为 true，则结果中的该元素被设置为 true；如果某个元素在每个现有集合中均为 false，则结果中的该元素被设置为 false）。
- b) 提供一个 `intersectionOfSets` 成员函数，创建一个第三个集合，它是两个现有集合的集合论交集（即，如果某个元素在现有集合的任一或两者中为 false，则结果中的该元素被设置为 false；如果某个元素在每个现有集合中均为 true，则结果中的该元素被设置为 true）。
- c) 提供一个 `insertElement` 成员函数，通过将 `m_boolSet[k]` 设置为 true 来将新整数 *k* 放入集合中。提供一个 `deleteElement` 成员函数，通过将 `m_boolSet[m]` 设置为 false 来删除整数 *m*。
- d) 提供一个 `toString` 成员函数，将集合作为字符串返回，其中包含以空格分隔的数字列表。仅包含集合中存在的那些元素（即，它们在 vector 中的位置值为 true）。对于空集，返回空字符串。
- e) 提供一个 `isEqualTo` 成员函数，用于确定两个集合是否相等。
- f) 提供一个额外的构造函数，接收一个整数数组，并使用该数组初始化一个集合对象。

现在编写一个驱动程序来测试你的 `IntegerSet` 类。实例化几个 `IntegerSet` 对象。测试你的所有成员函数是否正常工作。

## **9.24** *（洗牌和发牌）*

创建一个程序来洗牌并发出（deal）一副牌。该程序应由 `Card` 类、`DeckOfCards` 类和驱动程序组成。`Card` 类应提供：

- a) 数据成员 `m_face` 和 `m_suit`——使用枚举表示点数和花色。
- b) 一个构造函数，接收两个表示点数和花色的枚举常量，并使用它们初始化数据成员。
- c) 两个字符串静态数组，分别表示点数和花色。
- d) 一个 `toString` 函数，将 `Card` 作为字符串返回，形式为“face of suit”。你可以使用 + 运算符连接字符串。

`DeckOfCards` 类应包含：

- a) 一个名为 `m_deck` 的 `Cards` 数组，用于存储这些牌。
