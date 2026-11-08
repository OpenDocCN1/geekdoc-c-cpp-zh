
- **13.9 宏安全与保护** 426
  - 13.9.1 隐藏宏代码 426
  - 13.9.2 执行特定宏版本 427
- **13.10 使用宏语言 IN 运算符** 430
  - 13.10.1 可能出什么问题 430
  - 13.10.2 使用 MINOPERATOR 选项 431
  - 13.10.3 使用 MINDELIMITER= 选项 432
  - 13.10.4 这些选项的编译与执行 432
- **13.11 使用 MFILE 系统选项** 433
- **13.12 宏引用浅谈** 434

关于宏语言已经有很多著述。SAS Institute 提供的文档很好，而且已经有两本 SAS Press 的书专门讨论这个主题：*Carpenter 的 SAS 宏语言完全指南，第 2 版*（Carpenter，2004）和 *SAS 宏编程轻松入门，第 2 版*（Burlew，2006）。因此，本书对宏语言的论述必然只能限于少数几个主题。

## 另见

Russ Tyndall 是 SAS Institute 负责 DATA 步和宏语言的首席技术支持分析师，他撰写了 TS739（Tyndall，2005），其中包含许多高级技巧以及宏语言的一些较新功能。

## 13.1 避免宏变量冲突——让宏变量成为 %Local

“在宏内部创建的宏变量将局部于该宏”这一经验法则是一条非常危险的规则，原因恰恰在于它通常是对的。在编程世界里，偶尔才出现的问题是最难发现和修复的问题之一。仅仅知道符号表赋值的规则（而知道这些规则绝非易事）是不够的。大多数符号表赋值取决于宏程序员通常不知道、甚至更常见的是无法知道的情况。符号表赋值的规则在 Carpenter，2004，第 13.6 节，第 395 页中描述。

当宏变量赋值被写入非预期的符号表，并意外覆盖现有宏变量的值时，就会发生宏变量冲突。这种情况经常发生在同一个宏变量名被无意中用于一系列嵌套宏中的多个宏时。

```sas
%macro primary;
.... code not shown....

  %do i = 1 %to &dsncnt; ❷
    %chksurvey(&dsn&i);
  %end;

.... code not shown....
%mend primary;
```

这里展示的程序片段中包含一个微妙的宏变量冲突示例，这种冲突可能造成可怕的错误，却让程序员浑然不觉。在这个例子中，一个次级宏（%CHKSURVEY）从 %PRIMARY 中的 %DO 循环内被调用。

```sas
%macro chksurvey(dset);
.... code not shown....

  %do i = 1 %to 5; ❶

.... code not shown....
%mend chksurvey;
```

%PRIMARY 中的 %DO 循环似乎运行无误。但更仔细地检查内部宏 %CHKSURVEY，就会发现一个隐藏的问题。

❶ %CHKSURVEY 中的 %DO 循环使用 &I 作为索引变量。这个变量通常会局部于 %CHKSURVEY；然而，由于 &I 已经存在于调用宏的更高层符号表中，它就不会是局部的。当 %CHKSURVEY 执行时，它会修改 %PRIMARY 更高层符号表中 &I 的值。❷

在这个例子中，如果 &DSNCNT ❷ 小于或等于 6，%PRIMARY 中的循环将只执行一次。如果程序员运气好，&DSNCNT 会大于 6，从而产生无限循环。这算是幸运的，因为这样程序员至少会知道要查找问题！

不幸的是，我们无法保护符号表中的宏变量不被外层宏所调用的宏覆盖。但是，我们可以通过强制将所有宏变量放入 LOCAL 符号表来保护更高层符号表。这是通过使用 %LOCAL 语句完成的。在使用嵌套宏调用（即调用宏的宏）时，一定要始终使用 %LOCAL 来防止冲突！！在前面的例子中，只需将 %LOCAL 语句添加到 %CHKSURVEY，就可以避免冲突。❸ 顺带说一句，我们无法确定 %PRIMARY 中的宏变量 &I 不会同样对更高层符号表造成问题，因此该宏中也应当包含 %LOCAL 语句。

