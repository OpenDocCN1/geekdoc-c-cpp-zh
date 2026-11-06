

### 5. 9.7（*增强 `Time` 类*）

修改图 9.5–9.6 中的 `Time` 类，加入一个 `tick` 成员函数，将 `Time` 对象中存储的时间递增一秒。编写一个程序，在循环中测试 `tick` 成员函数，并在每次循环迭代中按标准格式打印时间，以说明 `tick` 成员函数工作正确。务必测试以下情况：

- A. 递增到下一分钟。
- B. 递增到下一小时。
- C. 递增到下一天（即 11:59:59 PM 到 12:00:00 AM）。

### 6. 9.8（*增强 `Date` 类*）

修改图 9.14–9.15 中的 `Date` 类，对数据成员 `month`、`day` 和 `year` 的初始值执行错误检查。另外，提供一个成员函数 `nextDay`，将日期增加一天。编写一个程序，在循环中测试函数 `nextDay`，并在每次迭代中打印日期，以说明 `nextDay` 工作正确。务必测试以下情况：

- A. 递增到下一月。
- B. 递增到下一年。

### 7. 9.9（*合并 `Time` 类和 `Date` 类*）

将*练习 9.7*中修改后的 `Time` 类和*练习 9.8*中修改后的 `Date` 类合并为一个名为 `DateAndTime` 的类。修改 `tick` 函数，使时间递增到下一天时调用 `nextDay` 函数。修改函数 `toStandardString` 和 `toUniversalString`，使每个函数返回的 `string` 都包含日期和时间。编写一个程序来测试新的 `DateAndTime` 类，具体测试时间递增到下一天的情况。

### 8. 9.10（**从 `Time` 类的 set 函数返回错误指示符**）

修改图 9.5–9.6 中 `Time` 类的 set 函数，使这些函数在尝试将 `Time` 类对象的数据成员设置为无效值时返回适当的错误值。编写一个程序来测试新版本的 `Time` 类。当 set 函数返回错误值时，显示错误消息。

### 9. 9.11（**`Rectangle` 类**）

创建一个具有属性 `length` 和 `width` 的 `Rectangle` 类，两者的默认值均为 1。提供成员函数来计算矩形的 `perimeter`（周长）和 `area`（面积）。此外，为 `length` 和 `width` 属性提供 set 和 get 函数。set 函数应验证 `length` 和 `width` 均为大于 0.0 且小于 20.0 的浮点数。

### 10. 9.12（**增强 `Rectangle` 类**）

创建一个比你在**练习 9.11**中创建的 `Rectangle` 类更复杂的类。该类只存储矩形四个角的笛卡尔坐标。构造函数调用一个 set 函数，该函数接受四组坐标，并验证每组坐标都位于第一象限，且任何单个 x 或 y 坐标都不大于 20.0。该 set 函数还验证所提供的坐标确实指定了一个矩形。提供成员函数来计算 `length`（长度）、`width`（宽度）、`perimeter`（周长）和 `area`（面积）。`length` 是两个维度中较大的一个。包含一个谓词函数 `square`，判断该矩形是否为正方形。

### 11. 9.13（*增强 `Rectangle` 类*）

修改**练习 9.12**中的 `Rectangle` 类，加入一个 `draw` 函数，在一个 25×25 的方框内显示该矩形，方框包围矩形所在的第一象限区域。加入一个 `setFillCharacter` 函数，指定用于填充矩形主体的字符。加入一个 `setPerimeterCharacter` 函数，指定用于绘制矩形边框的字符。如果你愿意接受挑战，还可以加入缩放矩形大小以及让其在第一象限指定区域内移动的函数。

### 12. 9.14（*HugeInteger* 类）

