

## 5.3.3.4 声明语句

- 如果 stmt 是不带初始化器的声明语句，则 v 在 stmt 结束点的明确赋值状态与在 stmt 开始处相同。
- 如果 stmt 是带有初始化器的声明语句，则 v 的明确赋值状态按如下方式确定：就像 stmt 是一个语句列表，其中每个带初始化器的声明对应一个赋值语句（按声明顺序）。

## 5.3.3.5 if 语句

对于形式如下的 if 语句 stmt：

```
if ( expr ) then-stmt else else-stmt
```

- v 在 expr 开始处的明确赋值状态与在 stmt 开始处相同。
- 如果 v 在 expr 结束处已明确赋值，则在控制流转移到 then-stmt 以及转移到 else-stmt（如果没有 else 子句，则转移到 stmt 的结束点）时，v 都已明确赋值。
- 如果 v 在 expr 结束处具有“真表达式之后明确赋值”状态，则在控制流转移到 then-stmt 时，v 已明确赋值；而在控制流转移到 else-stmt 或（如果没有 else 子句）stmt 的结束点时，v 未明确赋值。
- 如果 v 在 expr 结束处具有“假表达式之后明确赋值”状态，则在控制流转移到 else-stmt 时，v 已明确赋值；而在控制流转移到 then-stmt 时，v 未明确赋值。当且仅当 v 在 then-stmt 的结束点已明确赋值时，v 才在 stmt 的结束点已明确赋值。
- 否则，在控制流转移到 then-stmt 或 else-stmt，或（如果没有 else 子句）转移到 stmt 的结束点时，v 被视为未明确赋值。

## 5.3.3.6 switch 语句

在以 expr 为控制表达式的 switch 语句 stmt 中：

- v 在 expr 开始处的明确赋值状态与 v 在 stmt 开始处的状态相同。
- 在控制流转移到可到达的 switch 块语句列表时，v 的明确赋值状态与 v 在 expr 结束处的明确赋值状态相同。

> **埃里克·利珀特** 不幸的是，在少数情况下，可以在没有默认 switch 标签的情况下对整个控制表达式的范围进行穷举 switch（即 bool、字节类型及其对应的可空类型），此时明确赋值检查不会考虑以下可能性：如果变量在每个 switch 节结束时都已明确赋值，那么它在 switch 结束时也可能已明确赋值。例如：
>
> ```
> int x;
> bool b = B();
> switch(b) {
> case true : x = 1; break;
> case false: x = 2; break;
> }
> Console.WriteLine(x); // Error: x is not definitely assigned
> ```
>
> 在这些罕见情况下，你总是可以在某个 switch 节上放置一个不必要的默认 switch 标签，以使明确赋值检查器满意。

## 5.3.3.7 while 语句

对于形式如下的 while 语句 stmt：

```
while ( expr ) while-body
```

- v 在 expr 开始处的明确赋值状态与在 stmt 开始处相同。
- 如果 v 在 expr 结束处已明确赋值，则在控制流转移到 while-body 以及转移到 stmt 的结束点时，v 都已明确赋值。
- 如果 v 在 expr 结束处具有“真表达式之后明确赋值”状态，则在控制流转移到 while-body 时，v 已明确赋值，但在 stmt 的结束点未明确赋值。
- 如果 v 在 expr 结束处具有“假表达式之后明确赋值”状态，则在控制流转移到 stmt 的结束点时，v 已明确赋值，但在控制流转移到 while-body 时，v 未明确赋值。

## 5.3.3.8 do 语句

对于形式如下的 do 语句 stmt：

```
do do-body while ( expr ) ;
```

- 在控制流从 stmt 开始处转移到 do-body 时，v 的明确赋值状态与在 stmt 开始处相同。
- v 在 expr 开始处的明确赋值状态与在 do-body 的结束点相同。
- 如果 v 在 expr 结束处已明确赋值，则在控制流转移到 stmt 的结束点时，v 已明确赋值。
- 如果 v 在 expr 结束处具有“假表达式之后明确赋值”状态，则在控制流转移到 stmt 的结束点时，v 已明确赋值。

