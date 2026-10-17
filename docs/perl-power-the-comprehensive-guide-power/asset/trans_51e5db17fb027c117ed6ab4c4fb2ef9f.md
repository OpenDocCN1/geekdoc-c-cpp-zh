

| Term | Discussion |
|---|---|
| `for` | `for` 循环可以以多种方式设置。它可以使用由分号分隔的表达式，用于初始化、设置循环条件以及建立步进表达式。你可以选择在 `for` 语句中省略其中一个或全部表达式。即使其他内容都省略，你也必须始终在测试表达式中使用两个分号。`for` 语句位于块之前，并允许块中的语句或语句继续执行，只要其控制条件为真。如果你未设置任何条件，则会创建一个无限循环。 |
| loop controls | 如果你未设置任何条件来控制循环，则会创建一个无限循环。如果你的程序进入无限循环，你别无选择，只能通过使用操作系统来终止其执行。 |
| `next` | 如果你在循环内的任何位置放置 `next` 运算符，它会导致程序流程跳过循环中剩余的语句。然而，它不会完全跳出循环。相反，它会导致活动流程返回到控制点。你可以将标签与 `next` 运算符一起使用。要将 `next` 与标签一起使用，请在其后跟上标签的名称（通常为大写字母）。标签本身可以放置在控制点。你在标签后跟一个冒号（`LABEL:`）。 |
| `last` | 此运算符允许你完全退出循环。它还可以允许你以与 `next` 运算符相同的方式访问标签。 |
| `redo` | `redo` 运算符导致程序流程跳回到循环的开头，而不评估循环的控制表达式。结果是，即使控制表达式在正常评估时会导致循环终止，循环中的语句仍会执行。 |
| `continue` | `continue` 运算符是 break 的另一个版本。它导致程序流程立即退出循环。程序流程从循环的右花括号之后继续。循环中随后的语句将被忽略。 |

你可以在本章后续部分中找到编程示例和对各项内容的扩展解释。

## 重复与 `for` 语句

`for` 语句为程序中的基本重复提供了典型的载体。使用它很方便，因为它让你有机会将三个参数引入重复活动中。在查看以下列表中的项目时，请参考图 11.2：

- **控制值。** 控制值是一个标量标识符，用于建立起始值。起始值通常设置为零（0）。
- **限制。** 第二个表达式使用关系运算符将控制标识符的值与另一个值进行比较，该值通常由你作为常量值提供。
- **增量表达式。** 增量表达式通常由控制值加上或减去增量运算符组成。

## 第 11 章 — 控制结构与应用

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_278_0.png)

Listing11_01 演示了 `for` 语句的几种变体。基本的 `for` 语句使用由分号分隔的三个参数。根据你要解决的问题，你可以将这些参数放在括号内或外部。例如，你可以在控制块内递增控制值，或者在 `for` 语句之前初始化计数器。

```perl
#Listing11_01

#1 Basic for repetition statement
#Control, Limit, and Counter

$Example = 1;
@Minerals = qw(Covelite Galena Stibnite
               Molybdenite Graphite Pyrolusite Basalt);

$LIMIT = scalar(@Minerals);

# 1 Set the counter at 0 to accommodate the array
print "\n\n Example " . $Example++ .
      ': for($Itr = 0; $Itr < $LIMIT ; $Itr++)' . "\n ";

for($Itr = 0; $Itr < $LIMIT ; $Itr++)
{
    print "\n " . $Itr . " $Minerals[$Itr].";
}
# 2 Increment inside the loop by increments of 2
print "\n\n Example " . $Example++ .
```

```php
': for($Itr = 0; $Itr < $LIMIT ;)' . "\n ";

for($Itr = 0; $Itr < $LIMIT ;)
{
    print "\n " . $Itr . " $Minerals[$Itr].";
    $Itr = $Itr + 2;
}

# 3 Pre-decrement operator inside the loop ; set limit outside
print "\n\n Example " . $Example++ .
': for(; $Itr >=0;)' . "\n ";
$Itr = $LIMIT;
for(; $Itr > 0 ;)
{
    --($Itr);
    print "\n " . $Itr . " $Minerals[$Itr].";
}
```

在注释 #1 处，你设置了一个由几个元素名称组成的数组。你还使用 `scalar()` 函数来访问数组中的元素数量，并将其分配给 `$LIMIT` 标识符。鉴于你已将元素数量分配给 `$LIMIT`，你随后实现了一个 `for` 重复语句，该语句采用了可能被称为 `for` 测试表达式的标准形式。标识符 `$Itr` 被设置为 0。你通过设置将其限制在小于 `$LIMIT` 的值的条件来控制 `$Itr` 可以达到的最大值。要移动计数器，你使用增量运算符（`$Itr++`）。结果如图 11.3 中的示例 1 所示。

在注释 #2 处，你设置了一个 `for` 语句，将增量操作放在 `for` 块内。推进计数器的语句以 2 为增量进行推进。你可以在图 11.3 中的示例 2 之后看到结果。

注释 #3 之后的行中出现了一种不同的方法。使用这种 `for` 语句的实现，你可以递减循环。在为重复语句设置最大值后，你使用控制表达式的中间条件来限制计数器的值，使其大于 0。在 `for` 块内，你以 2 为递减量递减计数器。结果出现在图 11.3 中的示例 3 之后。

## 使用 last 退出 for 循环

除了使用 `for` 语句控制外，你还可以实现使用 `last` 运算符的循环。`last` 运算符导致程序流程退出重复块。Listing11_02 提供了使用 `if` 和 `unless` 选择语句的示例。

```perl
#Listing11_02
#1 Set up some data
$Example = 1;
@Minerals = qw(Covelite Galena Stibinite
    Molybdenite Graphite Pyrolusite);
$LIMIT = scalar(@Minerals);

print "\n\nExample " . $Example++ .
    ': for(;;){unless(){last;;}}' . "\n\n";
#2 Set the counter at 0 to accommodate the array
$Itr = 0;
for(;;)
{
    print "\n " . $Itr . " " $Minerals[$Itr++] .";
    unless($Itr < $LIMIT)
    {
        last;
    }
}
```

## 图 11.3

你可以将 `for` 语句的控制元素放在 `for` 块内部和外部。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_280_0.png)

## 使用 last 退出 for 循环

```perl
print "\n\n Example " . $Example++ .
': for(;;){if(){last;}}' . "\n";
#3 Use an if selection statement to exit using last
$Itr = 0;
for(;;)
{
	print "\n " . $Itr . " $Minerals[$Itr++].";
	if($Itr >= $LIMIT)
	{
		last;
	}
}
```

在 Listing11_02 中的注释 #1 处，你设置了一个数组（@Minerals）以供程序中的 `for` 循环使用。你还使用 `scalar()` 函数来获取数组中的元素数量。

注释 #2 之后的行实现了一个 `for` 控制语句，该语句在括号之间没有控制语句。计数器（$Itr）在 `for` 语句之前设置。在语句块内，你使用 `unless` 选择语句来评估计数器何时大于限制。当这种情况发生时，你调用 `last` 运算符。`last` 运算符退出 `for` 循环。

在注释 #2 标识的行中，你再次设置了一个 `for` 重复语句，该语句在括号之间不包含控制内容。你在控制语句之前定义迭代器。在 `for` 块内，你使用 `if` 选择语句来评估计数器何时超过限制。当它超过限制时，你退出 `for` 块。图 11.4 说明了 Listing11_02 的输出。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_281_0.png)

**图 11.4**
你可以将 `if` 和 `unless` 选择与 `last` 结合使用，以退出重复块。

