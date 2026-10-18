
# 3.15.3 输入和输出操作（EMatrix）

如前所述，我们已经推迟了针对 EMatrix 对象执行特定操作的函数定义。在本节中，我们将分析两个函数，AskUserForMatrixData 和 ShowMatrix，用于读取并显示矩阵值。

AskUserForMatrixData 函数定义在列表 3.21 的第 3–18 行。在此，最好包含说明函数功能的信息，以及其参数的作用；在此情况下，几行注释即可。

**列表 3.21** 读取矩阵 m 的数值的 AskUserForMatrixData 函数定义（在 EasyMatrix，EMUtility.cpp 中）。

```cpp
// Ask the user to enter values for matrix m
// from the keyboard.
void AskUserForMatrixData( EMatrix & m )
{
    const Dim kCols = m.GetCols();
    const Dim kRows = m.GetRows();

    for( Dim r = 0; r < kRows; ++ r )
    {
        std::cout << "Enter data for row no. " << r << " of " << kRows << std::endl;
        for( Dim c = 0; c < kCols; ++ c )
        {
            std::cout << c << ": ";
            std::cin >> m.fData[ r ][ c ];  // read a value from the keyboard
        }
        std::cout << std::endl;  // new line again
    }
}
```

第 5–6 行读取输入对象 m 的列数和行数，并将它们存储在两个常量 kCols 和 kRows 中，这两个常量将在访问 m 的元素时作为边界使用。Dim 是一种用于索引向量和矩阵元素的类型，如列表 3.4 所声明。

由于矩阵是二维的，要访问其元素需要两个循环，分别遍历行和列。为此，第一个遍历矩阵行的循环在第 8 行开始。第 9–16 行的所有语句都在循环变量（迭代器） r 取 0 到 kRows − 1 的值时重复执行。每次迭代后，r 通过 ++ r 增加 1。第 10 行，我们向用户显示即将输入的行号的提示信息。

第二个嵌套循环在第 11 行开始。它在 12–15 行的花括号内执行两个操作。首先，第 13 行打印表示列号的文本。然后，第 14 行等待从键盘读取输入。用户输入的值被赋给矩阵元素位置 r, c。通过一系列调用实现：首先，m.fData 找到 fData……**（此处原文截断，但根据上下文可推断）**

要对两个矩阵求和，它们的维度必须相同；此条件通过 assert 验证。若维度相同，则在第 9 行创建并立即初始化输出矩阵 c，使用第一个矩阵 a 的数据。这可能因为编译器会假设只需复制 c.fData 成员即可从 a.fData 复制。此外，由于这些是 std::vector 对象，它们知道如何相互复制，因此此操作会自动完成。这解释了代码内部的行为，尽管关于复制和移动构造函数的详细说明将在 4.4 节中留待。

**列表 3.22** 基本矩阵操作函数定义（在 EasyMatrix，EMUtility.cpp 中）。

1    // Add two matrices, return the result:
2    // c = a + b
3    // Dimensions of a and b must be the same.
4    EMatrix AddMatrix( const EMatrix & a, const EMatrix & b )
5    {
6        assert( a.GetRows() == b.GetRows() );    // dim must be the same
7        assert( a.GetCols() == b.GetCols() );
8
9        EMatrix c { a };    // Make c the same as a
10
11        for( Dim row = 0; row < b.GetRows(); ++ row )
12            for( Dim col = 0; col < b.GetCols(); ++ col )
13                c.fData[ row ][ col ] += b.fData[ row ][ col ];
14
15        return c;
16    }

将两个矩阵相加需要两个 for 循环，如第 11、12 行所示。这些循环与 AskUserForMatrixData 函数中完全相同地遍历 fData 的行和列。第 13 行，使用 += 运算符将 b 矩阵的元素加到 c 矩阵对应元素上。写法 x += y 等价于 x = x + y，如 GROUP 15 运算符（表 3.15）所说明。最后，c 在第 15 行返回。

让我们简要回顾一下矩阵乘法。下面考虑以下两个矩阵 A 和 B：

![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_161_0.png)

![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_161_1.png)

我们排列矩阵以表明矩阵乘法依赖于将第一个矩阵的每行与第二个矩阵的每列相乘——因此这些维度必须相同。对应元素相乘后相加，得到结果矩阵中对应位置的元素。例如，第一行第一列的乘积计算方式为：1 · 0 + 0 · 2.2 + (−5) · 3 = −15。

掌握这些知识后，我们准备编写列表 3.23 中的代码。矩阵乘法函数 MultMatrix 定义在第 20 行，它接受两个代表真实矩阵的 EMatrix 对象，通过常量引用 a 和 b 传递。与矩阵加法不同，矩阵乘法要求 a 的列数等于 b 的行数。在第 22–26 行，我们读取行数和列数，并通过 assert 检查维度是否匹配。随后，第 30 行创建返回矩阵 c 并显式初始化为 0.0（如果未提供，则默认使用 0）。

**列表 3.23** 矩阵乘法函数定义（EMUtility.cpp 部分）。

```cpp
// Multiply two matrices, return the result:
// c = a * b
// Dimensions of a and b must comply for multiplication
EMatrix      MultMatrix( const EMatrix & a, const EMatrix & b )
{
    const auto a_cols = a.GetCols();
    const auto a_rows = a.GetRows();

    const auto b_cols = b.GetCols();
    const auto b_rows = b.GetRows();

    assert( a_cols == b_rows );          // Dimensions must be the same

    EMatrix c( a_rows, b_cols, 0.0 );    // Output matrix has such dimensions

    for( Dim ar = 0; ar < a_rows; ++ ar )       // Traverse rows of a
        for( Dim bc = 0; bc < b_cols; ++ bc )   // Traverse cols of b
            for( Dim ac = 0; ac < a_cols; ++ ac ) // Traverse cols of a == rows of b
                c.fData[ ar ][ bc ] += a.fData[ ar ][ ac ] * b.fData[ ac ][ bc ];

    return c;
}
```

从前面的例子可知，矩阵乘法需要三个循环：第一个遍历 a 的行，第二个遍历 b 的列，第三个遍历 a 的列（其数量必须等于 b 的行数）。这些循环在第 32–34 行以 for 语句实现。第 35 行，将 a 与 b 对应元素的乘积之和累加到矩阵 c 的相应位置。

最后，第 37 行返回结果矩阵 c。此时 c 按值返回，可能会产生昂贵的对象复制开销。但得益于 4.6.4 节讨论的优化机制，这不应成为大问题。

# 3.15.5 组织项目文件并运行应用程序

前面的代码片段来源于本书的 *EasyMatrix* 项目（可从书籍项目网页获取，Cyanek 2018）。`EMatrix` 结构体的定义位于 *EMatrix.h* 头文件。矩阵操作位于 *EMUtility.h* 和 *EMUtility.cpp* 文件中，测试函数位于……**（此处原文截断）**