## 5.3.3.9 for 语句

对于形式如下的 for 语句：

```
for ( for-initializer ; for-condition ; for-iterator ) embedded-statement
```

其明确赋值检查按如下方式完成：就像该语句写成：

```
{
    for-initializer ;
    while ( for-condition ) {
        embedded-statement ;
        for-iterator ;
    }
}
```

如果 for 语句中省略了 for-condition，则明确赋值的计算按如下方式进行：就像在上述展开中用 true 替换了 for-condition。

## 5.3.3.10 break、continue 和 goto 语句

由 break、continue 或 goto 语句引起的控制流转移中，v 的明确赋值状态与 v 在语句开始处的明确赋值状态相同。

## 5.3.3.11 throw 语句

对于形式如下的语句 stmt：

```
throw expr ;
```

## 5.3.3.12 return 语句

对于形式如下的语句 stmt：

```
return expr ;
```

- v 在 expr 开始处的明确赋值状态与 v 在 stmt 开始处的明确赋值状态相同。
- 如果 v 是输出参数，则它必须在以下位置之一已明确赋值：
  - 在 expr 之后；或
  - 在包含该 return 语句的 try-finally 或 try-catch-finally 的 finally 块结束处。

对于形式如下的语句 stmt：

```
return ;
```

- 如果 v 是输出参数，则它必须在以下位置之一已明确赋值：
  - 在 stmt 之前；或
  - 在包含该 return 语句的 try-finally 或 try-catch-finally 的 finally 块结束处。

## 5.3.3.13 try-catch 语句

> **比尔·瓦格纳** 从这里开始，你会看到任何非结构化语句（例如 throw、catch、goto、finally）如何使编译器的分析和你自己的理解都变得复杂。在日常逻辑中使用这些语句时要小心。try/finally 语句是一个简化的特殊情况，但一般情况会大大降低程序的可读性。

对于形式如下的语句 stmt：

```
try try-block
catch(...) catch-block-1
...
catch(...) catch-block-n
```

- v 在 try-block 开始处的明确赋值状态与 v 在 stmt 开始处的明确赋值状态相同。
- v 在 catch-block-i 开始处（对于任意 i）的明确赋值状态与 v 在 stmt 开始处的明确赋值状态相同。
- v 在 stmt 结束点的明确赋值状态为已明确赋值，当且仅当 v 在 try-block 的结束点以及每个 catch-block-i（对于从 1 到 n 的每个 i）的结束点都已明确赋值。

## 5.3.3.14 try-finally 语句

对于形式如下的 try 语句 stmt：

```
try try-block finally finally-block
```

- v 在 try-block 开始处的明确赋值状态与 v 在 stmt 开始处的明确赋值状态相同。
- v 在 finally-block 开始处的明确赋值状态与 v 在 stmt 开始处的明确赋值状态相同。
- v 在 stmt 结束点的明确赋值状态为已明确赋值，当且仅当以下至少一项为真：
  - v 在 try-block 的结束点已明确赋值。
  - v 在 finally-block 的结束点已明确赋值。

如果发生控制流转移（例如 goto 语句），该转移从 try-block 内开始并在 try-block 外结束，那么如果 v 在 finally-block 的结束点已明确赋值，则 v 在该控制流转移上也被视为已明确赋值。（这不是“仅当”：如果 v 由于其他原因在该控制流转移上已明确赋值，则它仍被视为已明确赋值。）

## 5.3.3.15 try-catch-finally 语句

对于形式如下的 try-catch-finally 语句，其明确赋值分析按如下方式完成：就像该语句是包含 try-catch 语句的 try-finally 语句：

```
try {
  try try-block
  catch(...) catch-block-1
  ...
  catch(...) catch-block-n
}
finally finally-block
```

下面的示例演示了 try 语句（§8.10）的不同块如何影响明确赋值。

