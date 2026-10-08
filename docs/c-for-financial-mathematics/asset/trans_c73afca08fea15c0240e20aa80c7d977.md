

几乎任何其他函数的性能优化，你的努力都将白费！

在对代码进行任何严肃的优化尝试之前，建议你先对代码进行性能分析（profile）。

除非你的性能要求非常精确，否则你未必需要购买单独的软件来分析代码性能。一种简单的方法是执行那段较慢的代码，然后随机停止处理十次，并记录当时正在发生什么。你很可能发现，每次停止时代码做的事情都差不多。你可以安全地推断出性能问题就出在这里。

必须指出，这本书是关于编写高质量 C++ 代码的，但并不是关于编写具有绝对最优性能的 C++ 代码。对于大多数问题来说，代码能够正确执行比它以人类可能的最快速度执行要重要得多。大多数时候，为了代码的其他良好品质——如易于理解、阅读和扩展——而牺牲一些速度是值得的。

唐纳德·克努斯（Donald Knuth），图灵奖得主，著名的编程专家，曾名言：“过早优化是万恶之源”（Premature optimisation is the root of all evil）。

## 15.4.10 示例

这本书拥有一个复杂的构建流程。文本使用 LaTeX 编写，并引用了众多不同项目中的各种 C++ 文件。每当这本书做出任何更改时，所有的 C++ 代码都会经过编译，并在 Windows 和 Unix 上进行测试。此外，还有测试用于检查 LaTeX 文档中显示的所有代码是否与计算机项目中的 C++ 代码相匹配。最后，将所有代码示例和文本放到网站上的过程完全是自动化的。

如果没有自动构建，这本书将布满（甚至更多）错误。所有代码都包含 bug，毫无疑问这本书也包含许多错误。尽管如此，自动构建确保了最严重的问题能被迅速消除。

## 练习

- 15.4.1. 找出并修复 FMLib15 中的所有 bug。
- 15.4.2. 尝试在调试信息关闭并替换为优化后的机器代码的情况下运行 FMLib。你可以在 Visual Studio 中通过从菜单栏选择 Release 选项来实现这一点。此外，对于专家而言，项目配置选项让你可以访问大量的配置参数，其中许多可用于调整性能。

在 Unix 上，你应该从 Makefile 中移除调试选项 `-g` 和 `-D_GLIBCXX_DEBUG`，并用 `-O` 代替以进行优化。然后你应该运行 **make clean**。每次你更改 Make 文件中的选项时，都应该运行 **make clean**。还有各种更复杂的优化选项可供使用。请参见 **gcc** 的文档。

这对程序运行的速度有多大影响？你可能需要更改 **testPlotDeltaHedding-Histogram** 中的步数，使代码运行得更慢，以便更容易看到差异。

## 15.5 总结

调试器是寻找代码错误所在的一个有用工具。调试器的两个重要用途是：

- 在错误发生时获取堆栈跟踪；
- 逐行单步执行代码，以查看正在发生的事情。

虽然调试器是一个有用的工具，但它不能替代单元测试。相反，它是一种互补的开发技术。

在编写软件时，你应该使用一些工具和技术。这些包括版本控制和 bug 数据库。调试和维护代码的技能至少与编写代码本身的技能同等重要。虽然我们并未试图深入探讨这些问题，但书 [5] 和 [1] 讨论了软件开发中超越简单编码的重要方面。

```cpp
 double HedgingSimulator::runSimulation() const {
    double T = toHedge->getMaturity();
    double S0 = simulationModel->stockPrice;
    vector<double> pricePath =
    simulationModel->generatePricePath(T,nSteps);

    double dt = T / nSteps;
    double charge = chooseCharge(S0);
    double stockQuantity = selectStockQuantity(0,S0);
    double bankBalance = charge - stockQuantity*S0;
    for (int i = 0; i< nSteps-1; i++) {
        double interest = bankBalance *
        exp(simulationModel->riskFreeRate*dt);
        double S = pricePath[i];
        double date = dt*(i + 1);
        double newStockQuantity
        = selectStockQuantity(date, S);
        double costs
        = (newStockQuantity - stockQuantity)*S;
        bankBalance = bankBalance + interest - costs;
        stockQuantity = newStockQuantity;
    }
    double interest = bankBalance *
    exp(simulationModel->riskFreeRate*dt);
    double S = pricePath[nSteps];
    double stockValue = stockQuantity*S;
    double payout = toHedge->payoff(S);
    return bankBalance +interest
    +stockValue - payout;
}
```

![](img/c60a618fcc2a2ed9d1e8d96a1b4157ff_287_0.png)

![](img/c60a618fcc2a2ed9d1e8d96a1b4157ff_288_0.png)

# 第 16 章 矩阵类

C++ 没有内置的表示实数矩阵的类。我们将在本章中编写我们自己的类。

在编写 **Matrix** 类的过程中，我们将涵盖一些有趣的 C++ 主题。具体包括：

- 构造器和析构器，
- 运算符重载，
- 三法则，
- 返回引用，
- 使用 `const` 进行重载。

## 16.1 Matrix 的基本功能

让我们开始设计矩阵类的基本行为。**Matrix** 类将存储一个双精度浮点数的二维数组，并具有以下数据成员（均为私有的）。

- (i) `int nrows`。行数。
- (ii) `int ncols`。列数。
- (iii) `double* data`。指向第一个单元格的指针。
- (iv) `double* endPointer`。指向最后一个单元格之后位置的指针。

指针 `data` 将指向一块长度为 $\text{nrows} \times \text{ncols}$ 的连续内存块。单元格 $(i, j)$ 将存储在位置 `data+(j*nRows)+i`。请注意，我们在最后这个表达式中使用了指针算术。

我们决定使用指针和 `new []` 运算符，而不是 **vector**，因为最终，如果你想要使用特殊的 CPU 优化（如我们将在 16.7 节中讨论的那样），你需要有一个指向数据的指针，而不仅仅是一个 **vector** 对象。此外，这使得这个 **Matrix** 类成为测试你指针编程技能的一个良好工具。

以下是 **Matrix** 数据成员的声明。

```cpp
private:
    /* The number of rows in the matrix */
    int nrows;
    /* The number of columns */
    int ncols;
    /* The data in the matrix */
    double* data;
    /* Pointer to one after the end of the data */
    double* endPointer;
```

我们的矩阵类允许用户读取行数和列数，但不能更改它们。因此，我们在头文件中添加了以下数据访问方法：

```cpp
    /* The number of rows in the matrix */
    int nRows() const {
        return nrows;
    }

    /* The number of columns in the matrix */
    int nCols() const {
        return ncols;
    }
```

这些方法是内联的——也就是说，我们在类声明内部写函数定义。由于我们将大量使用 Matrix 类，利用一些内联优化是很重要的。

我们已经指出，单元格 $(i,j)$ 的值存储在内存位置 $data + (j * nRows) + i$。让我们提供获取和设置函数，以便用户可以读取给定单元格的值并更改单元格的值。

```cpp
    /* Retrieve the value at the given index */
    double get( int i, int j ) const {
        return data[ offset( i, j ) ];
    }

    /* Set the value at the given index */
    void set( int i, int j, double value ) {
        data[ offset( i, j ) ] = value;
    }
```

这两个函数都利用了 offset 函数。该函数执行计算，确定单元格 $(i,j)$ 相对于 data 指针在内存中的存储位置。

