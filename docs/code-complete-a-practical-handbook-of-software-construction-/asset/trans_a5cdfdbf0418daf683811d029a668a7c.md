

## 尽可能缩短变量的“存活”时间

与变量作用域相关的一个概念是变量的“存活时间”，即变量保持存活的语句总数。变量的生命周期始于首次被引用的语句；其生命周期结束于最后一次被引用的语句。

与作用域不同，存活时间不受变量在首次和最后引用之间使用次数的影响。如果变量首次在第 1 行被引用，最后在第 25 行被引用，则其存活时间为 25 条语句。如果这两行是唯一使用它的行，则其平均作用域为 23 条语句。如果变量在第 1 行到第 25 行的每一行都被使用，则其平均作用域为 0 条语句，但其存活时间仍为 25 条语句。图 10-1 说明了作用域和存活时间。

![](img/649c8eee28c38ca1e062691e45dc9883_282_0.png)

![](img/649c8eee28c38ca1e062691e45dc9883_282_1.png)

图 10-1 “长存活时间”意味着变量在许多语句期间保持存活。“短存活时间”意味着它仅在少数几条语句中存活。“作用域”指的是对变量的引用有多接近。

与作用域一样，关于存活时间的目标是保持数值尽可能低，即尽可能缩短变量的存活时间。与作用域一样，保持数值较低的基本优势在于它减少了脆弱窗口。你减少了

在你打算更改它的地方之间错误地或无意地更改变量的可能性。

保持存活时间短的第二个优势是它能让你准确地了解你的代码。如果一个变量在第 10 行被赋值为一个值，直到第 45 行才再次使用，两次引用之间的空间本身就暗示该变量在第 10 行和第 45 行之间被使用。如果变量在第 44 行被赋值为一个值，并在第 45 行使用，则不会暗示变量的其他用途，并且当你思考该变量时，可以集中在较小的代码段上。

短的存活时间还能降低初始化错误的风险。随着你修改程序，直线代码往往会变成循环，而你往往会忘记在循环远处进行的初始化。通过让初始化代码和循环代码更接近，你可以降低修改引入初始化错误的可能性。

短的存活时间使你的代码更具可读性。读者一次需要记住的代码行越少，你的代码就越容易理解。同样，存活时间越短，在编辑和调试时，你需要保留在屏幕上的代码就越少，以便查看变量的所有引用。

最后，短的存活时间在将大型例程拆分为更小型例程时很有用。如果对变量的引用保持紧密，就更容易将相关的代码段重构为自己的例程。

## 衡量变量的存活时间

你可以通过计算变量首次和最后引用之间的行数来形式化存活时间的概念，包括首次和最后两行。以下是存活时间过长的示例：

```
Java Example of Variables with Excessively Long Live Times
1  // initialize all variables
2  recordIndex = 0;
3  total = 0;
4  done = false;
   ...
26 while ( recordIndex < recordCount ) {
27  ...
28      recordIndex = recordIndex + 1;
   ...
64 while ( !done ) {
   ...
69  if ( total > projectedTotal ) {
70      done = true;
Last reference to recordIndex.
Last reference to total.
Last reference to done.
```

以下是此示例中变量的存活时间：

*recordIndex*      ( line 28 - line 2 + 1 ) = 27
*total*            ( line 69 - line 3 + 1 ) = 67
*done*             ( line 70 - line 4 + 1 ) = 67
Average Live Time  ( 27 + 67 + 67 ) / 3 = 54

下面重写了该示例，使变量引用更接近：

## Java Example of Variables with Good, Short Live Times

```
25  recordIndex = 0;
26  while ( recordIndex < recordCount ) {
27  ...
28      recordIndex = recordIndex + 1;
...
62  total = 0;
63  done = false;
64  while ( !done ) {
...
69      if ( total > projectedTotal ) {
70          done = true;
```

recordIndex 的初始化从第 3 行移至下方。

total 和 done 的初始化从第 4 行和第 5 行移至下方。

以下是此示例中变量的存活时间：

*recordIndex*      ( line 28 - line 25 + 1 ) = 4
*total*            ( line 69 - line 62 + 1 ) = 8
*done*             ( line 70 - line 63 + 1 ) = 8
Average Live Time  ( 4 + 8 + 8 ) / 3 ≈ 7

> 进一步阅读 有关“存活”变量的更多信息，请参阅 *Software Engineering Metrics and Models*（Conte, Dunsmore, and Shen 1986）。

直观上，第二个示例比第一个更好，因为变量的初始化更接近变量的使用位置。两个示例之间平均存活时间的差异是显著的：平均 54 与平均 7 提供了良好的定量支持，支持对第二段代码的直觉偏好。

是否有硬性数字可以将良好的存活时间与不良的存活时间区分开？良好的作用域与不良的作用域？研究人员尚未产生该定量数据，但可以安全地假设最小化作用域和存活时间是一个好主意。

如果你尝试将作用域和存活时间的概念应用于全局变量，你会发现全局变量具有巨大的作用域和存活时间——这是避免全局变量的众多充分理由之一。

## 最小化作用域的一般准则

以下是你可以用来最小化作用域的一些具体准则：

交叉引用 有关在变量使用附近初始化变量的详细信息，请参阅本章前文第 10.3 节“初始化变量的准则”。

# 将循环中使用的变量在循环之前立即初始化，而不是在包含循环的例程开头初始化

这样做可以提高你在修改循环时记住对循环初始化进行相应修改的机会。后来，当你修改程序并在初始循环外再加一个循环时，初始化将在每次通过新循环时生效，而不是仅在第一次通过时生效。

交叉引用 有关这种变量声明和定义风格的更多信息，请参阅第 10.3 节中“理想情况下，在变量首次使用附近声明和定义每个变量”。

# 不要在值使用之前很久就为变量赋值，而是在值使用前立即赋值

你可能经历过试图弄清楚变量的值是在哪里赋值的挫败感。你能做得越多来明确变量从何处接收其值越好。像 C++ 和 Java 这样的语言支持以下类型的变量初始化：

```
C++ Example of Good Variable Declarations and Initializations
int receiptIndex = 0;
float dailyReceipts = TodaysReceipts();
double totalReceipts = TotalReceipts( dailyReceipts );
```

交叉引用 有关保持相关语句在一起的更多详细信息，请参阅第 14.2 节“语句顺序无关紧要”。

# 对相关语句进行分组

以下示例展示了汇总每日收据的例程，并说明了如何将对变量的引用放在一起以便更容易定位。第一个示例说明了违反这一原则的情况：

```
C++ Example of Using Two Sets of Variables in a Confusing Way
void SummarizeData(...) {
...
GetOldData( oldData, &numOldData );
GetNewData( newData, &numNewData );
totalOldData = Sum( oldData, numOldData );
totalNewData = Sum( newData, numNewData );
PrintOldDataSummary( oldData, totalOldData, numOldData );
PrintNewDataSummary( newData, totalNewData, numNewData );
SaveOldDataSummary( totalOldData, numOldData );
SaveNewDataSummary( totalNewData, numNewData );
...
}
```

请注意，在此示例中，你必须同时跟踪 oldData、newData、numOldData、numNewData、totalOldData 和 totalNewData——仅此一项就有六个变量

使用两组变量的语句。

