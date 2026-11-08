
- ❻ IF-THEN/ELSE 处理用于确定数据源，并为变量 GROUP 赋值。

对于大型数据集，IF-THEN/ELSE 可能很耗时，可以通过使用 INDSNAME= SET 语句选项完全避免。

```sas
data grouped2;
   set boomer
        others indsname=dsn; ❸
   length group $6; ❺
   group=scan(dsn,2,'.'); ❹
run;
```

- ❸ INDSNAME= 选项标识一个临时字符变量（DSN），该变量保存当前观测所读取数据集的名称。
- ❹ 由于变量 DSN 将包含两级名称（'WORK.BOOMER'），因此使用 SCAN 函数删除 libref 部分，并将名称部分（第二个词）存储在变量 GROUP 中。
- ❺ 声明 GROUP 变量的长度；否则，SCAN 函数将返回 $200 的长度。

INDSNAME= 选项的默认长度为 $41。如果使用物理路径（作者通常不推荐这样做），这可能不够长。

### 3.8.3 关于 END= 选项的说明

END= 选项可用于创建一个数值型（0/1）临时变量，用于指示最后一条记录已被读取。在下面的示例中，使用 END= 选项定义的 EOF 变量 ❷ 用于控制何时执行 PUT 语句。

```sas
data a;
   if eof then put total=; ❶
   set sashelp.class end=eof; ❷
   end=eof;
   total+age;
   put 'last ' age= total= eof=;
run;
```

IF 语句 ❶ 仅有一次为真，其操作（PUT 语句）仅在 DATA 步的最后一遍执行。

但是，请注意 IF 语句 ❶ 位于 SET 语句之前。这提醒我们，默认情况下，直到读取最后一条观测后尝试执行 SET 语句时，DATA 步才会完全终止。

```text
last Age=12 total=212 eof=0
last Age=15 total=227 eof=0
last Age=11 total=238 eof=0
last Age=15 total=253 eof=1
total=253
```

### 3.8.4 包含两个 SET 语句的 DATA 步

正如本章中众多示例所示，DATA 步可以包含多个 SET 语句。多个 SET 语句可以在读取数据的过程中为你提供极大的能力和灵活性。然而，当你控制读取过程时，请务必谨慎，并确保你理解你要求 DATA 步执行什么。

```sas
data new;
   set a;
   set b;
run;
```

这个双 SET 语句的最简单情况本质上是一种带限制的一对一合并。而这些限制（也可以说是条件）非常重要。

在没有其他控制（通常由程序员提供）的情况下，新数据集中的观测数由最小的原始数据集中的观测数决定。一旦 SAS 从**任一数据集读取到最后一条观测，整个 DATA 步就不会再次完整执行。**

你会注意到，在所有其他包含两个 SET 语句的示例中，对于 SET 语句如何执行都有一些限制或控制。通常，我们希望该步按我们的条件终止，而不一定仅仅因为从其中一个数据集读取到了最后一条观测。

与 MERGE 一样，如果存在共同变量，则从最后一个数据集读入的值会替换从较早数据集读入的值。同样与 MERGE 一样，PDV 将包含来自任一输入数据集的所有变量，并且每个变量将根据其在 DATA 步编译期间首次遇到时的情况分配属性。一如既往，从输入数据集读取的任何变量都会自动保留。

如第 3.1.5、3.1.6 和 3.8.1 节所示，能够使用多个 SET 语句是可能的，有时甚至非常有利。只需确保你理解这样做时发生了什么，并确保在控制读取过程时保持谨慎。

### **更多信息**

第 3.8.1 节的第二个示例中使用了两个 SET 语句。第 3.6.2 节中的示例使用 DOW 循环和两个 SET 语句读取两个数据集。

### **另见**

一个 SAS 论坛问题的解决方案使用了包含两个 SET 语句的 DATA 步  
http://communities.sas.com/message/42266。

## 3.9 使用 DO 循环做更多事情

