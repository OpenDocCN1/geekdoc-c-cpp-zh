
```
{Pascal Example Program
Input:  An integer, listlen, where listlen is less than
        100, followed by listlen-integer values
Output: The number of input values that are greater than
        the average of all input values }
program pasex (input, output);
type intlisttype = array [1..99] of integer;
var
    intlist : intlisttype;
    listlen, counter, sum, average, result : integer;
begin
result := 0;
sum := 0;
readln (listlen);
if ((listlen > 0) and (listlen < 100)) then
begin
{ Read input into an array and compute the sum }
for counter := 1 to listlen do
begin
readln (intlist[counter]);
sum := sum + intlist[counter]
end;
{ Compute the average }
average := sum / listlen;
{ Count the number of input values that are > average }
for counter := 1 to listlen do
    if (intlist[counter] > average) then
        result := result + 1;
{ Print the result }
    writeln ('The number of values > average is:',
             result)
    end { of the then clause of if ((listlen > 0 ... }
else
    writeln ('Error-input list length is not legal')
end.
```

### 2.12.2 一种可移植的系统语言：C

与 Pascal 一样，C 对先前已知的语言特性集合贡献甚少，但它在很长一段时间内被广泛使用。尽管最初是为系统编程设计的，但 C 非常适合各种应用。

#### 2.12.2.1 历史背景

C 的祖先包括 CPL、BCPL、B 和 ALGOL 68。CPL 于 20 世纪 60 年代初在剑桥大学开发。BCPL 是一种简单的系统语言，同样在剑桥开发，这次是由 Martin Richards 在 1967 年完成（Richards, 1969）。

UNIX 操作系统的第一个工作是在 20 世纪 60 年代末由贝尔实验室的 Ken Thompson 完成的。第一个版本是用汇编语言编写的。UNIX 下实现的第一个高级语言是 B，它基于 BCPL。B 由 Thompson 于 1970 年设计和实现。

BCPL 和 B 都不是类型化语言，这在高级语言中是个异类，尽管它们都比 Java 这类语言低级得多。非类型化意味着所有数据都被视为机器字，这虽然简单，但导致许多复杂性和不安全性。例如，在表达式中指定浮点运算而不是整数运算就是一个问题。在 BCPL 的一个实现中，浮点运算的变量操作数前面加句点。没有句点前缀的变量操作数被视为整数。另一种替代方案是为浮点运算符使用不同的符号。

这个问题以及其他几个问题，促使了基于 B 的新类型化语言的开发。它最初称为 NB，后来命名为 C，由 Dennis Ritchie 于 1972 年在贝尔实验室设计和实现（Kernighan and Ritchie, 1978）。C 在某些情况下通过 BCPL，在其他情况下直接受到 ALGOL 68 的影响。这可以从它的 `for` 和 `switch` 语句、赋值运算符以及对指针的处理中看出。

# 第2章 主流编程语言的演变

C 语言在其最初十五年里的唯一“标准”是克尼汉和里奇合著的那本书（1978）。在这段时间里，语言缓慢演进，不同的实现者加入了不同的特性。1989 年，ANSI 发布了 C 语言的正式描述（ANSI, 1989），其中包含了许多实现者已经加入语言中的特性。该标准于 1999 年更新（ISO, 1999）。后一个版本包含复数数据类型、布尔数据类型以及 C++ 风格的注释（`//`）。我们将长期被称为 ANSI C 的 1989 版本称为 C89；将 1999 版本称为 C99。

C 语言拥有足够的控制语句和数据结构设施，使其能够用于许多应用领域。它还提供丰富的运算符，具有高度的表达能力。

C 语言之所以既受欢迎又受诟病，最重要的原因之一是它缺少完整的类型检查。例如，在 C99 之前的版本中，可以编写参数不经类型检查的函数。喜欢 C 的人欣赏其灵活性；不喜欢它的人则认为其太不安全。在 20 世纪 80 年代，C 语言受欢迎程度大幅增长的一个主要原因是，它的编译器是广泛使用的 UNIX 操作系统的一部分。这种包含在 UNIX 中的做法提供了一款基本免费且质量相当好的编译器，可供众多不同类型计算机上的程序员使用。

