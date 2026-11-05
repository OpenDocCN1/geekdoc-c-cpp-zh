
```
public static void TestRef(ref int aValue)
{
    aValue = 333;
    Console.WriteLine("Inside TestRef -"
                      + "Value: "
                      + "{0}", aValue);
}

public static void TestDefault(int aValue)
{
    aValue = 111;
    Console.WriteLine("In TestDefault -"
                      + "Value: "
                      + "{0}", aValue);
}

public static void TestOut(out int aValue)
{
    aValue = 222;
    Console.WriteLine("In TestOut - "
                      + "Value: "
                      + " {0}", aValue);
}
}
```

图3-8所示的输出说明了值参数是如何保持不变的。它们在调用方法中保留原始值。这是因为实际上是对原始值进行了复制。当返回调用方法时，原始的保留值仍然可见。

使用 `ref` 和 `out` 发送的参数在控制权返回调用方法时会被更改。`out` 参数在调用前不必初始化；但是，在方法返回之前，必须为 `out` 参数赋值。C# 不允许使用未初始化的变量。

**图 3-8** ParameterClass 示例的输出

![](img/36e48639a06772bcb0fa1ea2525b33a3_207_0.png)

图3-9以图形方式说明了按值调用和按引用调用之间的区别。它还提醒我们注意一个事实：out 参数类型在调用前不必初始化。请注意，此图使用了示例3-18中的程序语句。

![](img/36e48639a06772bcb0fa1ea2525b33a3_207_1.png)

**图 3-9** 按引用调用与按值调用

参数，而不是在调用方法时需要担心哪个参数放在哪里的精确顺序。你还可以为参数分配默认值，这样在调用方法时，除非值不同于相关的默认值，否则无需发送值。尽管这些功能可能应该谨慎使用，但它们是该语言不错的补充，将在接下来的章节中讨论。

## 使用可选参数的默认值

当你为参数分配默认值时，它就成了可选参数。每次调用方法时不必发送值。相反，如果没有发送值作为参数，则使用默认值。一个方法可以有多个可选参数。但是，如果有多个可选参数，则必须将它们放在参数列表的最后，即任何必需参数之后。示例 3-19 演示了带有默认值的可选参数。

### 示例 3.19

```
public static void DoSomething(string name, int age = 21,
    bool currentStudent = true,
    string major = "CS")
{
    // additional program statements go here
}
```

现在你可以调用 DoSomething( ) 并为默认值传入参数，否则默认值将赋给参数。示例 3-20 展示了对 DoSomething( ) 方法的有效调用。

### 示例 3.20

```
DoSomething ("Elizabeth Abbott", 20);
DoSomething ("James Gabriel");
DoSomething ("Jonathan Byrle", 25, false, "MS");
```

默认值必须是常量。如果没有为特定参数发送参数，则使用默认值。使用可选参数的一个限制是，如果需要为任何可选参数发送参数，则必须为所有前面的可选参数提供参数。因此，调用 DoSomething ("Gabriella Henson", "MS"); 是无效调用，但 DoSomething ("Joe Smith", 20, false); 是有效调用。注意，虽然不需要为 major 发送值，但如果你需要为 currentStudent 发送布尔值，则必须为所有前面的参数发送值。在这种情况下，你必须为可选参数 age 发送值。

## 命名参数

命名参数使您无需记住或查找方法调用的参数顺序。每个参数的参数都可以使用参数名后跟冒号 ( : ) 然后是所赋参数值来指定。命名参数还有一个附加功能，即可以按任意顺序将参数发送到方法中。示例 3-21 展示了使用命名参数对 DoSomething( ) 的调用。

### 示例 3.21

```
DoSomething (name: "Robert Wiser", age: 20);

DoSomething (name: "Paul Nelson", major: "BIO");

DoSomething (name: "Fredrick Terrell", age: 25, major: "MS");
```

你会注意到，可选参数和命名参数在一起使用非常有用。只要参数有默认值，在使用命名参数时就可以省略它。你可以只为你想要赋予新值的参数提供值。

