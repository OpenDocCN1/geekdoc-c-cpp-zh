
```
Console.Write("Hours: ");
inputValue = Console.ReadLine();
hrs = int.Parse(inputValue);
Console.Write("Minutes: ");
inputValue = Console.ReadLine();
mins = int.Parse(inputValue);
}
public static double CalculateDistance(double numberOfStepsPerMin,
                                       int totalMinutes)
{
    const double STRIDE = 2.5;
    const int FEET_PER_MILE = 5280;

    return numberOfStepsPerMin * STRIDE * totalMinutes /
           FEET_PER_MILE;
}
public static void DisplayResults(double numberOfStepsPerMin,
                                  int hrs, int mins,
                                  double distanceTraveled)
{
    Console.Clear();
    Console.WriteLine("{0,35}", "Jogging Distance " +
                      "Calculator");
    Console.WriteLine();
    Console.WriteLine("{0,-25} {1} Feet Per Step",
                      "Stride:", 2.5);
    Console.WriteLine("{0,-25} {1} Steps", "Strides Per " +
                      "Minute: ", numberOfStepsPerMin);
    Console.WriteLine("{0,-25} {1} Hour(s) and {2} Minute(s)",
                      "Jogging Time:", hrs, mins);
    Console.WriteLine("{0,-25} {1:F2} Miles", "Distance " +
                      "Traveled:", distanceTraveled);
}
}
}
}
```

**实现代码** 编译源代码。如果你有任何规则违规，请进行修正，直到没有错误为止。运行应用程序，输入前面指示的值（185, 120, 1, 12）。

![](img/e33ae760e23d89eac66541252ad65de8_205_0.png)

## 测试与调试

在这个最后步骤中，测试程序并确保得到正确的结果。测试值的输出应与你的原型一致。图 3-15 显示了前面源代码生成的输出。

## 编码标准

建立并遵循良好的编码标准很重要。创建一组编码标准的目的是提供一份可接受的指南列表，供团队所有成员遵循。以下标准列表是与方法相关的建议。

### 命名约定

- 方法标识符使用 Pascal 命名法（所有单词的首字符大写；所有其他字符小写）。
- 局部变量标识符和参数使用 Camel 命名法（除第一个单词外，所有单词的首字符大写；所有其他字符小写）。
- 使用动词或动作短语来命名方法。不要使用误导性的名称。方法名应说明该方法做什么。如果你选择了好的方法名，就不需要额外文档来解释该方法做什么。

### 间距约定

- 将花括号（ { } ）与方法标头对齐。
- 每个局部变量都在单独的行上独立声明。可以重复使用数据类型，但每个变量应位于单独的行上。
- 类中每个方法之间应有一个且只有一个空行。
- 避免编写过长的方法。当方法超过 25 行代码时，考虑重构。
- 避免源代码文件过大。当单个类中的文件大小超过 300–400 行时，考虑重构。

### 声明约定

- 单个文件中不要有多个类。
- 在使用局部变量的方法中声明并初始化这些变量。
- 尽量在声明变量时初始化它们。
- 避免向方法传递过多参数。如果参数超过 4–5 个，最好定义一个类或结构。
- 一个方法应只做一件事：只有一个主题。
- 返回类型不是 `void` 的方法应从能够接受返回值的程序语句中调用（即赋值语句或输出语句）。
- 方法应只有一个入口和一个出口。

### 注释约定

- 良好、可读的代码只需要很少的注释。如果使用有意义的变量名和方法名，就不需要很多注释。
- 在方法中包含注释，以解释可能无法完全理解的复杂或令人困惑的逻辑。

## 资源

你可能想探索的其他网站：

- C# 开发者中心：http://www.csharp.net
- 代码库网站：http://code.msdn.com/csharpfuture

## 快速回顾