```sas
%macro chksurvey(dset);
  %local i;
.... code not shown....

  %do i = 1 %to 5;

.... code not shown....
%mend chksurvey;
```

在上一段中，我建议你始终使用 %LOCAL 语句。其他人认为这种说法过于强硬，%GLOBAL 语句和全局符号表存在是有原因的——就是为了让我们使用它们。毕竟，这种观点认为，在某些情况下，你希望将值从局部符号表传出并传入全局环境。虽然我承认这种需求，甚至可能承认自己也曾以这种方式使用全局符号表，但恕我直言，我的看法带有偏见：这不应当成为首选方案；它通常是在本章讨论的某种替代技术不可行，或者更可能是尚未被充分理解时采用的解决方案。话虽如此，只要程序员完全理解风险并正确、成功地缓解了这些风险，使用全局符号表传递值并没有什么错。

使用全局符号表的问题在于，它并不存在于嵌套宏所隐含的父子层级中。调用宏是父宏，被调用宏是子宏。我们可以利用这种关系。

避免冲突的最佳方式是直接控制符号表的放置位置。我们通过在宏定义中放置 %LOCAL 语句做到了这一点。另一种不使用全局符号表的方法，是定义你的宏变量，以及符号

### 13.2.1 与 CALL SYMPUT 的比较

SYMPUTX 例程相对于 SYMPUT 有两个主要优点和一个次要缺点。SYMPUTX 相对于 SYMPUT 的唯一缺点是，它的名称多了一个需要输入的字母，而这个字母是 x！实际上，这并不算多大的缺点。

SYMPUTX 相对于 SYMPUT 的优点：

- 自动转换数值输入（不会在 LOG 中产生提示）。❶
- 在将数值型第二个参数转换为字符值时，使用最多 32 个字符的字段宽度。CALL SYMPUT 使用最多 12 个字符的字段宽度。
- 赋值前会移除值的前导空格和尾随空格。❸
- 能够强制将宏变量放入局部或全局符号表。❹

SYMPUTX 相对于 SYMPUT 的优点足够大，以至于通常所有新代码都

```sas
data _null_;
   set advrpt.demog(where=(subject=205));
   call symput('EDU205a',edu); ❶
   call symput('EDU205b',left(put(edu,3.))); ❷
   call symputx('EDU205c',edu); ❸
run;
%put &edu205a| &edu205b| &edu205c|;
```

优先使用 SYMPUTX 而不是 SYMPUT 来编写。这些优点在这个示例中得到了展示：该示例将受试者 205 的数值变量 EDU 的值写入三个宏变量。❶ 使用数值变量 EDU 会在 LOG 中生成一条转换提示，并会存储一个右对齐的字符串。

❷ 使用 SYMPUT 时，必须使用 PUT 函数转换数值，以避免在 LOG 中出现提示。这里本可以使用 TRIM 函数来避免存储尾随空格。

❸ SYMPUTX 例程解决了 ❶ 和 ❷ 中展示的两个问题。

LOG 显示：

```text
NOTE: Numeric values have been converted to character values at the
      places given by: ❶
      (Line):(Column).
      47:26
NOTE: There were 1 observations read from the data set ADVRPT.DEMOG.
      WHERE subject=205;
NOTE: DATA statement used (Total process time):
      real time           0.06 seconds
      cpu time            0.00 seconds

51   %put &edu205a| &edu205b| &edu205c|;
      12| 12| ❶ 12| ❷
```

SYMPUTX 例程的可选第三个参数可用于将宏变量

```sas
call symputx('EDU205c',edu,'l' ❸);
```

放入局部（'l' 或 'L'）或全局（'g' 或 'G'）符号表 ❸。在试图避免宏变量冲突时，控制符号表赋值的能力尤为重要（见第 13.1 节）。当宏变量的名称像本例中那样已知时，使用 %LOCAL（或 %GLOBAL）语句同样容易。然而，当宏变量的名称是在程序执行期间派生出来时，并不总是能够使用 %LOCAL 语句。
