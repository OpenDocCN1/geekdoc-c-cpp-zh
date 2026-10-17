

## 第 5 章 标量与格式化

```
$TableTitleText .
$DC x int(( $TW - length($TableTitleText))/2));
#3 Create the table rows
$RowZ = sprintf "%s", $NL . $TableTitle;
$RowE = sprintf "$COLSTRSTR",
$NL . $COLAHEAD, $COLBHEAD;
$RowA = sprintf "$COLSTRF",
$NL . $ProEText,
$PlRadiusOfEarth;
$RowB = sprintf "$COLSTRF",
$NL . $ERoEText,
$EqRadiusOfEarth;
$RowC = sprintf "$COLSTRE",
$NL . $EtSText,
$EarthToSun;
$RowD = sprintf "$COLSTRF",
$NL . $EtMText,
$EarthToMoon;
$RowF = sprintf "$COLSTRF",
$NL . $AoSSText,
$AgeOfSolarSystem;
$RowG = sprintf "$COLSTRF",
$NL . $AoKUText,
$AgeOfKnownUniverse;
$RowH = sprintf "$COLSTRF",
$NL . $REtoUText,
$RatioOfSStOku;
$RowI = sprintf "$COLSTRF",
$NL . $SoLMSText,
$SpeedOfLight;
$RowJ = sprintf "$COLSTRF",
$NL . $SoLKSText, $
KmspeedOfLight;
#4 Create the table
$AstroTable = join("", ($DL, $RowZ,
$DL, $RowE, $DL,
$RowA, $SL,
$RowB, $SL,
$RowC, $SL,
$RowD, $SL,
$RowF, $SL,
$RowG, $SL,
$RowH, $SL,
$RowI, $SL,
$RowJ,
$DL)));

#Print the table
print $AstroTable;
```

在 Listing05_13 中紧随注释 #1 和 #2 之后的行中，你定义程序所使用的数据和格式化信息。完成此代码后，你编写的任何代码都不能以相当通用的方式使用。这种定义表格格式的方法的目标是，从构建表格的工作中（这项工作始于与注释 #3 关联的代码）尽可能移除更多细节。当你使用标量来存储格式化信息时，例如，你可以更改表格中任何字段的宽度或内容，只需更改你在注释 #1 和 #2 所指定部分中设置的标识符。这种任务隔离特征体现在许多编程工作中。

在与注释 #3 关联的代码中，你使用程序中先前创建的标识符，不再使用文本字符串、标签或格式化说明符。相反，你使用与注释 #1 和 #2 关联的行中定义的通用组件。同样，请注意在 sprintf() 调用中省略括号的“Perl 风格”。这种做法可能比使用括号更常见，但省略括号（在此语境下）构成一种编程特性。最终，你能多轻松地阅读和维护代码，应决定你是否使用括号。

图 5.15 说明了 Listing05_13 的输出。注释 #1 之后的代码行充当你可能视为从数据库检索的一组数据。

在 Listing05_13 与注释 #4 关联的部分中，你构建表格。表格的构建可以进一步简化。使用行标识符让你了解如何构建表格，并让你能够相对容易地添加或删除行。要删除一行，只需将其注释掉。

# 图 5.15 格式化表格变成了调整自定义格式标签的问题。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_146_0.png)

# 结论

在本章中，你探索了确定给定标识符是否已定义的不同方法。使用 defined() 和 undef() 函数在这方面证明很有帮助。在检查了使用数值所涉及的一些问题后，你创建了一些涉及定义数值数据的程序，并在其中包含了 Perl 提供的用于处理数值数据的函数。其中这些函数包括 int()、ord()、rand() 和 hex() 函数。在处理数值时最有益的函数是 printf() 和 sprintf() 函数。

printf() 函数允许你使用类型说明符和精度标志来格式化信息。使用 printf() 函数，你可以创建精确格式化的表格数据。在本章中，重点一直放在命令行输出上，但应该清楚，你学习如何使用打印函数的格式化功能所做的所有工作，都可以应用于 HTML、XML 和其他互联网开发领域。

你为 printf() 学到的所有格式化技巧都适用于 sprintf()。使用 sprintf()，你获得将一种数据类型转换为另一种的能力。你可以使用它将字符串转换为数字，或将数字转换为字符串。除了数据转换，它为你提供的一大优势涉及创建模块化程序。在这样的程序中，你隔离复杂性并创建可以用相对较小的努力更改的数据显示。