- 1. 方法是 `class` 的成员，用于描述数据的行为。
- 2. 控制台应用程序和 Windows 应用程序都需要 `Main( )` 方法。
- 3. `Main( )` 应包含 `static` 关键字。
- 4. 方法的标头可以由修饰符、`return` 类型、方法标识符和参数组成。方法体包含在花括号中。
- 5. 当方法包含 `static` 修饰符时，它就成为 `class` 方法。
- 6. `return` 类型标识方法完成时返回的值的类型。可以返回任何预定义类型或有效的用户定义类型。
- 7. `void` 关键字指定该方法不 `return` 值。
- 8. 许多程序员采用使用动作动词短语命名方法的标准约定。
- 9. 形式参数出现在方法的标头中。实际参数出现在调用中。实际参数是发送给方法的实际数据。
- 10. 方法的签名由方法名、修饰符及其形式参数的类型组成。它不包括 `return` 类型。
- 11. `ReadLine( )` 方法返回直到当前行尾终止符（Enter 键）之前的所有字符。它返回一个 `string`，在值可用于算术运算之前，必须将其解析为数字。
- 12. 在 `Main( )` 方法和其他方法中声明的变量被视为局部变量，并且只能在其声明所在的方法体内可见。
- 13. 如果从方法返回值，例如通过表达式或输出语句返回值，那么方法完成时必须有一个可以接受该值的位置。调用实际上可以出现在可放置该类型兼容值的任何位置。
- 14. 要调用无返回值方法，只需键入方法名。如果方法有参数，则调用中在括号内包含实际参数，但不包含类型。
- 15. C# 同时提供按值调用和按引用调用。如果标头中未添加关键字，则默认按值调用。通过使用 `ref` 和 `out` 关键字可以实现按引用调用。它们必须同时出现在标头和调用中。`ref` 要求实参在传递之前已初始化。
- 16. 命名实参使你能够使用参数名而不是参数顺序来传入值。
- 17. 当你为参数分配默认值时，它就成为可选参数。

## 练习

- 1. 其他语言中的函数或模块类似于 C# 中的 ______________。

  - a. 修饰符
  - b. 参数
  - c. 实参
  - d. 方法
  - e. 类

- 2. 以下哪一项放在方法标头中，表示不会返回任何值？

  - a. `public`
  - b. `static`
  - c. 参数
  - d. `void`
  - e. `return`

- 3. 以下哪个修饰符限制性最强？

  - a. `private`
  - b. `static`
  - c. `public`
  - d. `internal`
  - e. `protected`

- 4. 以下哪个标识符遵循方法的标准命名约定？

  - a. Calculate Final Grade
  - b. MilesPerGallon
  - c. InValueMethod
  - d. PrintReport
  - e. Method1

- 5. 以下哪种是调用 `Math` 类中预定义 `Floor( )` 方法最合适的方式？
`public static double Floor(double)`

  - a. `answer = Floor(87.2);`
  - b. `answer = Math.Floor(87.2);`
  - c. `Floor(87.2);`
  - d. `Math.Floor(double);`
  - e. `Math.Floor(87.2);`

- 6. 给定以下语句，`DetermineAnswer( )` 方法的最佳标头是什么？

```
int aValue,
    result;
result = DetermineAnswer(27.83, aValue);
```

  - a. `public void DetermineAnswer(27.83, aValue)`
  - b. `public int DetermineAnswer( )`
  - c. `public int DetermineAnswer(double v1, int v2)`
  - d. `public double int DetermineAnswer( )`
  - e. `public void DetermineAnswer(double v1, int v2)`

- 7. 完成被调用方法的方法体后，控制权会返回：

  - a. 返回到调用方法中发起调用的位置
  - b. 返回到发起调用的方法中的最后一条语句
  - c. 返回到发起调用的方法中的第一条语句
  - d. 返回到 `Main( )` 方法
  - e. 返回到打印源代码中列出的下一个方法

- 8. 以下哪一项是 `DetermineHighestScore` 的有效方法调用？

```
void DetermineHighestScore(int val1, int val2)
```

  - a. `void DetermineHighestScore(int val1, int val2)`
  - b. `DetermineScore(int val1, int val2)`
  - c. `DetermineHighestScore(val1, val2)`
  - d. `DetermineHighestScore(2, 3.5)`
  - e. `GetHighestScore( )`

- 9. 以下方法的签名是什么？

```
public void SetNoOfSquareYards(double squareYards)
{
    noOfSquareYards = squareYards;
}
```

  - a. `public void SetNoOfSquareYards(double squareYards)`
  - b. `public SetNoOfSquareYards(double squareYards)`
  - c. `SetNoOfSquareYards`
  - d. `public SetNoOfSquareYards(double)`
  - e. `SetNoOfSquareYards(double)`

