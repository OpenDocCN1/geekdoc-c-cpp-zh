
“写注释会迫使你更深入地思考你的代码在做什么，”伊斯门从午餐室回来时说。“如果注释很难写，那要么是代码本身糟糕，要么是你对代码理解得还不够透彻。无论是哪种情况，你都需要在代码上花更多时间，所以你花在写注释上的时间并没有浪费，因为它指出了你需要做的工作。”

“好吧，”苏格拉底说。“我想不出更多问题了，而且我认为今天伊斯门把你们说得心服口服。我们会鼓励写注释，但我们不会那么天真。我们会进行代码审查，以便每个人都能清楚哪些注释真正有帮助。如果你在理解别人的代码时遇到困难，请告诉他们如何改进。”

## 32.4 高效注释的关键

> 只要存在模糊的目标、离奇的缺陷和不切实际的进度安排，就会有真正的程序员愿意投身其中并解决问题，把文档留到以后再说。Fortran 万岁！——埃德·波斯特

下面的例程是做什么的？

```
Java Mystery Routine Number One
// write out the sums 1..n for all n from 1 to num
current = 1;
previous = 0;
sum = 1;
for ( int i = 0; i < num; i++ ) {
    System.out.println( "Sum = " + sum );
    sum = current + previous;
    previous = current;
    current = sum;
}
```

你最好的猜测是什么？

这个例程计算前 num 个斐波那契数。它的编码风格比本章开头那个例程的风格稍好些，但注释是错的，如果你盲目相信注释，就会误入歧途。

这个呢？

```
Java Mystery Routine Number Two
// set product to "base"
product = base;

// loop from 2 to "num"
for ( int i = 2; i <= num; i++ ) {
    // multiply "base" by "product"
    product = product * base;
}
System.out.println( "Product = " + product );
```

这个例程计算整数 base 的整数 num 次幂。这个例程中的注释是准确的，但并未给代码增加任何信息。它们只是用更啰嗦的方式重述了代码本身。

最后一个例程：

```
Java Mystery Routine Number Three
// compute the square root of Num using the Newton-Raphson approximation
r = num / 2;
while ( abs( r - (num/r) ) > TOLERANCE ) {
    r = 0.5 * ( r + (num/r) );
}
System.out.println( "r = " + r );
```

这个例程计算 num 的平方根。代码本身不算好，但注释是准确的。

哪个例程最容易让你正确理解？这些例程没有一个是特别好的——变量名尤其糟糕。但一言以蔽之，这些例程说明了内部注释的优点和缺点。例程一有错误的注释。例程二的注释只是重复代码，因此毫无用处。只有例程三的注释物有所值。糟糕的注释比没有注释更糟。例程一和例程二与其有糟糕的注释，不如没有注释。

下面的小节将描述撰写高效注释的关键。

### 注释的种类

注释可以分为六类：

#### 重复代码

重复性注释用不同的措辞复述代码的功能。它只是让代码的读者多读一些内容，而没有提供额外信息。

#### 解释代码

解释性注释通常用于解释复杂、棘手或敏感的代码片段。在这种情况下它们是有用的，但这通常只是因为代码令人困惑。如果代码复杂到需要解释，那么改进代码几乎总是比增加注释更好。让代码本身更清晰，然后使用总结或意图注释。

下面是一种特别难以维护的注释风格：

![](img/649c8eee28c38ca1e062691e45dc9883_826_0.png)

### Microsoft Visual Basic 示例：难以维护的注释风格

```
`set up Color enumerated type
+----------------------------+
---
set up Vegetable enumerated type
+----------------------------+
---`
```

很难说每行虚线开头和结尾的加号对注释有什么价值，但很容易猜到，每次注释改变时，下划线都必须调整，以便结尾的加号位于正确的位置。如果注释跨了两行，你又该怎么办？如何对齐加号？从注释中删词让它只占一行？还是让两行长度相同？当你试图始终如一地应用这种方法时，问题会成倍增加。

一种类似动机下常见的 Java 和 C++ 指南是，单行注释使用 // 语法，较长注释使用 /* ... */ 语法，如下所示：

### Java 示例：对不同用途使用不同的注释语法

```
// This is a short comment
---
/* This is a much longer comment. Four score and seven years ago our fathers brought forth on this continent a new nation, conceived in liberty and dedicated to the proposition that all men are created equal. Now we are engaged in a great civil war, testing whether that nation or any nation so conceived and so dedicated can long endure. We are met on a great battlefield of that war. We have come to dedicate a portion of that field as a final resting-place for those who here gave their lives that that nation might live. It is altogether fitting and proper that we should do this.
*/
```

第一个注释只要保持简短，就易于维护。对于较长的注释，创建成列的双斜杠、在行间手动断行以及其他类似操作并不怎么值得，因此，对于多行注释，/* ... */ 语法更合适。

![](img/649c8eee28c38ca1e062691e45dc9883_826_1.png)

重点是，你应该关注自己如何花费时间。如果你花大量时间输入和删除横线以让加号对齐，那不是在编程，而是在浪费时间。找到一种更高效的风格。对于带加号的下划线，你可以选择只保留注释，不加任何下划线。如果你需要用下划线来强调，可以找其他方式，而不是

### 注释的最佳数量

![](img/649c8eee28c38ca1e062691e45dc9883_828_0.png)

卡珀斯·琼斯（Capers Jones）指出，IBM 的研究发现，大约每 10 条语句一条注释的注释密度，是清晰度达到峰值的密度。注释更少会使代码难以理解。注释更多也会降低代码的可理解性（Jones 2000）。

这类研究可能会被滥用，项目有时会采用这样的标准：“程序必须至少每隔五行有一条注释。”这个标准针对的是程序员没有编写清晰代码这一症状，但并没有解决根本原因。

如果你有效使用伪代码编程过程，你最终可能会每隔几行代码就有一条注释。然而，注释的数量将是该过程本身的副产品。与其关注注释的数量，不如关注每条注释是否高效。如果注释描述了代码编写的原因，并且符合本章确立的其他标准，那么你的注释数量就够了。

## 32.5 注释技术

根据注释适用的级别，可以有多种不同的注释技术：程序级、文件级、例程级、段落级或单独行级。

### 单行注释

在好的代码中，很少需要为单独一行代码写注释。以下是某行代码需要注释的两个可能原因：

-   该行代码足够复杂，需要解释。
-   该行代码曾经出现过错误，而你想留下错误记录。

以下是为某行代码写注释的一些指导原则：

#### 避免自我放纵的注释

许多年前，我听说过一个维护程序员的故事。他半夜被人从床上叫起来去修复一个出故障的程序。程序作者已经离开公司，无法联系。这个维护程序员以前从未维护过该程序，在仔细检查文档之后，他只找到了一条注释，内容如下：

```
MOV AX, 723h   ; R. I. P. L. V. B.
```

在整夜研究这个程序并琢磨这条注释后，程序员成功地打了补丁，然后回家睡觉了。几个月后，他在一次会议上遇到了程序作者，得知这条注释代表“安息吧，路德维希·凡·贝多芬。”贝多芬卒于1827年（十进制），也就是723（十六进制）。而那个位置需要 723h 这件事与这条注释毫无关系。啊啊啊！
