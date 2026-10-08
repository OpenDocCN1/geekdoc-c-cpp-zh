

# 284 第 7 章 方法：深层观察

```cs
// 提示并输入三个浮点数值
Console.Write("Enter first floating-point value: ");
double number1 = double.Parse(Console.ReadLine());
Console.Write("Enter second floating-point value: ");
double number2 = double.Parse(Console.ReadLine());
Console.Write("Enter third floating-point value: ");
double number3 = double.Parse(Console.ReadLine());

// 确定三个值中的最大值
double result = Maximum(number1, number2, number3);

// 显示最大值
Console.WriteLine("Maximum is: " + result);

// 返回三个参数中的最大值
static double Maximum(double x, double y, double z)
{
    double maximumValue = x; // 假设 x 是最大的

    // 确定 y 是否大于 maximumValue
    if (y > maximumValue)
    {
        maximumValue = y;
    }
    // 确定 z 是否大于 maximumValue
    if (z > maximumValue)
    {
        maximumValue = z;
    }
    return maximumValue;
}
```

Enter first floating-point values: 3.33
Enter second floating-point values: 1.11
Enter third floating-point values: 2.22
Maximum is: 3.33

Enter first floating-point values: 2.22
Enter second floating-point values: 3.33
Enter third floating-point values: 1.11
Maximum is: 3.33

Enter first floating-point values: 2.22
Enter second floating-point values: 1.11
Enter third floating-point values: 3.33
Maximum is: 3.33

**图 7.3** | 带有三个参数的方法 Maximum。（2 部分之 2）。

## 7.4 多参数方法

### 7.4.1 关键字 static

方法 Maximum 的声明以关键字 `static` 开始，这使得 Main 方法（或静态方法）可以如第 19 行所示调用 Maximum，而无需创建 `MaximumFinder` 类的对象，无需使用类名 `MaximumFinder` 来限定方法名——同一类中的静态方法可以互相调用。

### 7.4.2 方法 Maximum

考虑方法 Maximum 的声明（第 26–43 行）。第 26 行表示该方法返回一个 `double` 值，并且该方法需要三个 `double` 参数（x、y 和 z）来完成任务。当一个方法有多个参数时，这些参数以逗号分隔的列表形式指定。在第 19 行调用 Maximum 时，参数 `x` 初始化为参数 `number1` 的值，参数 `y` 初始化为参数 `number2` 的值，参数 `z` 初始化为参数 `number3` 的值。对于方法声明中的每次调用，方法中必须有一个参数。每个参数都必须与对应参数的类型一致。例如，`double` 类型的参数可以接收如 7.35 (double)、2 (int) 或 0.34 (double) 这样的值，但不能接收像 "hello" 这样的字符串。第 7.6 节讨论了为简单类型的每个参数在方法调用中可以提供的参数类型。注意在方法 12、14 和 16 中使用了 `double` 的 `Parse` 来将用户使用的字符串转换为 `double` 值。

**常见编程错误 7.2**：将参数声明为与 `x` 相同的类型而不是 `double y` 是一个语法错误——参数列表中的每个参数都需要指定类型。（img/57baed2319be0bb1f5986746271）

### 确定最大值的逻辑

为了确定最大值，我们首先假设参数 `x` 包含最大值，因此第 28 行声明了局部变量 `maximum` 并将其初始化为参数 `x` 的值。`y` 或 `z` 可能包含最大值，因此我们将这些值中的每一个与 `maximum` 进行比较。第 31–34 行的 `if` 语句确定 `y` 是否大于 `maximum`。如果是，第 33 行将 `y` 赋值给 `maximum`。第 37–40 行的语句确定 `z` 是否大于 `maximum`。此时，三个值中最大的存储在 `maximum` 中，因此第 42 行返回到第 19 行赋值给变量 `result`。当程序控制返回到调用 Maximum 的应用程序时，方法最多返回一个值；返回的值可以是包含一个或多个值的类型（实现为 `struct`；第 10.1 节）。

