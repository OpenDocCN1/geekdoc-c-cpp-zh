

# 附录 B 编程中的重要主题

检查逻辑错误（容错编程中的错误）。一个看起来运行正常的程序在某些时刻可能会出现意料之外的行为，即使它读取的数据是有效的。例如，程序可能没有考虑到引起意外情况的特定数据，尽管你已经尝试测试了程序的逻辑。或者，你修改了程序，而该修改使你在程序其他部分所做的某个假设失效了。无论困难有多大，程序都应该具有防止此类错误的内置保护措施。它应该监控自己，并能够指示出某些错误，并且你不应该信任这些结果。

## B.5.1 保护输入数据中的错误

假设你正在计算收入在 $10,000 到 $100,000 之间的人的统计数据。这些区间四舍五入到最近的千美元：$10,000、$11,000，等等，直到 $100,000。原始数据是一个包含一行或多行如下格式的文件：

`G N` 其中 N 是收入落在 G 千美元组的人数。如果有多人汇总了这些数据，可能会出现同一个 G 值的多个条目。当用户输入数据时，程序必须为每个 G 值增加并记录人数。从上下文中可以明显看出，G 是 10 到 100 之间的整数，N 是一个非负整数。

作为一个防止输入错误的示例，考虑一个用于此问题的输入函数。编写此函数的首次尝试将说明程序无法达到容错理想的常见方式。最终，你将看到一个与原始解决方案更接近的输入函数。

函数的第一次尝试可能是：

```cpp
const int LOW_END = 10; // 1万美元收入
const int HIGH_END = 100; // 10万美元收入
const int TABLE_SIZE = HIGH_END - LOW_END + 1;
typedef TableType[TABLE_SIZE];
/**
 * readData 组织收入统计数据。
 * @param incomeData 一组收入统计数据的表类型 A。
 * @pre 调用函数向用户提供指导。
 * 输入是无错误的，其中 A 是收入在 G 千美元组且 LOW_END <= G <= HIGH_END 的人数。
 * 一行同时包含 G 和 N 值的输入行将结束输入。
 * @post 对于每个 G，incomeData[G-LOW_END] 是收入在 G 千美元组的人数总量。显示这些值。 */
void readData(TableType incomeData) {
    bool terminateInput = false;
    int group, number; // 输入值
    for (group = LOW_END; group <= HIGH_END; group++)
        incomeData[group - LOW_END] = 0;
    do {
        cout << "Please enter group and number of ";
        cout << "people in group, separated by a space: ";
        cin >> group >> number;
```

这个函数不是容错的：

```cpp
        terminateInput = (group == 0) && (number == 0);

        // group 和 number 不为 0
        cout << "Income group " << group << " contains "
        << number << " people.\n";
        incomeData[group - LOW_END] += number;
    } while (terminateInput); // 结束 do-while
} // 结束 readData
```

这个函数存在问题。如果输入行包含意外数据，程序的行为将不合理。考虑两种可能性：

- 输入行上的第一个整数（函数赋值给 group）不在 LOW_END 到 HIGH_END 范围内。引用 `incomeData[group - LOW_END]` 是错误的，因为它访问了数组边界之外的元素。当用户试图通过为 group 和 number 输入 0 来结束输入时，也会发生这种错误。
- 输入行上的第二个数字（函数赋值给 number）是负数。虽然 number 的负值是合法的（因为一个收入组中不可能有负数的人），但函数会将该值加到组数组中。因此，arrayData 将是错误的。

在函数读取 group 和 number 的值之后，它必须检查 group 是否在 LOW_END 到 HIGH_END 之间，以及 number 是否为正数。如果任一值不在范围内，你就要处理输入错误。

假设你不是在将 number 值加到数组 `incomeData[group - LOW_END]` 之前检查其值，而是执行加法并查看和是否为正数。这种方法是不够的，你可能会将一个负值添加到 incomeData 的条目中，而该条目并没有变成负数。例如，如果 number 是 -4,000，且数组 `incomeData` 中对应的条目是 10,000，那么 number 的负值可能无法被检测到，导致程序其余部分的失效。

当数据无效时，函数可以采取的一种可能的行动是设置错误标志并终止。另一种可能性是设置错误标志，忽略错误的输入行并继续。哪种操作是正确的取决于程序在读取数据后如何使用它。

下面的 `readData` 尝试尽可能通用，并使函数尽可能具有适应性。当函数遇到错误时，它返回调用模块，以便在发生输入错误时确定适当操作——例如中止或继续。因此，你可以在许多语文中使用同一个函数，并在需要时轻松修改方法。

```cpp
/**
 * readData 程序统计收入数据。
 * @param incomeData 收入统计数据的表类型 A。
 * @pre 调用行包含正好两个符合 G N 格式的整数，
 * 其中 N 是收入在 G 千美元组的人数，且 LOW_END <= G <= HIGH_END。两个值均为 0 的输入行将结束输入。
 * @post incomeData[G - LOW_END] 是收入在 G 千美元组的人数总量。值被读取并显示。如果 G 或 N 任一出错（无论是 G < LOW_END, G > HIGH_END 或 N < 0），函数将忽略该数据行并继续执行。
 * @return 如果读取的任何数据行 G 或 N 出错（无论是 G < LOW_END, G > HIGH_END 或 N < 0），则返回 true。在这种情况下，调用程序应采取行动。如果数据行无错误，则返回 true。 */
bool readData(TableType incomeData)
{
    int group = -1;
    int number = -1; // 输入值
    bool dataCorrect = true; // 尚未发现数据错误
    bool userFinished = false;

    for (group = LOW_END; group <= HIGH_END; group++)
        incomeData[group - LOW_END] = 0;
    do {
        cout << "Please enter group and number of ";
        cout << "number, separated by a space: ";
        cin >> group >> number;

        cout << "Input line specifies that income group ";
        cout << group << "\ncontains " << number << "\n";
        if (group >= LOW_END) && (group <= HIGH_END) {
            if (number >= 0)
                // 输入数据有效 - 累加
                incomeData[group - LOW_END] += number;
            else if (group == 0) && (number == 0)
                userFinished = true; // 用户结束
            else
                // 输入错误：
                // 设置错误标志并忽略输入
                dataCorrect = false;
        }
    } while (dataCorrect && !userFinished); // 结束 do-while
    return dataCorrect;
} // 结束 readData
```

尽管此函数能够优雅地处理常见的输入错误，但它并不是完全容错的。如果输入行只包含一个整数会怎样？如果输入行包含非数字会怎样？如果函数逐字符读取、将字符转换为整数并检查输入行的结束，它将更具容错性。在大多数语文中，这可能有点极端。然而，如果输入数据的人输入非整数，你可以轻松地修改输入函数，因为该函数是一个隔离的模块。在任何情况下，函数的初始注释都应该包含它对数据的所有假设，以及可能导致程序正常中止的指示。

## B.5.2 防止程序逻辑错误

现在考虑程序应该防止的第二类错误：其自身的逻辑错误。这些错误在你调试程序时可能没有捕获，或者是你通过程序修改引入的。

遗憾的是，程序无法让你知道它的（告知你错误的机制）出了问题（你能依赖一个程序来告诉你它告知你错误的机制本身出了问题吗？）。然而，你可以在程序中构建一种机制，确保当程序执行算法时，某些条件始终成立。例如，上一个示例中 `incomeData` 数组中的所有整数必须大于或等于零。虽然
```