创建一个 `HugeInteger` 类，使用一个包含 40 个数字元素的数组来存储最大达 40 位的整数。提供成员函数 `input`、`output`、`add` 和 `subtract`。为了比较 `HugeInteger` 对象，提供函数 `isEqualTo`、`isNotEqualTo`、`isGreaterThan`、`isLessThan`、`isGreaterThanOrEqualTo` 和 `isLessThanOrEqualTo`——这些函数都是“谓词”函数，如果两个 `HugeInteger` 之间满足该关系，则返回 `true`；如果不满足，则返回 `false`。另外，提供一个谓词函数 `isZero`。如果你愿意接受挑战，可以提供成员函数 `multiply`、`divide` 和 `remainder`。在第 10 章中，你将学习如何重载输入、输出、算术、相等和关系运算符，以便你可以编写包含 `HugeInteger` 对象的表达式，而不是显式调用成员函数。

### 13. 9.15（*`TicTacToe` 类*）

创建一个 `TicTacToe` 类，使你能够编写一个完整的井字棋游戏程序。该类包含一个作为 `private` 数据的 3×3 二维整数数组。构造函数应将空棋盘初始化为全 0。允许两名人类玩家。第一名玩家每次落子时，在指定方格中放入 1；第二名玩家每次落子时，放入 2。每次落子都必须落在空方格中。每次落子后，判断游戏是否已获胜或平局。如果你愿意接受挑战，可以修改程序，使计算机代替其中一名玩家落子。此外，允许玩家指定自己先走还是后走。如果你想要挑战极高难度，可以在 4×4×4 的棋盘上开发一个三维井字棋程序。*[注意：这是一个极具挑战性的项目，可能需要花费数周时间！]*

### 14. 9.16（**友元关系**）

解释友元关系的概念。解释文中所描述的友元关系的负面方面。

### 15. 9.17（**构造函数重载**）

一个 `Time` 类定义如果同时包含*以下两个*构造函数：

```cpp
Time(int h = 0, int m = 0, int s = 0);
Time();
```

能否用于默认构造一个 `Time` 对象？如果不能，请解释原因。

### 16. 9.18（*构造函数和析构函数*）

如果为构造函数或析构函数指定返回类型（即使是 `void`），会发生什么？

### 17. 9.19（*修改 Date 类*）

修改**图 9.18**中的 `Date` 类，使其具备以下功能：

- A. 以多种格式输出日期，例如：

```text
June 14, 1992
DDD, YYYY
MM/DD/YY
```

- B. 使用重载构造函数创建 `Date` 对象，并以第 (a) 部分中的日期格式进行初始化。

- C. 创建一个 `Date` 构造函数，使用 `<ctime>` 头文件中的标准库函数读取系统日期，并设置 `Date` 的成员。有关 `<ctime>` 头文件中函数的信息，请参阅你的编译器参考文档或 [http://en.cppreference.com/w/cpp/chrono/c](http://en.cppreference.com/w/cpp/chrono/c)。你可能还想查看 [http://en.cppreference.com/w/cpp/chrono](http://en.cppreference.com/w/cpp/chrono) 上的 C++11 `chrono` 库。

在**第 10 章**中，我们将能够创建运算符来测试两个日期是否相等，并比较日期以确定一个日期是在另一个日期之前还是之后。

### 18. 9.20（**`SavingsAccount` 类**）

创建一个 `SavingsAccount` 类。使用一个 `static` 数据成员 `annualInterestRate` 来存储每位储户的年利率。该类的每个对象包含一个 `private` 数据成员 `savingsBalance`，表示储户当前存款的金额。提供成员函数 `calculateMonthlyInterest`，通过将 `savingsBalance` 乘以 `annualInterestRate` 再除以 12 来计算月利息；该利息应加到 `savingsBalance` 中。提供一个 `static` 成员函数 `modifyInterestRate`，将 `static` 的 `annualInterestRate` 设置为新值。编写一个测试程序来测试 `SavingsAccount` 类。实例化 `SavingsAccount` 类的两个不同对象 `saver1` 和 `saver2`，余额分别为 $2000.00 和 $3000.00。将 `annualInterestRate` 设置为 3%，然后计算月利息，并打印每位储户的新余额。再将 `annualInterestRate` 设置为 4%，计算下个月的利息，并打印每位储户的新余额。

### 19. 9.21（**`IntegerSet` 类**）

创建一个 `IntegerSet` 类，其每个对象可以容纳 0 到 100（含）范围内的整数。

