
输入成绩，因此控制流转向 `while` 的条件（第24行），以根据刚刚赋给变量 *input* 的值判断循环是否应继续执行。

### *连续的* `case` 标签

`switch` 的 case 显式测试值 10、9、8、7 和 6。第33–34行测试值 9 和 10（两者都表示成绩 A）。以这种方式连续列出 case 标签且它们之间没有语句，可使这些 case 执行同一组语句——当 `switch` 表达式的求值为 9 或 10 时，第35–36行的语句执行。`switch` 语句不提供测试值范围的机制，因此每个要测试的值都必须列在单独的 case 标签中。每个 case 可以有多个语句。`switch` 语句与其他控制语句的不同之处在于，它*不*要求在每个 case 中的多个语句周围加大括号。

### *该* `default` *分支*

如果 `switch` 表达式的值与某个 `case` 标签之间*没有匹配*，则执行 `default` 标签之后的语句（第47–48行）。在此示例中，我们使用 `default` 标签处理所有小于 6 的 `switch` 表达式值——即所有不及格成绩。如果没有匹配发生，并且 `switch` *不*包含 `default` 标签，则程序控制直接继续执行 `switch` 语句之后的第一个语句（如果有的话）。

> **良好编程习惯 6.1**
> *尽管 `switch` 中的每个 `case` 和 `default` 标签可以按任意顺序出现，但为了清晰起见，请将 `default` 标签放在最后。*

### *C# 的* `switch` *语句中没有“穿透”*

在许多其他包含 `switch` 的编程语言中，case 末尾的 **break 语句** *不是必需的*。在这些语言中，如果没有 break 语句，则每当 `switch` 中发生匹配时，该 case 及后续 case 的语句都会执行，直到遇到 break 语句或 `switch` 结束。这通常称为“穿透”到后续 case 的语句。当你忘记 break 语句时，这会导致逻辑错误。C# 与其他编程语言不同——在 case 中的语句之后，你*必须*包含一个终止该 case 的语句，例如 `break`、`return` 或 `throw`；¹ 否则会发生编译错误。²

### *显示成绩报告*

第54–76行根据输入的成绩输出报告（如图6.9中的输入/输出窗口所示）。第57行判断用户是否至少输入了一个成绩——这有助于避免除以零。如果是，第60行计算这些成绩的平均值。然后第63–71行输出所有成绩的总分、班级平均分以及获得每个字母等级的学生人数。如果未输入任何成绩，第75行输出相应的消息。图6.9中的输出显示了基于10个成绩的示例成绩报告。

1. 我们在第13章“异常处理：深入探讨”中讨论 `throw` 语句。
2. 你可以通过将 case 或 default 的动作之后的 break 语句替换为如下形式的语句来实现穿透：`goto case` *value*;（其中 *value* 是 switch 的某个 case 中的字面量或常量）或 `goto default`;。

### 6.7.2 switch 语句 UML 活动图

图6.10显示了通用 switch 语句的 UML 活动图。case 标签之后的每组语句通常以 break 或 return 语句结束执行，以便在处理完该 case 后终止 switch 语句。通常，你会使用 break 语句。图6.10通过在活动图中包含 break 语句来强调这一点。该图清楚地表明，case 末尾的 break 语句会使控制立即退出 switch 语句。

![](img/3f5ef6be1748bb746e5f71c483bba4d0_173_0.png)

**图 6.10** | 带 break 语句的 switch 多选择语句 UML 活动图。

### 6.7.3 关于 switch 每个 case 中表达式的说明

在 switch 语句的 case 中，常量整型表达式可以是字符常量——单引号中的特定字符，例如 'A'、'7' 或 '$'——它们表示字符的整数值。（附录显示了 ASCII 字符集中字符的整数值，ASCII 字符集是 C# 使用的 Unicode 字符集的一个常用子集。）字符串常量（或字符串字面量）是双引号中的字符序列，例如 "Welcome to C# Programming!"，或者是 const string 变量。对于字符串，你也可以使用 null 或 string.Empty。

