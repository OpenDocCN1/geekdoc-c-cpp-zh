

- 23. 函数声明为：

    ```cpp
    double readFilter();
    //Reads a number from the keyboard. Returns the number
    //read provided it is >= 0; otherwise returns zero.
    ```

    函数定义为：

    ```cpp
    //uses iostream
    double readFilter()
    {
        using namespace std;
        double valueRead;
        cout << "Enter a number:\n";
        cin >> valueRead;

        if (valueRead >= 0)
            return valueRead;
        else
            return 0.0;
    }
    ```

- 24. 函数调用只有一个参数，因此它会使用只有一个形参的函数定义。

- 25. 函数调用有两个 `double` 类型的参数，因此它会使用与有两个 `double` 类型参数的函数声明相对应的函数，即第一个函数声明。

- 26. 第二个参数是 `int` 类型，第一个参数会由 C++ 在需要时自动转换为 `double` 类型，因此它会使用与第一个参数为 `double` 类型、第二个参数为 `int` 类型的函数声明相对应的函数，即第二个函数声明。

- 27. 第二个参数是 `double` 类型，第一个参数会由 C++ 在需要时自动转换为 `double` 类型，因此它会使用与有两个 `double` 类型参数的函数声明相对应的函数，即第一个函数声明。

- 28. 这无法做到（至少不能以优雅的方式做到）。正方形披萨和圆形披萨的自然表示方式是相同的。两者都自然地表示为一个数字，即圆形披萨的直径和方形披萨一边的长度。在任何情况下，`unitprice` 函数都需要有一个 `double` 类型的价格形参和一个 `int` 类型的尺寸形参（半径或边长）。因此，这两个函数声明将具有相同数量和类型的形参。具体来说，它们都将有一个 `double` 类型的形参和一个 `int` 类型的形参。因此，编译器将无法决定使用哪个定义。你仍然可以通过定义两个函数来击败这种邪恶的披萨店的策略，但它们需要有不同的名称。

- 29. `unitprice` 的定义不进行任何输入或输出，因此不使用库 `iostream`。在 `main` 中我们需要使用指令，因为 `cin` 和 `cout` 在 `iostream` 中定义，并且这些定义将 `cin` 和 `cout` 放在 `std` 命名空间中。

## Practice Programs

*Practice Programs can generally be solved with a short program that directly applies the programming principles presented in this chapter.*

- 1. 直角三角形的斜边长度是另外两边平方和的平方根。编写一个函数 `calcH`，接受两个 `double` 作为函数参数并返回一个 `double`。提示用户输入三角形的底边长度和垂直边长度。使用 `cmath` 中的 `pow` 和 `sqrt` 函数执行计算。

- 2. 修改你在练习程序 1 中的程序以添加一个计算三角形周长的函数。你的函数 `calcPerimeter` 应接受两个参数并返回一个 `double`。你的 `calcPerimeter` 函数应在计算周长时使用你的 `calcH` 函数。将周长添加到你的程序输出中。

- 3. 股票价格有时以美元的八分之一为单位给出；例如，29 7/8 或 89 1/2。编写一个程序来计算用户持有一只股票的价值。程序会询问用户持有的股票数量、价格的整数美元部分以及分数部分。分数部分应作为两个 `int` 值输入，一个为分子，一个为分母。程序随后输出用户持有的价值。你的程序应允许用户根据需要重复此计算，并包含一个函数定义，该函数具有三个 `int` 参数，由价格的整数美元部分和构成分数部分的两个整数组成。该函数返回一只股票的价格作为单个 `double` 类型数字。

- 4. 在一次考试中，学生每答对一题得 1 分，每答错一题扣 0.25 分。编写一个程序提示用户输入学生答对的问题数量和答错的问题数量。程序应使用函数 `calcMarkAsPercentage` 计算学生的最终成绩百分比。仔细考虑计算正确分数所需的运算顺序以及是否需要转换任何值。

- 5. 修改你在上一个练习程序中的程序，要求用户输入要输入成绩的学生人数。你的程序随后应提示用户输入所需数量学生的成绩。如果学生的分数低于 0，则其成绩应设为 0 并输出为 0。你的程序随后应打印所计算学生的最高分、最低分和平均分。