```
/* C Example Program
Input: An integer, listlen, where listlen is less than 100, followed by listlen-integer values
Output: The number of input values that are greater than the average of all input values */
int main () {
    int intlist[99], listlen, counter, sum, average, result;
    sum = 0;
    result = 0;
    scanf("%d", &listlen);
    if ((listlen > 0) && (listlen < 100)) {
        /* Read input into an array and compute the sum */
        for (counter = 0; counter < listlen; counter++) {
            scanf("%d", &intlist[counter]);
            sum += intlist[counter];
        }
        /* Compute the average */
        average = sum / listlen;
    }
    /* Count the input values that are > average */
    for (counter = 0; counter < listlen; counter++)
        if (intlist[counter] > average) result++;
    /* Print result */
    printf("Number of values > average is:%d\n", result);
}
else
    printf("Error-input list length is not legal\n");
}
```

## 2.13 基于逻辑的编程：Prolog

简而言之，逻辑编程就是使用一种形式化的逻辑记号，将计算过程传达给计算机。谓词演算是当前逻辑编程语言所使用的记号。

逻辑编程语言中的编程是非过程式的。这类语言中的程序并不精确说明结果应如何计算，而是描述结果的必要形式和/或特征。要在逻辑编程语言中提供这种能力，需要一种简洁的方式，既向计算机提供相关信息，又提供用于计算期望结果的推理过程。谓词演算提供了与计算机交流的基本形式，而由 Robinson（1965）首先提出的、名为归结的证明方法则提供了推理技术。

### 2.13.1 设计过程

在 20 世纪 70 年代早期，艾克斯-马赛大学人工智能小组的阿兰·科尔默劳尔（Alain Colmerauer）和菲利普·鲁塞尔（Phillippe Roussel），与爱丁堡大学人工智能系的罗伯特·科瓦尔斯基（Robert Kowalski）一起，提出了 Prolog 的基本设计。Prolog 的主要组成部分是一种用于指定谓词演算命题的方法，以及一种受限归结形式的实现。谓词演算和归结都将在第 16 章中描述。第一个 Prolog 解释器于 1972 年在马赛开发完成。所实现的语言版本在 Roussel（1975）中有描述。Prolog 这一名称来自“programming logic”（编程逻辑）。

### 2.13.2 语言概述

Prolog 程序由语句的集合组成。Prolog 只有少数几种语句，但它们可能很复杂。

Prolog 的一个常见用途是作为一种智能数据库。这种应用为讨论 Prolog 语言提供了一个简单的框架。

Prolog 程序的数据库由两类语句组成：事实和规则。以下是事实语句的示例：

```
mother(joanne, jake).
father(vern, joanne).
```

这些语句表明 joanne 是 jake 的母亲，vern 是 joanne 的父亲。

规则语句的一个示例是

```
grandparent(X, Z) :- parent(X, Y), parent(Y, Z).
```

该语句表示，对于变量 `X`、`Y` 和 `Z` 的某些特定值，如果 `X` 是 `Y` 的父（母）且 `Y` 是 `Z` 的父（母）成立，则可以推断出 `X` 是 `Z` 的祖父（母）。

Prolog 数据库可以通过目标语句进行交互式查询，例如：

```
father(bob, darcie).
```

该查询询问 bob 是否是 darcie 的父亲。当这样的查询（或目标）提交给 Prolog 系统时，系统会使用其归结过程尝试确定该语句的真假。如果它能得出结论该目标为真，则显示“true”。如果无法证明，则显示“false”。

### 2.13.3 评价

在 20 世纪 80 年代，有相对较少的一批计算机科学家相信，逻辑编程为摆脱命令式语言的复杂性，也为摆脱生产所需的大量可靠软件这一巨大难题，提供了最好的希望。然而，到目前为止，逻辑编程尚未得到更广泛应用，主要有两个原因。其一，与其他一些非命令式方法一样，迄今为止用逻辑语言编写的程序已被证明相对于等价的命令式程序效率极低。其二，人们已确定它只对少数相对较小的应用领域有效：某些类型的数据库管理系统以及人工智能的某些领域。