DO 语句的四种主要形式广为人知，并且通常被应用以取得很大优势。然而，我们还可以用这个语句做更多事情，有时甚至以令人惊讶的方式。本节讨论其中一些技巧。

### **另见**

Paul Dorfman（2002）对 DO 循环做了很好的概述，并演示了它的许多行为。Fehd（2007）讨论了 DO UNTIL 和 DO WHILE 循环之间的差异。可以在 SASCommunity.org 上找到大量参考文献和链接列表：  
http://www.sascommunity.org/wiki/Do_until_last.var。

### 3.9.1 使用 DOW 循环

虽然 DOW 循环可能最初由 Don Henderson 提出，但 DOW 循环（也称为 DO-W 循环）是以 Ian Whitlock 命名的，他推广了这项技术，并且是最早展示其效率的人之一。DOW 循环通常可用于提高 DATA 步的性能；在其最简单的形式中，DOW 循环会控制 DATA 步的隐含循环。

考虑 DATA 步的隐含循环。在执行阶段，DATA 步中的每个可执行语句都会为输入数据集（WORK.BIG）中的每条观测执行一次。这包括相当多的后台处理。当执行 DATA 语句时，派生变量的值会被清除，临时变量 _N_ 的值会递增。对于此处展示的步，我们并不关心这些事情。通过使用 DOW 循环，我们可以绕过隐含循环。

```sas
data implied;
  set big;
  output implied;
  run;
```

### 3.9.2 复合循环规范

迭代 DO 循环通常用于遍历一个值列表。较少为人所知的是，我们并不局限于单个列表。这里的变量 COUNT 取值为 1、2、3、5、10、15、20、26 和 33。这个 DO 语句实际上有四个不同的循环规范。第一个（1 to 3）有一个隐含的 BY，最后两个由一个单值组成。事实上，正如最后两个规范所演示的那样，TO 和 BY 并非必需。数字本身不必是数值常量，也可以写成求值为数字的表达式。

```sas
do count=1 to 3, 5 to 20 by 5, 26, 33;
```

为了说明表达式的使用，这个示例包含了一个表达式；然而，迭代 DO 仅限于单个索引变量。在此处展示的 DO 语句中，作者希望先遍历 COUNT（1、2、3），然后遍历 CNT（4、6、8）。然而，实际情况并非如此。

```sas
do count=1 to 3, cnt=4 to 8 by 2;
```

CNT=4 被解释为一个逻辑表达式，其求值为 0 或 1。如果 CNT 不等于 4，则第二个循环规范将使 COUNT 取值 0、2、4、6、8；否则，该规范将得到值 1、3、5、7。实际上，这个 DO 语句的编码方式就好像表达式被括号包围一样。

```sas
do count=1 to 3, (cnt=4) to 8 by 2;
```

由于各个值都是表达式，你也可以使用求值为字符值的表达式。

```sas
do month = 'Jan', 'Feb', 'Mar';
```

### 3.9.3 循环规范的特殊形式

迭代 DO 循环在循环底部进行求值。每次遍历后，在 END 语句处，循环计数器会递增，然后进行求值。下面的简单循环展示了这一点。

```sas
data _null_;
   do count=1 to 3;
      put 'In loop ' count=;
   end;
   put 'Out of loop ' count=;
run;
```

日志显示，在退出循环之前，该变量已递增到 4。

```text
In loop count=1
In loop count=2
In loop count=3
Out of loop count=4
```

通常这种行为是可以接受的；然而，我们可能希望控制计数器在最后一次是否递增。我们可以向 DO 语句添加 UNTIL，以对循环如何退出提供额外控制。日志显示，UNTIL 子句在计数器（COUNT）递增之前执行。

```sas
data _null_;
   do count=1 to 3 until(count=3);
      put 'In loop ' count=;
   end;
   put 'Out of loop ' count=;
run;
```

```text
In loop count=1
In loop count=2
In loop count=3
Out of loop count=3
```