> **注意** 可选参数在 Visual Basic 中已经存在相当长一段时间了。随着 C# 4.0 的引入，开发人员可以在 C# 中使用此功能，并且也能够使用命名参数。

可选参数使您能够在方法调用中省略参数，而命名参数允许您按名称而不是按位置指定参数。

## 编程示例：JoggingDistance

此示例演示了程序中方法的使用。问题规范如图 3-11 所示。

![](img/36e48639a06772bcb0fa1ea2525b33a3_211_0.png)

**图 3-11** JoggingDistance 示例的问题规范

### 分析问题

您应该查看图 3-11 中的问题规范，并确保理解问题定义。程序中必须输入多个值。这些值必须作为*字符串*变量输入，然后解析为数值字段，以便执行算术运算。

### 变量

**表 3-3** JoggingDistance 类的变量

| 数据项描述 | 类型 | 标识符 |
|---|---|---|
| 第一分钟内的步幅数 | int | initialStrideCount |
| 最后一分钟内的步幅数 | int | finalStrideCount |
| 慢跑时间 | int | hrs, mins, totalMinutes |
| 每分钟平均步幅数 | double | numberOfStepsPerMin |
| 总行进距离 | double | distanceTraveled |

### 常量

步幅（每步英尺数）被设置为常量值。标识符和预设常量值为 STRIDE = 2.5。

每英里的英尺数也被设置为常量。

```
FEET_PER_MILE = 5280;
```

### 设计方案

所需的输出是显示给定慢跑时段所行进的距离（以英里为单位）。图 3-12 显示了所需最终输出的原型。xxx.xx 放在原型中，表示计算值应出现的位置。

![](img/36e48639a06772bcb0fa1ea2525b33a3_213_0.png)

**图 3-12** 原型

面向对象的方法更侧重于对象。类图用于帮助设计和记录这些特征。图 3-13 显示了 JoggingDistance 示例的类图。

![](img/36e48639a06772bcb0fa1ea2525b33a3_213_1.png)

**图 3-13** 类图

在设计过程中，重要的是开发算法，显示解决问题的分步过程。结构化英语，也称为伪代码，适用于面向对象的方法。除了 Main( ) 方法之外，还需要设计七个额外的方法。图 3-14 显示了 JoggingDistance 示例的结构化英语设计。

```
Main()
DisplayInstructions()
set initialStrideCount = GetNumberStrides("first")
set finalStrideCount = GetNumberStrides("last")
InputJoggingTime(out int hrs, out int mins)
set totalMinutes = CalculateTime(hrs, mins)
set numberOfStepsPerMin = CalculateAvgSteps(initialStrideCount, finalStrideCount)
set distanceTraveled = CalculateDistance(numberOfStepsPerMin, totalMinutes)
DisplayResults()

DisplayInstructions()
Write message indicating what program will do
Write message alerting user to what values will be entered

Int GetNumberStrides(string when)
Write prompt to enter numberOfSteps using when argument
Read numberOfSteps into string inValue
numberOfSteps = parse(inValue)
return numberOfSteps

InputJoggingTime(out int hrs, out int mins)
Write prompt to enter hrs
Read hrs into string inValue
hrs = parse(inValue)
Write prompt to enter mins
Read mins into string inValue
mins = parse(inValue)

double CalculateAvgSteps(int initialStrideCount, int finalStrideCount)
return (initialStrideCount + finalStrideCount) / 2.0

int CalculateTime(int hrs, int mins)
return hrs * 60 + mins

double CalculateDistance(double numberOfStepsPerMin, int totalMinutes)
return numberOfStepsPerMin * 2.5 * totalMinutes / 5280

DisplayResults()
Write averageStride
Write joggingTime
Write distanceTraveled
```

**图 3-14** JoggingDistance 示例的结构化英语

这些方法展示了 void 和值返回操作。注意，DisplayInstructions( )、InputJoggingTime( ) 和 DisplayResults( ) 都是非值返回方法。在实现解决方案时，关键字 void 出现在它们的方法头中。这些方法的主体中没有 return 语句。当这些方法的语句执行完毕时，控制权返回到调用这些方法的 Main( ) 方法。