有一种支持面向对象编程的 Prolog 方言：Prolog++（Moss, 1994）。逻辑编程和 Prolog 将在第 16 章中更详细地描述。

## 2.14 历史上规模最大的设计工作：Ada

Ada 语言是有史以来投入最广泛、成本最高的语言设计工作的成果。以下段落简要描述了 Ada 的演变过程。

### 2.14.1 历史背景

Ada 语言是为美国国防部（DoD）开发的，因此其计算环境的状况在决定其形式方面起了关键作用。到 1974 年，国防部计算机应用中有超过一半是嵌入式系统。嵌入式系统是指计算机硬件嵌入在其所控制或提供服务的设备中的系统。软件成本迅速上升，主要是因为系统复杂性不断增加。国防部项目使用了 450 多种不同的编程语言，且没有一种得到国防部的标准化。每个国防承包商都可以为每份合同定义一种新的、不同的语言。12 由于语言的泛滥，应用软件很少被重用。此外，也没有创建软件开发工具（因为它们通常依赖于具体语言）。当时使用的语言很多，但没有一种真正适合嵌入式系统应用。出于这些原因，1974 年，陆军、海军和空军各自独立地提议为嵌入式系统开发一种单一的高级语言。

### 2.14.2 设计过程

注意到这种广泛的兴趣，1975 年 1 月，国防研究与工程主任马尔科姆·柯里（Malcolm Currie）成立了高级语言工作组（HOLWG），最初由空军的威廉·惠特克中校（Lt. Col. William Whitaker）领导。HOLWG 有来自所有军种的代表，并与英国、法国以及当时的西德保持联络。其最初的章程是完成以下工作：

- 确定国防部新高级语言的需求。
- 评估现有语言，判断是否存在可行的候选者。
- 建议采用或实现一组最小化的编程语言。

1975 年 4 月，HOLWG 为新语言编写了 Strawman 需求文档（Department of Defense, 1975a）。该文档分发给了各军种、联邦机构、选定的工业界和大学代表，以及欧洲的相关方。

12. 这一结果在很大程度上是由于嵌入式系统广泛使用汇编语言，以及大多数嵌入式系统使用专用处理器这一事实。

The Strawman document was followed by Woodenman (Department of Defense, 1975b) in August 1975, Tinman (Department of Defense, 1976) in January 1976, Ironman (Department of Defense, 1977) in January 1977, and finally Steelman (Department of Defense, 1978) in June 1978.

After a tedious process, the many submitted proposals for the language were narrowed down to four finalists, all of which were based on Pascal. In May 1979, the Cii Honeywell/Bull language design proposal was chosen from the four finalists as the design that would be used. The Cii Honeywell/Bull design team in France, the only foreign competitor among the final four, was led by Jean Ichbiah.

In the spring of 1979, Jack Cooper of the Navy Materiel Command recommended the name for the new language, Ada, which was then adopted. The name commemorates Augusta Ada Byron (1815–1851), countess of Lovelace, mathematician, and daughter of poet Lord Byron. She is generally recognized as being the world’s first programmer. She worked with Charles Babbage on his mechanical computers, the Difference and Analytical Engines, writing programs for several numerical processes.

The design and the rationale for Ada were published by ACM in its SIGPLAN Notices (ACM, 1979) and distributed to a readership of more than 10,000 people. A public test and evaluation conference was held in October 1979 in Boston, with representatives from over 100 organizations from the United States and Europe. By November, more than 500 language reports had been received from 15 different countries. Most of the reports suggested small modifications rather than drastic changes and outright rejections. Based on the language reports, the next version of the requirements specification, the Stoneman document (Department of Defense, 1980a), was released in February 1980.

A revised version of the language design was completed in July 1980 and was accepted as MIL-STD 1815, the standard Ada Language Reference Manual. The number 1815 was chosen because it was the year of the birth of Augusta Ada Byron. Another revised version of the Ada Language Reference Manual was released in July 1982. In 1983, the American National Standards Institute standardized Ada. This “final” official version is described in Goos and Hartmanis (1983). The Ada language design was then frozen for a minimum of five years.