- 6. 为计算信用卡账户余额的利息编写一个函数的函数声明。该函数接受初始余额、月利率以及需要支付利息的月数作为参数。返回值是应付利息。不要忘记复利——即对到期利息计息。到期利息计入应付余额，下个月的利息使用这个更大的余额计算。使用一个类似于（但不必完全相同于）Display 2.14 中所示的 `while` 循环。将函数嵌入到一个读取利率、初始账户余额和月数然后输出应付利息的程序中。将你的函数定义嵌入到一个让用户计算信用卡账户余额应付利息的程序中。程序应允许用户在用户说想结束程序之前重复计算。

- 7. 两个质量分别为 *m₁* 和 *m₂*、相距 *d* 的物体之间的引力吸引力由下式给出：

    $$F = \frac{Gm_1m_2}{d^2}$$

    其中 G 是万有引力常数：

    $$G = 6.673 \times 10^{-8}\left(\frac{\mathrm{cm}^3}{\mathrm{g} \times \mathrm{sec}^2}\right)$$

    编写一个函数定义，接受两个物体的质量和它们之间的距离作为参数并返回引力。 由于你将使用上述公式，引力将以达因为单位。一个达因等于

    $$\left(\frac{\mathrm{g} \times \mathrm{cm}}{\mathrm{sec}^2}\right)$$

    你应使用全局定义的常数作为万有引力常数。将你的函数定义嵌入到一个完整的程序中，根据合适的输入计算两个物体之间的引力。你的程序应允许用户根据需要重复此计算。

    ![](img/88b1f375f11336dbd9dac8b1675d0698_280_0.png)

- 8. 我们“被祝福”拥有多个绝对值函数是历史的偶然。C 库在 C++ 出现时已经可用；它们可以很容易地使用，因此没有使用函数重载重写。你需要找到你能找到的所有绝对值函数并重写它们以重载 `abs` 函数名。至少，你应包含 `int`、`long`、`float` 和 `double` 类型。

- 9. 编写一个重载函数 `max`，它接受两个或三个 `double` 类型的参数并返回其中最大的一个。

You can find estimates of the caloric content of many foods on the Web. For example, a double cheeseburger has approximately 1000 calories.

- 6. 你发明了一台能够油炸松饼的自动售货机。编写一个程序来模拟自动售货机。购买一个油炸松饼的价格为 $3.50，机器只接受面值一美元、25美分、10美分或5美分的硬币。编写代码模拟一个人将钱投入自动售货机，通过反复提示用户插入下一枚硬币。当每枚硬币插入时输出迄今为止的总金额。当添加 $3.50 或更多时，程序应输出“Enjoy your deep-fried twinkie”以及应退还的任何找零。使用自顶向下设计来确定程序的适当函数。

- 7. 你的时光机最多可向前跳跃 24 小时。机器配置为以分钟为单位跳跃。为了输入正确的分钟数到你的机器中，你希望有一个程序可以接受一个开始时间（以小时、分钟和表示 AM 或 PM 的布尔值）和一个未来时间（以小时、分钟和表示 AM 或 PM 的布尔值）并计算开始时间和未来时间之间的分钟差。

    程序中时间以三个变量指定：

    ```cpp
    int hours, minutes;
    bool isAM;
    ```

    例如，要表示 11:50 PM，你会存储：

    ```cpp
    hours = 11
    minutes = 50
    isAM = false;
    ```

    这意味着你需要六个变量来存储开始时间和未来时间。

    编写一个程序允许用户输入开始时间和未来时间。包含一个名为 `computeDifference` 的函数，该函数将代表开始时间和未来时间的六个变量作为参数。你的函数应返回作为 `int` 的时间差（以分钟为单位）。例如，给定开始时间为 11:59 AM 和未来时间为 12:01 PM，你的程序应计算时间差为 2 分钟。给定开始时间为 11:59 AM 和未来时间为 11:58 AM，你的程序应计算时间差为 1439 分钟（23 小时 59 分钟）。

    你可能需要从用户输入中读取两个字符值来获取“AM”或“PM”。（Display 2.3 说明了字符输入。）字符可以像数字一样比较。例如，如果变量 `aChar` 是 `char` 类型，则 `(aChar == 'A')` 是一个布尔表达式，如果 `aChar` 包含字母 A 则求值为 true。

- 8. Do Programming Project 11 from Chapter 3 except write a function named containsDigit that determines if a number contains a particular digit. The header should look like:

