

# 21.9 Lambda 表达式

```c
// Fig. 21.7: Lambdas.cs
// 使用 lambda 表达式。
using System;
using System.Collections.Generic;

class Lambdas{
    // 接收一个 int 并返回 bool 的函数的委托
    public delegate bool NumberPredicate(int number);

    static void Main(string[] args)
    {
        int[] numbers = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

        // 使用隐式 lambda 表达式创建 NumberPredicate 委托的实例
        NumberPredicate evenPredicate = number => number % 2 == 0;

        // 通过变量调用 lambda 表达式
        Console.WriteLine($"Use a lambda-expression variable: {evenPredicate(4)}");

        List<int> evenNumbers = FilterArray(numbers, evenPredicate);

        // 显示结果
        DisplayList("Use a lambda expression to filter even numbers: ", evenNumbers);

        // 使用显式类型指定的 lambda 过滤奇数
        List<int> oddNumbers = FilterArray(numbers, (int number) => number % 2 == 1);

        // 显示结果
        DisplayList("Use a lambda expression to filter odd numbers: ", oddNumbers);

        // 使用隐式 lambda 语句过滤大于 5 的数字
        List<int> over5 = FilterArray(numbers, number => {return number > 5});

        // 显示结果
        DisplayList("Use a lambda expression to filter numbers over 5: ", over5);
    }

    // 选择数组中满足谓词的元素
    private static List<int> FilterArray(
        int[] array, NumberPredicate predicate)
    {
        // 存储选定的元素
        var result = new List<int>();
        // 遍历数组中的每个元素
        foreach (var item in array)
        {
            // 如果元素满足谓词
            if (predicate(item))
            {
                result.Add(item); // 将元素添加到结果
            }
        }
        return result; // 返回结果
    }

    // 显示 List 的元素
    static void DisplayList(string description, List<int> list)
    {
        Console.WriteLine(description); // 显示输出的描述
        // 遍历 List 中的每个元素
        foreach (int item in list)
        {
            Console.Write($"{item}"); // 打印项目并跟随
        }
        Console.WriteLine(); // 换行
    }
}
```

Use a lambda-expression variable: True
Use a lambda expression to filter even numbers: 2 4 8 10
Use a lambda expression to filter odd numbers: 1 3 5 7 9
Use a lambda expression to filter numbers over 5: 6 7 8 9 10

**图. 21.7** 使用 lambda 表达式。（部分 2/2）

## 第 21 章 泛型集合：使用 LINQ/PLINQ 进行函数式编程

### 21.9.1 表达式 Lambda

Lambda 表达式（第 17 行）

```c
number => number % 2 == 0
```

以参数列表（本例为 `number`）开始。参数列表后面是 `=>` lambda 运算符（读作 "goes to"）和一个代表 lambda 主体的表达式。第 17 行的 lambda 表达式使用 `%` 运算符来确定参数的值是否为偶数整数。表达式产生的值（如果是偶数则为 true，否则为 false）由 lambda 表达式隐式返回。第 17 行的 lambda 被称为表达式 lambda，因为它在 lambda 运算符的右侧只有一个表达式。我们没有为 lambda 表达式指定类型——返回类型是从返回值或委托的返回类型推断出的。第 17 行的 lambda 表达式等同于图 21.6 中的 `IsEven` 方法。注意，C# 6 的表达式体方法使用了与表达式 lambda 类似的语法，包括 lambda 运算符（`=>`）。

## 21.10 函数式编程简介

### 21.9.2 将 Lambda 赋值给委托变量

在图 21.7 的第 17 行中，lambda 表达式被赋值给 `NumberPredicate` 类型的变量——这是第 9 行声明的委托类型。委托可以持有 lambda 表达式的引用。使用传统方法，由 lambda 表达式定义的方法签名必须与委托类型匹配。`NumberPredicate` 委托可以持有任何返回 `int` 和 `bool` 的方法的引用。基于此，编译器能够推断出第 17 行的 lambda 表达式接收一个 `int` 作为参数，并返回主体表达式的 `bool` 结果。

第 20–21 行显示调用第 17 行定义的 lambda 表达式的结果。该 lambda 通过引用它的变量（`evenPredicate`）调用。第 24 行将 `evenPredicate` 传递给方法 `FilterArray`（第 49–66 行），这与图 21.6 中的方法相同——它使用 `NumberPredicate` 委托来确定数组元素是否包含在结果中。第 27–28 行显示过滤后的结果。

### 21.9.3 显式类型 Lambda 参数

Lambda 表达式常用带有委托类型参数的方法，但在某些情况下，你可能需要显式指定参数类型：

```csharp
(int number) => number % 2 == 1
```

当编译器无法从上下文中推断类型或你为了清晰而想显式指定时，这非常有用。

### 21.9.4 语句 Lambda

语句 lambda 允许你使用代码块而不是单个表达式：

```csharp
number => {return number > 5}
```

当 lambda 使用语句块时，主体被包裹在大括号中，如果它返回一个值，则必须使用 `return` 关键字。