### 7.4.3 使用拼接组合字符串

C 语言允许通过使用运算符 `+`（或复合赋值运算符 `+=`）将较小的字符串组装成较大的字符串。这被称为字符串拼接。当运算符 `+` 的操作数是字符串对象时，`+` 运算符会新的字符串对象，其中包含左操作数字符的拷贝，随后是右操作数字符的拷贝。例如，表达式 `"hello " + "there"` 会创建字符串 `"hello there"` 而不干扰原始字符串。

在第 22 行，表达式 `"Maximum is: " + result` 使用了 `string` 和 `double` 类型的 `+` 运算符。每个简单值都有一个 `ToString` 表示。当 `+` 的操作数之一是字符串时，它会被隐式转换为字符串，然后拼接两个字符串。在第 22 行中，`double` 值被转换为其字符串表示并放置在 `"Maximum is: "` 的末尾。如果 `double` 值中有任何尾随零，它们会被丢弃。因此，9.3500 的字符串表示是 `"9.35"`。

### 任何内容都可以转换为字符串

当 `+` 的操作数之一是字符串时，它会被隐式转换为字符串，然后拼接两个字符串。在第 22 行中，`double` 值被转换为其字符串表示并放置在 `"Maximum is: "` 的末尾。如果 `double` 值中有任何尾随零，它们会被丢弃。因此，9.3500 的字符串表示是 `"9.35"`。 (注：此处原文处似乎存在文本重复或逻辑乱码，翻译已根据语意进行处理)

### 使用插值格式化字符串

为了格式化字符串，可以使用字符串插值，如上文所示：

```cs
Console.WriteLine($"Maximum is: {result}");
```

### 7.4.4 换行长字符串

当方法返回控制时，方法最多返回一个值；返回的值可以是包含一个或多个值的类型（实现为 `struct`；第 10.1 节）。

### 7.4.5 声明为字段

变量只有在方法方法中使用时才声明为字段。

### 7.4.6 通过复用方法实现 Maximum

从图 7.2 回忆，`Math.Max` 方法可以确定两个值。我们方法的整个主体可以使用嵌套调用 `Math.Max` 来实现，如下：

```cs
return Math.Max(x, Math.Max(y, z));
```

调用任何方法之前，运行时会评估所有参数以确定它们的值。如果参数是方法调用，则必须执行该调用以确定其返回值。因此，在上述语句中，首先执行 `Math.Max(y, z)` 以确定 y 和 z 的较大值，然后将其结果作为第二个参数传递给第一个 `Math.Max`。这种方式使用 `Math.Max` 是软件复用的良好示例——我们通过复用寻找两个值的方法来找到三个值的最大值。代码比图 7.3 第 28–42 行简洁。

## 7.5 使用方法的注意事项

### 调用方法的方法

你已经看到了三种调用方法的方法：

- 使用方法名调用同一类中的方法——如图 7.3 第 19 行所示，从 `Main` 方法调用 `Maximum(number1,number2,number3)`。
- 使用对象的引用、后跟成员访问运算符 `.` 以及方法名来调用所引用对象的非静态方法——如图 4.12 第 23 行所示，从 `AccountTest` 类的 `Main` 方法调用 `account1.Deposit(depositAmount)`。
- 使用类名和成员访问运算符 `.` 来调用类的类的静态方法——如图 7.3 第 12–14 行所示，每次都调用 `Console.ReadLine()`，或如第 7.3 节中的 `Math.Sqrt(900.0)`。

### 从方法返回的方法

你已经看到了三种返回控制到调用方法的语句的方法：

- 在返回类型为 `void` 的方法到达方法结束的大括号。
- 当以下语句在返回类型为 `void` 的方法执行时：

```cs
return;
```

- 当方法通过如下形式的语句返回结果，其中表达式被求值并将其结果（以及控制）返回给调用者时：

```cs
return expression;
```