每个 case 中的表达式也可以是常量——一个在整个应用期间不会改变的值。常量使用关键字 `const` 声明（在第7章讨论）。C# 还有一个称为*枚举*的特性，我们也会在第7章介绍。枚举常量也可以用在 case 标签中。在第12章中，我们介绍一种更优雅的实现 switch 逻辑的方式——我们使用一种称为*多态*的技术来创建应用，这些应用通常比使用 switch 逻辑的应用更清晰、更易于维护且更易于扩展。

## 6.8 AutoPolicy 类案例研究：switch 语句中的字符串

`strings` 可用于 `switch` 表达式中，`string` 字面量可用于 `case` 标签中。为了演示这一点，我们将实现一个满足以下要求的应用：

> *你受雇于一家汽车保险公司，该公司服务于这些东北部州——康涅狄格州、缅因州、马萨诸塞州、新罕布什尔州、新泽西州、纽约州、宾夕法尼亚州、罗得岛州和佛蒙特州。公司希望你创建一个程序，生成一份报告，针对其每份汽车保险单，指出该保单是否位于提供“无过错”汽车保险的州——马萨诸塞州、新泽西州、纽约州和宾夕法尼亚州。*

该应用包含两个类——`AutoPolicy`（图6.11）和 `AutoPolicyTest`（图6.12）。

**类 AutoPolicy**

`Class AutoPolicy`（图6.11）表示一份汽车保险单。该类包含：
- 自动实现的 `int` 属性 `AccountNumber`（第5行），用于存储保单的账号，
- 自动实现的 `string` 属性 `MakeAndModel`（第6行），用于存储汽车的品牌和型号（例如“Toyota Camry”），
- 自动实现的 `string` 属性 `State`（第7行），用于存储表示保单所在州的两个字符的州缩写（例如，马萨诸塞州的“MA”），
- 一个构造函数（第10–15行），用于初始化该类的属性，以及
- 只读属性 `IsNoFaultState`（第18–37行），返回一个 `bool` 值，指示该保单是否位于无过错汽车保险州；请注意属性名——`bool` 属性的常见命名约定是以“Is”开头。

在属性 `IsNoFaultState` 中，`switch` 表达式（第25行）是 `AutoPolicy` 的 `State` 属性返回的 `string`。`switch` 语句将 `switch` 表达式的值与 `case` 标签（第27行）进行比较，以确定该保单是否位于马萨诸塞州、新泽西州、纽约州或宾夕法尼亚州（这些是无过错州）。如果有匹配，则第28行将局部变量 `noFaultState` 设置为 `true`，并且 `switch` 语句终止；否则，`default` case 将 `noFaultState` 设置为 `false`（第31行）。然后，`IsNoFaultState` 的 `get` 访问器返回局部变量 `noFaultState` 的值。

```
// Fig. 6.11: AutoPolicy.cs
// Class that represents an auto insurance policy.
class AutoPolicy
{
    public int AccountNumber { get; set; } // policy account number
    public string MakeAndModel { get; set; } // car that policy applies to
    public string State { get; set; } // two-letter state abbreviation

    // constructor
    public AutoPolicy(int accountNumber, string makeAndModel, string state)
    {
        AccountNumber = accountNumber;
        MakeAndModel = makeAndModel;
        State = state;
    }

    // returns whether the state has no-fault insurance
    public bool IsNoFaultState
    {
        get
        {
            bool noFaultState;

            // determine whether state has no-fault auto insurance
            switch (State) // get AutoPolicy object's state abbreviation
            {
                case "MA": case "NJ": case "NY": case "PA":
                    noFaultState = true;
                    break;
                default:
                    noFaultState = false;
                    break;
            }

            return noFaultState;
        }
    }
}
```

**图 6.11** | 表示汽车保险单的类。

为简单起见，我们不验证 AutoPolicy 的属性，并假设州缩写始终是两个大写字母。此外，真实的 AutoPolicy 类可能还会包含许多其他属性和方法，用于处理账户持有人的姓名、地址、出生日期等数据。

### 类 AutoPolicyTest

类 AutoPolicyTest（图6.12）创建两个 AutoPolicy 对象（Main 中的第10–11行）。第14-15行将每个对象传递给静态方法 policyInNoFaultState（第20-28行），该方法使用 AutoPolicy 的方法来确定并显示它接收的对象是否表示一份位于无过错汽车保险州的保单。