## 数组基础

本章为你介绍 Perl 数组。Perl 数组更像是一个容器，而不是一个基本数组。它会自动扩展。它允许你使用与之关联的许多函数来执行插入和提取元素等操作。在本章中，你主要关注与初始化数组以及处理几个与之相关的基本函数相关的问题。本章涉及的主题包括：

- 熟悉 Perl 数组的标量形式和隐式形式
- 探索几个定义问题
- 将较小的数组合并为较大的数组
- 更改数组中元素的顺序
- 使用专用函数将项目列表添加到数组
- 交换、切片和拼接数组

### 数组基础知识

数组由按顺序存储在计算机内存中的一系列项目组成。数组类似于一组抽屉。每个抽屉是一个元素。你可以根据元素的索引来了解数组中的每个元素。数组的索引从零开始。

如图 6.1 所示，Perl 数组具有两种形式。一种形式称为数组的*标量*形式或*标量*形式。你可以识别这种形式的数组，因为它看起来像一个带有后缀的标量标识符，后缀由包含数字的方括号组成。另一种形式称为数组的*隐式*形式。数组的隐式形式由带有商业“at”符号（@）前缀的标识符组成。

**图 6.1**
数组具有标量形式和隐式形式。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_148_0.png)

如本章和下一章所广泛探讨的，当你使用数组的标量形式时，你使用元素的索引来访问其元素。另一方面，要使用数组的隐式形式，你可以使用 Perl 提供的专门用于数组的相当大一组函数中的任何一个。图 6.1 说明了其中一个函数，`sort()`，它允许你按字母顺序或数值顺序组织数组中的元素。

# 添加元素

数组会动态扩展。因此，你不需要以任何方式声明或初始化它们，除非你在首次声明和定义它们时使用它们的方式。要向数组添加元素，你可以采用两种基本方法。从一种方法来看，你可以使用数组的标量（$）形式并命名要为其赋值的索引来向数组添加元素。从另一种方法来看，你可以使用所谓的*列表函数*将新元素分配给数组的隐式（@）形式。一些程序员将 @ 称为数组的*隐式*形式。Listing06_01 提供了几个示例，说明如何定义、检索和打印数组中的元素。

```
```perl
#Listing06_01
#Array definitions

$NL = "\n";
#1 Add items using the scalar form of the array
$NewArray[0] = "Fields ";
$NewArray[1] = "of ";
$NewArray[2] = "Green ";

#2 Print as a scalar or interpolated value
print "$NL Array element identified by index 1: "
                 . $NewArray[1] . "$NL";
```

print "$NL Array element identified by index 1: $NewArray[1] $NL";

#3 Use the list operation to add elements to an array
@SomeArrayA = (@SomeArrayA, "Little");
@SomeArrayA = (@SomeArrayA, "things", "always" );
@SomeArrayA = (@SomeArrayA, "matter", "in ", "the", "end");

#4 Interpolate an array to see all the values in it
print "$NL Elements after list add: " . "@SomeArrayA";

#5 Arrays accept any combination of data
@MixedArray = (32,all,22,44.7,32,34.5,numbers);
print "\n";
print "$NL Mixed array: @MixedArray";

#6 Retrieving values for printing
print "$NL Mixed array [0]: ". $MixedArray[0];
print "$NL Mixed array [1]: ". $MixedArray[1];
print "$NL Mixed array [2]: ". $MixedArray[2];
print "$NL Mixed array [3]: ". $MixedArray[3];

#7 Extracting values into a numeric context
$AddedValues = $MixedArray[0] + $MixedArray[3];
print "$NL Added Value " . $AddedValues . $NL ;
```

# 为数组赋值

如 Listing06_01 中与注释 #1 关联的行所示，要向数组添加元素，你可以使用数组的 $ 形式并将项目分配给特定索引。你可以指定任何索引。数组会扩展以容纳你分配的值：
$NewArray[0] = "Fields ";
$NewArray[1] = "of ";
$NewArray[2] = "Green ";

如 Listing06_01 中注释 #3 所显而易见的，要向数组的 @ 标识符添加元素，你可以使用列表函数。如前所述，列表函数涉及两个括号。你可以通过用逗号分隔来命名列表中的项目。要一次向数组添加一个元素，请将数组和要添加的元素放在括号内。数组占据第一个位置。以下是 Listing06_01 中的代码：

