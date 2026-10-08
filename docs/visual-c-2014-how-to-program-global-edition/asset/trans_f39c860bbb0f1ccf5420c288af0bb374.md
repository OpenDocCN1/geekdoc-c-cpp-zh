

# 第 7 章方法：深入探讨

## 软件工程观察 7.8

默认情况下，C# 不允许你选择是否按值或按引用传递任何参数。值类型按值传递。对象不会被传递到方法中；而是对象的引用被按值传递的。当方法接收到对象的引用时，该方法可以直接操作该对象，但引用值不能被更改以指向一个新的对象。

![](img/57baed2319be0bb1b5f98674846f2711_320_0.png)

## 7.18.2 演示 ref、out 和值参数

图 7.20 中的应用程序使用 ref 和 out 关键字来操作整数值。该类包含三个计算整数平方的方法。

```cs
// 图 7.20: ReferenceAndOutputParameters.cs
// 引用、输出和值参数。
using System;

class ReferenceAndOutputParameters
{
    // 使用引用、输出和值参数调用方法
    int y = 5; // 将 y 初始化为 5
    int z; // 声明 z，但不初始化它

    // 显示 y 和 z 的原始值
    Console.WriteLine($"Original value of y: {y}");
    Console.WriteLine($"Original value of z: uninitialized\n");

    // 按引用传递 y 和 z
    SquareRef(ref y); // 必须使用关键字 ref
    SquareOut(out z); // 必须使用关键字

    // 显示 y 和 z 在被方法修改后的值
    // 分别由 SquareRef 和 SquareOut 修改的
    Console.WriteLine($"Value of y after SquareRef: {y}");
    Console.WriteLine($"Value of z after SquareOut: {z}\n");

    Square(y);
    Square(z);

    // 显示 y 和 z 在被方法修改后的值
    // 以证明按值传递的参数不会被修改
    Console.WriteLine($"Value of y after Square: {y}");
    Console.WriteLine($"Value of z after Square: {z}");
}

// 使用引用参数来修改调用者的变量
static void SquareRef(ref int x)
{
    x = x * x;
}

// 使用输出参数为未初始化的变量赋值
static void SquareOut(out int x)
{
    x = 6; // 为调用者的变量赋值
    x = x * x; // 调用者变量的值平方
}

// 参数接收作为参数传递的值拷贝，
// 因此此方法无法修改调用者的变量
static void Square(int x)
{
    x = x * x;
}
```

图 7.20 引用、输出和值参数。（第 1 部分）

| 方法 | 说明 |
| :--- | :--- |
| `SquareRef(ref int x)` | 第 37–40 行：将参数 x 乘以自身，并将新值赋值给 x。因为参数声明为 ref，所以它会修改调用者中原始参数的值。 |
| `SquareOut(out int x)` | 第 44–48 行：将参数值 6 相乘并进行平方。参数声明为 out，这表示传递给此方法的参数不需要初始化。 |
| `Square(int x)` | 第 52–55 行：将参数 x 乘以自身，并将新值赋值给 x。当调用此方法时，参数的副本被传递给参数 x。因此，即使在方法中修改了 x，调用者中的原始值也不会被修改。 |

Original value of y: 5
Original value of z: uninitialized
Value of y after SquareRef: 25
Value of z after SquareOut: 36
Value of y after Square: 25
Value of z after Square: 36

## 7.18 按值和按引用传递参数

第 27–28 行使用 y 和 z 作为参数调用 Square。在这种情况下，两个值都是按值传递的——只有它们的副本被传递给 Square。结果是 y 和 z 的值保持为 25 和 36。第 32–33 行输出 y 和 z 的值，以显示它们没有被修改。

> **编程错误 7.14**: 方法调用中的 ref 和参数必须与方法声明中指定的 ref 和 out 参数匹配；否则，将发生编译错误。

## 7.19 总结

在本章中，我们讨论了静态方法和静态方法之间的区别，并展示了如何通过在方法名之前加上其所属的类名和成员访问运算符（.）来调用静态方法。你可能会发现 .NET Framework 类库提供了许多执行数学计算的方法。我们还讨论了类方法以及为什么 Main 被声明为静态的。

我们介绍了常用的框架类库命名空间。你学习了如何使用运算符 + 进行字符串拼接。你还学习了如何使用 `const` 关键字声明常量，以及如何使用 `enum` 定义常量集。我们演示了模拟技术和递归方法调用自身，使用了 `Random` 生成随机数。我们讨论了类中字段和局部变量的作用域。你学习了如何通过提供具有相同名称但不同签名的方法来重载类的方法。

我们展示了 C# 表达式体方法和仅包含返回语句的只读属性的简洁表示。我们讨论了递归方法调用自身，将大问题分解为更小的问题直到解决原始问题。你学习了值类型和引用类型在传递给方法时的区别，以及如何使用 ref 和 out 关键字按引用传递参数。

在第 8 章中，你将学习如何使用数组维护列表和表格。你将看到一个更优雅的掷 6000 万次骰子的应用程序实现，以及两个版本的 GradeBook 案例研究。你还将学习如何访问应用程序启动时传递给 Main 方法的命令行参数。

# 总结

### 7.1 引言

- 经验表明，开发大型应用程序的最佳方法是从简单的组件构建它。这种技术被称为分治法。

### 7.2 在 C# 中封装代码

- 三种常见的封装方式是方法、类和命名空间。

### 7.2.1 程序模块化

- 方法允许通过将任务分离到自包含单元来实现程序的模块化。
- 将程序拆分为有意义的方法有助于调试。

### 7.3 static 方法、变量和类

- 你可以通过指定所属类的名称，加上成员访问运算符（.）来调用任何静态方法，格式如 `ClassName.MethodName(arguments)`。

### 7.3.2 类常量

- 常量用 `const` 关键字声明；语句后其值无法更改。
- Math.PI (3.141592653589793) 是圆周与直径的比。
- Math.E (2.718281828459045) 是自然对数的底数。

### 7.3.4 关于 Main 的补充说明

- 如果你在项目的多个类中声明了多个方法，你需要指定哪一个是入口点。你可以通过点击菜单 项目 > [ProjectName] 属性... 并在启动对象列表中选择包含 Main 方法的类来实现。

