# C 笔记：C 编程语言指南





## 前言

C 是一门正在迅速流行的语言。从贝尔实验室默里山分部阁楼中的悄然起步，它已经传播到全世界数百种机器上；而这一切几乎没有依靠任何销售努力。

C 可以被描述为一种可实现的 Algol 68，一种不怕弄脏双手的 Pascal，或者干脆是一门满足系统级程序员需求的优雅小巧的语言。这些说法都没有完整刻画出它在纯粹性和实用性、可移植性和效率之间精心达成的平衡的全部要义。

C 语言的设计目标是以最少的形式提供最大的功能。本书旨在为这门语言提供一份指南，一份形式上精确、同时也不回避阐明实现依赖和语义特殊性中那些晦暗角落的指南。它不是教程——没有人能与 Kernighan 和 Ritchie 的《C 程序设计语言》相比——也不是正式定义：他们那本书的附录 A 已经足以承担这一任务。相反，它填补了两者之间的中间地带，提供一种与贝尔实验室视角不同的 C 语言视角。随着实现不断增多，这种更广阔的视角将变得越来越重要。

这是一本按二维结构组织的书。各章节覆盖语言的主要方面：

- 0. 语法
- 1. 外部声明
- 2. 初始化器与语句
- 3. 表达式
- 4. 局部声明
- 5. 参数化
- 6. 库例程
- 7. 机器相关性

每一章由八个节组成，逐一考察各种数据类型：

- .0 引言
- .1 整数
- .2 浮点数
- .3 指针
- .4 数组
- .5 结构体与联合体
- .6 函数
- .7 小结

想快速了解这门语言，可以阅读各章的 .0 节；想获得精确的总结，则阅读 .7 节。任何与某一主题相关的特殊内容，例如指针，都能在 .3 节找到；指针表达式也一定会在第 3 章 .3 节讨论，简称 [3.3]。

本书所述语言与丹尼斯·里奇在上述附录 A 中公布的技术规范高度一致。不过需要强调的是，尽管 C 仍然相当纯粹，现有编译器却没有一款能完全精确地符合该规范。

## 0：语法

> > 您在读什么，大人？
>
> > 词，词，词。
>
> > ——莎士比亚，《哈姆雷特》

C 编程语言由语言定义、实现和运行时环境组成。语言定义所描述的是与任何特定机器特性无关的 C；实现则努力在某种真实计算机上落实该定义；相应的运行时环境则弥补实现或机器上的任何不足，从而以足够保真度模拟一台 C 机器，以满足语言定义的要求。

C 是一门与机器无关的语言，它试图对大多数现代计算机的基本运算符和操作数进行建模。正因如此，C 能够被翻译成在各种机器上高效且紧凑的代码，但这要以语言定义中一定程度的非确定性为代价。因此，有必要偶尔强调 C 程序中那些可能因不同实现而有所差异的方面；而且，了解哪些行为仅通过修改运行时支持包就能加以控制，也往往很有用。

本书将主要关注 C 语言与机器无关的定义，因为那是它最具可移植性的方面。但务必记住，C 是通过编译器实现的，


也就是说，一个用 C 语言编写的程序，它读取用 C 语言编写的程序并输出汇编语言语句来实现源代码的意图。汇编器将这些语句翻译成目标模块，即一组指令提供给装载器，装载器实际构造可执行程序。装载器可能会将目标模块与其他单独编译和/或汇编的模块组合起来，并且它可以利用运行时支持例程库来完成程序。C 编译器施加的许多武断限制，仅仅反映了大多数汇编器和/或装载器的共同不足。

C 程序是一组一个或多个文本文件——每个文件可以是，例如，纸带或卡片组或用文本编辑器准备的在线文件。它由任意长度的行组成，每行都以一个特殊字符代码结尾，称为换行符（ASCII linefeed）。如果需要，运行时环境会将标准文本文件翻译成编译器的这种内部格式，以便在不同的操作系统和机器上以统一的方式实现行的概念。例如，一张卡片映像可能会变成 81 个字符的行，其中包括终止的换行符。

这里有一个不无道理的 C 程序：

```
/* copy input to output
*/
main()
{
    int c;
    c = getchar();
    while (c != -1)
    {
        putchar(c);
        c = getchar();
    }
}
```

这声明 main 为一个函数，无参数调用，其主体是花括号内的文本。主体声明 c 为仅函数内部已知的整型变量，并包含若干可执行语句，这些语句反复调用其他函数 getchar 和 putchar，直到 c 被赋值为 -1。事实证明，这些其他函数在运行时库中可用（参见 [6.01]）；除此之外它们并没有什么神奇之处。

显然，需要更多的解释，但这必须分散在几章中。目前，重点必须放在 C 程序的构建块上，它是如何表达的，以及它处理的基本数据。在最低层，它由各种标识符或名称组成，穿插着字面量、标点符号和空白字符，例如空格和制表符。

C 程序使用完整的 94 个可打印 ASCII 字符集编写（参见 [7.1]）。可打印字符的连续字符串根据各种词法规则被归并为标记。所有不可打印字符，包括换行符，都是空白字符，用于分隔可能否则会被合并在一起的相邻标记。还有注释，即以 /* 开始并以 */ 结束的任意字符字符串，其行为与空白字符非常相似。尽管语言对空白字符或注释的使用施加了很少的限制，但必须谨慎且统一地使用两者，以使源代码尽可能易读。

标识符是字母、数字和下划线字符 _ 的任意长度字符串，以字母或下划线字符开头。前一页所示的 C 程序包含标识符 main、int、c、getchar、while 和 putchar。由装载器使用的名称（参见 [7.0]）必须在前五个左右字符上有所不同（取决于特定的装载器）才能区分；内部使用的名称必须在前八个字符上有所不同。有些装载器拒绝区分大写和小写字母。标识符通常由用户创建来命名数据项和函数。

某些标识符是预定义的关键字，每个关键字在语言中都有特殊含义；它们不得被重新定义。在上面的示例中，int 和 while 是关键字。关键字的完整列表可在 [0.7] 中找到。由于在完整 ASCII 中小写字母和大写字母是不同的，因此 INT 不是关键字，Int 也不是。支持仅大写设备的安装必须在输入到编译器时转换为小写，并在输出时可能转换回大写。

类型可以分为 *基本*（整数和浮点）与 *派生*（指针、数组、结构体、联合、函数），或 *标量*（基本类型加指针）与 *复合*（数组、结构体、联合、函数）。

类型摘要将在 [0.7] 中给出。

### 0.1 整数

*整数* 是 C 程序的主力。它们用于计数，用于选择数组元素，用于表示文本字符、逻辑值和位序列，以及任何在幅度范围已知有限且不需要分数结果的算术运算。整数以多种方式实现也就不足为奇了。

基本整数可以表示为二进制数据，尽管语言中并没有关于算术是采用一的补码、两的补码、符号幅度还是某种更奇特的编码的假设。C 中的整数始终至少与目标机器上的地址一样大；它们可以无限制地用作下标或指针修饰符。

短整数可以用于计数数千的事物，以期实现存储经济性。然而，并不能保证短整数实际上会比基本整数更短。同样，长整数用于计数数亿的事物；它们也可能不比基本整数更长。

无符号整数通常与基本整数大小相同，在算术上行为也基本相同，只是它们的值始终被视为零或正数。在两的补码计算机上，这相当于将符号位视为另一个幅度位。它们的主要用途与其说是为了用正数加倍计数范围，不如说是为了允许与地址处理兼容的算术运算，在这些机器上地址占据一个整数大小的字。

最后，C 提供了一个 *字符* 类型，保证足够大以容纳机器字符集中的任何元素。字符在算术表达式中使用时表现得像非常小的整数，但不能保证负数在转换为字符再转换回整数时能够存活，无论它们有多小。可以安全地假设可打印字符表现得像小的正数。

到目前为止的讨论对实际数据大小避而不谈，而且是有意为之。C 确实知道 *字节*，按通常的机器意义，甚至在较小程度上知道 *位*。关键在于，允许实现大小有相当大的变化，以便 C 可以在 Intel 8080 或 IBM 370 上高效运行。所有真正承诺的内容都已在上面的段落中总结。

大多数现代计算机具有八位 *字节*，支持 *字节* 的倍数数据类型，并在两的补码中执行整数算术。在这样的机器上，可以可靠地期望字符适合一个字节，整数适合两个到四个字节。因此，字符可能容纳范围为 −128 到 +127 的数字，或许 0 到 255；双字节整数为 −32,768 到 +32,767 有符号，或 0 到 65,535 无符号；四字节整数为 −2,147,483,648 到 +2,147,483,647 有符号，或 0 到 4,294,967,295 无符号。地址的大小，以 *字节* 计，将很好地表明基本整数是在该范围的短侧还是长侧。当然，*所有* 整数都是四字节长是完全合法的。

一个好的程序将尽可能少地对目标机器的性质做出硬性假设，以最大化可移植性并最小化神秘常量。为了帮助可移植性，C 提供了一种确定任何数据类型的大小的机制，以 *字节* 表示，以便代码能够正确参数化。sizeof 运算符在 [3.1] 中描述。

整数字面量可以用几种不同的方式表示。每种形式和值都暗示了某种最小长度，以 *字节* 计，这可能会影响它在表达式中的使用方式，尽管实现可能使用比所需更长的版本。



任何以非零数字开头且仅由数字组成的字面量被视为 *十进制* 整数。 其长度为能够将其表示为正确值的 *正* 数的最小实现类型。

以数字零 0 开头且仅由数字组成的字面量被视为 *八进制* 整数。数字八 8 被视为八进制 10，数字九 9 被视为八进制 11。字面量的长度为能够将其表示为正确值的 *无符号* 数的最小实现类型。

以数字零后跟 x 或 X 开头的字面量被视为 *十六进制* 整数。字符 a 到 f，或同样地 A 到 F，被视为十六进制数字，其值分别为十到十五。字面量的长度为能够将其表示为正确值的 *无符号* 数的最小类型。

以单引号 ' 开头的字面量被视为 *字符* 整数。所有字符，包括空白，直到下一个单引号都被视为字面字符，用来定义整数的值。单个字符的长度为字符数据项的长度，其值等于目标机器上该字符的内部表示。附加字符按未指定的顺序连接，得到的长度是单个字符的适当倍数。

某些不可打印或难以获得的字符可以用 *转义序列* 表示，例如 \n 表示换行或 \' 表示单引号，因为这些在字符串中否则无法出现。任意代码可以用 \nnn 指定，其中 nnn 为一到三个八进制数字。请注意，所有这些转义序列在常量中都简化为单个字符。字符转义序列的完整列表可在 [0.7] 中找到。如果需要在下一行继续字符字面量，可以在换行符前直接使用转义 \ 来使其失效。

尽管有如此多的自由，谨慎的做法是严格限制字符字面量。包含多个字符的字面量极度依赖机器，而包含不可打印字符的字面量难以检查。应使用转义序列使所有代码可见，并应避免行续接。

而且，虽然字符字面量确实是整数，可以自由地在整数表达式中使用，最好不要假定任何特定的数值或范围，因为两者都可能因机器而异。字符字面量应主要用于输出或与字符数据进行精确比较。

任何整数字面量都可以在其后附加修饰符 I 或，更可取的是 L。 这强制长度为长整数的长度，无论其数值如何。如果任何整数字面量即使作为长整数也太长而无法正确表示，则将其视为长整数并在左侧截断。符号发生的情况取决于机器。

### 0.2 浮点数

浮点数有两个要素：指数和分数部分。 其值被解释为分数部分与某个预定义基数以指数为幂的乘积。 至少一种指数和分数部分的编码用于表示零值。 浮点数可以被视为对实数集的近似，其范围远大于整数的范围。

浮点运算可以在这个大范围内保持固定的精度，但代价是极大整数或连分数的表示不精确。 太大而无法正确表示为浮点的数称为溢出；太小的数下溢，通常被放大为零。 减去两个量级几乎相等的数可能导致精度损失，从而只能得到所需结果的粗略近似。

尽管存在这些缺点，浮点运算在数值计算中如此流行，以至于大多数现代计算机都用硬件指令支持某种版本。 结果是舍入、截断还是更随意地近似在不同机器之间差异很大。 因此，C 对浮点运算的详细属性几乎没有说明。

然而，该语言确实提供了数据类型 *浮点* 和 *双精度*。 尽管名称如此，并不能保证双精度浮点数的分数部分比基本浮点数据长一倍。 它通常比两倍长，但也可能不比 float 长。 也不能保证任何特定长度的整数可以扩展为 float 然后转换回具有相同值的整数，即使双精度表示被认为保留了所有算术类型中最多的信息。

在大多数机器上，浮点数据以四到八个字节表示，其中固定部分用于表示指数。 二进制计算机中的隐含基数通常是二或十六； 量级通常至少达到十的 38 次方； 分数部分保留六到十六位十进制精度的数字。

浮点字面量是以十进制数字或小数点开头的标记。 它们可能包含小数点、分数部分和指数部分，其中指数部分由字符 e 或 E、可选的加号或减号以及将剩余数字相乘的十进制十的幂组成。 整数部分或分数部分可以省略，但不能同时省略； 小数点或指数可以省略，但不能同时省略。 浮点字面量的任何部分之间不得出现空白。

双精度字面量没有特殊表示法，但会保留足够的精度以在上下文需要时生成双精度常量。 精度足够指定的字面量始终会被视为双精度。 浮点字面量的默认类型在 [3.2] 中讨论。

### 0.3 指针

*指针* 是用于定位其他数据项的数据项。 在最简单的实现中，指针仅保存指向的数据项的机器地址； 但原则上它可以保存更复杂的结构，例如字地址加上字节偏移，或引用计数以便于有效性检查和垃圾回收。 指针至少必须足够大以容纳程序中可用的最大机器地址。

重要的是，指针的特征在于它们指向的事物类型； C 中没有指向未指定类型的指针。 指向不同类型事物的指针可能具有不同的格式； 几乎肯定它们可能取值的约束不同。 然而，对于所有指针，都定义了一个空值，可与 C 中任何对象的地址区分，指针在不指向适当类型的当前实例时可以取该值。

在 C 中允许有指向任何类型对象的指针，包括指向其他指针，递归地无穷无尽。 它们在编程的许多方面自然出现，但在对象本身不应或不能直接传递的上下文中特别有用。 例如，将指针的副本传递给某个函数比复制整个数组或数据结构要容易得多。 而且，除非指针可用于代表子列表，否则无法表示某些列表结构： 例如，考虑一个循环列表，其中每个元素都在其自己的子列表中。

指针也可能被滥用，因为它们引入了一层间接性，使可读性变差，并且它们提供了在编译时彻底检查或在运行时高效检查几乎不可能的编程自由度。 C 在使用指针方面允许相当大的自由度，以牺牲甚至一些容易执行的检查为代价。 因此，应特别谨慎地使用它们。

语言本身没有指针字面量。 然而，有保证所有有效指针都有非零值，因此整数零可以作为字面空值。 此外，整数可以在多种上下文中用于初始化指针，尽管这种做法极度依赖机器。

### 0.4 数组

C 中任何已知大小的对象也可以以多重形式出现，称为数组。 与指向某物的指针一样，数组始终是某种其他类型的，尽管该类型也可以是其他类型的数组。 没有对维度的显式限制

数组就像指针链一样，其长度没有限制。指向整数数组的指针的数组的数组是完全可以接受的。

数组还由其起始地址和包含的元素数量（即其重数）来表征。前者由其存储类别决定，并且必须具有对与数组元素类型相同对象的指针合法的值。在此意义上，数组的起始地址可以被视为一个字面指针。

C 没有提供变长数组的支持，尽管程序当然可以自由使用数组中少于全部重数的元素。这意味着在许多上下文中，必须在引用数组之前确定元素数量，并且数组中存储的信息仅限于其所有元素的当前值。在确定重数时允许一定的灵活性，因此编译器通常可以自行计数，而不是让程序员负担。数组的重数为零是非法的。

重数未确定的数组不是“已知大小的对象”，因此不能构成其他数组或在另外一两个上下文中使用。也不允许形成函数数组，或内容未确定的结构数组。

存在一种字面数组。以双引号 " 开始的字面量被视为字符字符串，或字符数组。双引号之后的所有字符，包括空白，直到下一个双引号，都被视为字符整数，定义字符数组的后续元素。每个字符串都会附加一个空字符 \0，因此字符字符串的重数至少为一个，如 ""，它是空字符串。

在 [0.1] 和 [0.7] 中为字符整数定义的相同转义序列在字符串内部也可使用。特别是，\" 是一个字面双引号，\\ 是一个字面反斜杠，而 \ 换行会将字符串继续到下一行。有关字符整数的风格规则也应适用。

### 0.5 结构体和联合体
经常需要将不同类型的数据项组合在一起，因为这些项密切相关。输入输出记录是聚合的一个典型例子，复数也是如此。前者是字符数组，但这掩盖了特定子字段中字符之间的关系。同样，后者如果忽略两个字段处理的非对称性，可以被视为一个双元素浮点数组。然而，更为通用的是提供任意类型的聚合；这就是 C 中数据结构的用途。

任何已知大小的对象都可以收集到一个结构体中，包括指针、数组或其他结构体。结构体由其元素的顺序和类型定义；两个结构体只有在其对应元素具有相同类型且按相同顺序排列时才匹配。关于结构体的组成信息不会与其一起存储，只有每个元素的数值。

程序文本中可能存在某个结构体在内容定义之前就可以被引用的区域。在此区域中，该结构体不是已知大小的对象，因此不能构成数组或其他结构体。

人们很容易认为结构体的大小是其每个元素大小的总和，但这是天真的。许多现代计算机对某些数据类型在存储中的放置有一些限制。例如，四字节浮点数据可能要求其机器地址能被四整除。因此，每个数据类型不仅以字节大小为特征，还以其存储边界限制的严格程度为特征。

结构体内部明显的考虑是，一个元素可能无法紧跟在前一个元素之后放置——可能会出现空洞，其大小和位置取决于机器。同样明显的是，结构体本身必须对齐到至少与其中最受限制元素所需一样严格的存储边界上。因此，例如，如果一个四字节浮点数跟在一个字符之后，就可能需要引入一个三字节的空洞。如果浮点数要求从偶地址开始，如 PDP-11 中那样，则会出现一个一字节的空洞。

## 0：语法
更微妙的要求是，结构体必须结束于至少与开始时一样受限制的边界上。这是为了确保结构体数组的后续元素也能满足所有边界要求。因此，结构体甚至可能在末尾有一个空洞，姑且这么说。

没有结构体字面量。

数据结构的一个近亲是类型的联合体。联合体经常出现在程序中需要在同一存储位置放置多种类型数据的地方。经常重叠利用了所用不同类型大小的已知相似性，以及可能在如何移动它们方面的相似性；这极度依赖机器。像使用数组来表示结构体一样，这也可能具有误导性。

任何已知大小的对象都可以收集到一个联合体中，其大小足以容纳其最大元素，或其边界限制与最严格元素的边界限制一样严格。像结构体一样，联合体也可能被填充以使其结束于必须开始的同一边界上。与结构体不同，在任何给定时刻，联合体内部只能存在所选元素之一。关于联合体的组成或其当前内容的类型的任何信息都不会与其一起存储——只有其中一个元素的值。

因此，联合体主要用于告知实现一种很可能依赖机器的做法，以便编译器能够满足所选目标机器的最低要求。

没有联合体字面量。

### 0.6 函数
函数是 C 的可执行实体。它们可能代表要执行的复合操作，或调用一个或多个参数的数学函数计算。

每个 C 程序必须始终包含一个名为 main 的函数，其单次执行定义了程序的执行。这样的程序已在 [0.0] 中描述。

正如指针总是被声明为指向某个已知类型，函数总是被声明为返回某个类型，即使没有明确提及类型（参见 [1.6]），没有显式返回值 [2.6]，或从未使用返回值 [3.6]。函数只能返回标量类型，即整数、浮点数或指针。

函数参数按值传递，即每次调用函数时都会为每个参数制作一份新副本，函数可以随意更改这些私有副本。与返回值一样，只能传递标量类型作为参数（但参见 [3.4, 3.5, 3.6] 中非标量到标量的隐式强制转换）。

尽管一个有效的 C 程序可以仅由 main 函数组成，通常会将 main 所需的许多活动委托给其他函数，并继续这一过程直到所有函数都达到可管理的大小。main 及其从属函数之间的通信通常通过参数列表以及可能返回的结果来完成。在其他情况下，函数可以通过对全局已知变量的共同访问隐式通信，尽管这会导致程序可读性降低。

以下三个名为 main、newnum 和 printd 的函数说明了主要可能性：

```c
int c; /* globally known current input character */
main() /* read, convert, and print number */
{
    int number;
    c = getchar();
    number = 0;
    while (isdigit(c))
    {
        number = newnum(number);
        c = getchar();
    }
    printd(number);
}
```

```c
int newnum(n)    /* fold digit c into n */
    int n;
    {
    return (10 * n + (c - '0'));
    }
```

```c
printd(n)    /* print n as decimal */
    int n;
    {
    int quot, rem;
    quot = n / 10;
    rem = n % 10;
    if (quot != 0)
        printd(quot);    /* recursive call */
    putchar(rem + '0');
    }
```

在这个例子中，main、newnum 和 printd，以及一个全局整型变量 c，保存刚从输入读取的当前字符。函数 main 使用一个库函数 getchar 和另外三个函数来履行职责。其中两个函数已在此定义；isdigit 尚待定义。

函数 newnum 根据显式标明的参数 n 和隐式全局参数 c 执行计算；由于 newnum 返回整型结果，因此它是在 main 中的某个表达式内部被调用的。然而应当强调，在大多数情况下，这种将 c 传给函数 newnum 的方法是很不可取的。

函数 printd 不返回值；调用它是为了执行其动作，即在输出介质上打印一串数字。因此，从 main 对 printd 的调用以语句形式出现，而不是出现在表达式内部。即使 printd 被定义为返回结果，main 中的调用仍然合法，但返回值会被丢弃且永远不会使用。这个函数与其他函数的不同之处在于，它通过调用 printd(quot) 将某些职责委托给自身。这类递归调用在 C 中通常是允许的，但程序员必须小心避免无限递归。

函数不是具有已知大小的对象，因此不能组合进数组、结构或联合。然而，指向函数的指针完全可以这样使用。

不存在字面函数值，尽管形式参数和函数体实际上等同于字面函数值。这些主题在 [2.6] 节中有更详细的讨论，该节涉及函数初始化器。

### 0.7 语法摘要

一个正确构成的 C 程序由一系列记号组成，这些记号以非常精确的方式组成短语。规定所有正确构成的 C 程序集合的规则称为语法。每条规则通过规定从基本记号和其他短语构造某个短语的所有可能方式，来定义该特定短语名的含义。第一条规则将短语“C 程序”定义为一个或多个程序文件的序列，写作：

```
C-program = { program-file }
```

花括号表示一次或多次出现。

另一条规则将类型定义定义为关键字 typedef，后跟类型说明符，再跟声明符列表，最后跟记号 ;。

这条规则写作：

```
type-definition =
    typedef type-specifier declarator-list ;
```

短语“类型说明符”由以下规则定义：

```
type-specifier =
    [ integer-type | floating-type
    | type-name | structure-or-union-type ]
```

这意味着从四个备选项中择一。下标 opt 表示可选出现，因此

```
floating-type =
    [ short_opt double | long_opt float ]
```

表示关键字 double，其前面可能有 short，或者表示 float，其前面可能有 long。偶尔使用圆括号将可选出现的短语序列分组，如下所示：

```
( else statement )_opt
```

C 的关键字和其他字面记号使用粗体，而短语名使用斜体并带有内嵌连字符。任何形如 anything-list 的短语名，都是表示一个或多个 anything 类短语的逗号分隔序列的缩写。其形式含义可由以下模式给出：

```
anything-list = anything [, anything]opt % this is a comment
```

如上所示，语法注释可以插入形式语法规则中，位于百分号之后、下一个换行之前。

有时，可选选择中的某个备选项会带有下标 def，表示如果该短语缺失，其解释就完全等同于显式给出了该选择。这种隐式选择称为默认值。C 中的一个典型例子是

```
/auto_def | static | extern | register/opt
```

以下规则规定 C 程序记号的词法格式：

```
identifier =
[ letter | _ ] [ letter | _ | digit ]opt

keyword =
/auto | break | case | char | continue
| default | do | double | else | extern
| float | for | goto | if | int | long
| register | return | short | sizeof | static
| struct | switch | typedef | union
| unsigned | while /

comment =
/* character-sequence-not-containing-asterisk-slash */

integer-constant =
[ decimal-constant | octal-constant
| hexadecimal-constant | character-constant ]
```

decimal-constant = nonzero-digit { digit }opt

octal-constant = 0 { digit }

hexadecimal-constant = 0 ( x | X ) { hex_digit }

hex-digit = / digit | a | b | c | d | e | f | A | B | C | D | E | F /

floating-constant = / decimal-constant | 0 . decimal-constant exponentopt | . decimal-constant exponentopt | decimal-constant exponent /

fraction = . decimal-constant

exponent = [ e | E ] [ + | - ]_opt decimal-constant

character-constant = ' { character-literal } '

string = " { character-literal } "

character-literal = / character-other-than-'-or-\-or-' | \b % backspace | \n % newline | \r % carriage return | \t % tab character | \ % backslash | \' % ' | " % " | \% % | \octal-digit | \octal-digit octal-digit | \octal-digit octal-digit octal-digit /

punctuation = / ( { ) % grouping and association | [ ] % array subscripts | { } % initializers and compound statements | ; % separators and terminators | ? : % conditional expressions /

```
operator =
{ arithmetic-operator
| bitwise-operator
| parts-selection-operator
| dereferencing-operator
| location-operator
| logical-operator
| augmentation-operator
| relational-operator
| equality-operator
}

arithmetic-operator = { + | - | * | / | % }

bitwise-operator = { & | ^ | << | >> | ~ }

parts-selection-operator = { . | -> }

dereferencing-operator = *

location-operator = &

logical-operator = { && | || | ! }

augmentation-operator = { ++ | -- }

relational-operator = { < | > | <= | >= }

equality-operator = { == | != }
```

## 1：外部声明

> “当我使用一个词时，”矮胖子以相当轻蔑的语气说，“它恰恰意味着我选择它意味着的东西——不多也不少。”
> 
> ——刘易斯·卡罗尔，《爱丽丝镜中奇遇记》

一个 C 程序由一个或多个分别编译的文件组成的序列构成。一个程序文件是函数声明、类型定义和数据声明的序列。以下规则更形式化地规定了这一点：

```
C-program = { program-file }

program-file = { function-declaration | type-definition | data-declaration }
```

重要的是要认识到，C 程序不过是处于最外层或外部层次的声明，而该语言中的所有表达式都仅仅用作某个正在被声明项的初始化器。

进一步描述这些外部（或全局）声明形式的语法和含义，是本章的任务。用最简单的话说，声明引入某个变量，并将各种属性与其关联。

处理常量的程序通常没有太大用处；因此，变量概念对大多数编程语言都具有重要意义，C 也不例外。

简单变量是由名称和对象组成的一对；名称是程序员指定要操纵哪些对象所需的标识符，而每个对象由位置（通常是计算机地址和大小）、类型以及存储在该位置上的该类型的一个特定值组成。

之所以要如此小心地使用术语，是因为后面遇到指针和复合类型时，会出现名称表达式更复杂的变量，而众所周知的赋值语句的语法和含义将需要仔细考虑。该语言中还有一个运算符可给出变量的位置，从而使计算机地址成为可操纵的值。正确理解指针也必须建立在清晰理解变量之上。

外部声明宣告某些名称具有程序员所期望的属性。例如，

```
int i;
long float x;
```

赋予名称 i 以“整型变量”的属性（实现会处理实际位置），而 x 成为双精度浮点类型的变量。

除了类型之外，声明还可以指定存储类属性和初始化器。初始化器将在第 2 章介绍。存储类如果存在，必须写在最前面：

```
static int i;
extern long float x;
```

存储类由关键字 extern、static、auto 和 register 指定；typedef 说明符在语法上像存储类一样起作用，但它不会将名称与对象关联。

C 程序文件中的每个外部声明的名称都具有外部属性或静态属性，分别由关键字 extern 和 static 表示，其中外部属性是默认值。外部名称在所有程序文件中可见，这种机制允许分别编译的程序文件之间通信。静态名称在包含它的程序文件的其余部分中可见，但不能更广泛地可见。使用单独的程序文件并限制外部属性的使用，可以提供某些语言所不提供的模块化和保护。




Globally declared variables have a lifetime that endures for as long as the main program executes regardless of their visibility attribute (external or static).

全局声明的变量的生命周期持续整个主程序的执行时间，不受其可见性属性（外部或静态）的影响。

Sections [1.1] through [1.5] deal with the various kinds of data-declarations, so it is appropriate to introduce the formal syntax rules here:

各节 [1.1] 至 [1.5] 讨论各种数据声明，因此在此引入形式语法规则是合适的：

```
data-declaration =
  /extern_def/ | static_opt
  type-specifier_opt initializable-declarator-list_opt ;

type-specifier =
  [ integer-type | floating-type
  | type-name | structure-or-union-type ]

initializable-declarator =
  declarator initializer_opt
```

Function-declarations will be covered in [1.6], and type-definitions at the end of the chapter, in [1.7].

函数声明将在 [1.6] 中介绍，类型定义则在该章末尾的 [1.7] 中介绍。

### 1.1 Integer declarations

### 1.1 整数声明

An external integer declaration is a data declaration with a type specifier of the flavor integer type:

外部整数声明是一种数据声明，其类型说明符为整数类型：

```
integer-type =
  { char | unsigned | short | long }_opt int_def
```

and declarators that are identifiers. The declaration

并且声明符为标识符。声明

```
int number, smallest, largest;
```

makes number, smallest, and largest the names of three integer variables, which are externally visible by default. Any subsequent reference to one of these names will deliver its current value or cause replacement of its current value by a new value, depending on the context in which the name occurs.

使 number、smallest 和 largest 成为三个整数变量的名称，默认情况下它们是外部可见的。对这些名称中任何一个的后续引用将返回其当前值，或根据名称出现的上下文用新值替换其当前值。

These integer variables can participate as operands of integer operators, as described in [3.1]. The various flavors of integer type were explained in [0.1].

这些整数变量可以作为整数运算符的操作数参与运算，如 [3.1] 中所述。各种整数类型的变体已在 [0.1] 中解释。

If any of the adjectives short, unsigned, or long is present, int is assumed and may be omitted. In any context calling for an optional type specifier, the default type is taken as int. It is good practice, however, to explicitly type all declarations.

如果存在 short、unsigned 或 long 等形容词，则假定为 int 并且可以省略。在任何需要可选类型说明符的上下文中，默认类型被视为 int。然而，显式为所有声明指定类型是良好的实践。

### 1.2 Floating declarations

### 1.2 浮点声明

An external floating declaration is a data declaration with a type specifier of the flavor floating type:

外部浮点声明是一种数据声明，其类型说明符为浮点类型：

```
floating-type = / short | double | long | float /
```

and declarators which are identifiers. For example,

并且声明符为标识符。例如，

```
static long float x;
float y;
```

makes x the name of a floating variable of long precision, visible only in the enclosing program file, and y an externally visible single-precision floating variable. They may participate in expressions much as integers do, but with slightly different meaning attached to the operators. The operators relevant to floating variables are described in [3.2].

使 x 成为长精度的浮点变量的名称，仅在包含的程序文件中可见，而 y 是一个外部可见的单精度浮点变量。它们可以像整数一样参与表达式，但运算符的含义略有不同。与浮点变量相关的运算符在 [3.2] 中描述。

### 1.3 Pointer declarations

### 1.3 指针声明

An external pointer declaration is a data declaration with any flavor of type specifier and a declarator of the form

外部指针声明是一种数据声明，其类型说明符可以是任何类型，声明符形式为

```
*declarator
```

For example,

例如，

```
int *ptr_to_int;
struct item **ptr_to_item;
```

declares ptr_to_int as the name of a variable of type pointer to integer and ptr_to_item as a variable of type pointer to a struct item. The structured type struct item is a composite type whose definition presumably occurs elsewhere, but note that the content of the structure need not be known to declare a pointer to it.

声明 ptr_to_int 为指向整数的指针类型变量的名称，ptr_to_item 为指向 struct item 的指针类型变量。结构类型 struct item 是一个复合类型，其定义可能在其他地方出现，但请注意，声明指向它的指针不需要知道结构的内容。

Recalling the earlier definition of variable, the unique aspect of a pointer variable is that its class of admissible values ranges over the locations (machine addresses) of other values of the type to which the pointer variable is specified to point.

回顾变量的早期定义，指针变量的独特之处在于其可接受值类涵盖了指针变量指定指向的类型值的其他值的存储位置（机器地址）。

The use of these variables will be described subsequently in several chapters.

这些变量的使用将在后续几章中描述。

### 1.4 Array declarations

### 1.4 数组声明

An external *array declaration* is a data declaration with any type specifier and a declarator of the form

外部 *array declaration* 是一种数据声明，其类型说明符可以是任意类型，声明符形式为

`identifier [ constant-expr_opt ]`

The *constant-expr* must be a positive integer constant, calculable at compile-time, and defines the multiplicity N of the array. The valid subscripts range from 0 to N−1. For example,

*constant-expr* 必须是一个正整数常量，可在编译时计算，并定义数组的重复次数 N。有效下标范围从 0 到 N−1。例如，

`float point_3d[3];`

declares *point_3d* as an array variable consisting of three subvariables *point_3d[0]*, *point_3d[1]*, and *point_3d[2]* each of type *float*. The expressions *point_3d[2]*, *point_3d[1]*, and *point_3d[0]* are *variable-name-exprs*, each of which refers to one of the three floating variables making up the composite floating array variable *point_3d*.

声明 *point_3d* 为一个数组变量，由三个子变量 *point_3d[0]*、*point_3d[1]* 和 *point_3d[2]* 组成，每个子变量的类型均为 *float*。表达式 *point_3d[2]*、*point_3d[1]* 和 *point_3d[0]* 都是 *variable-name-exprs*，每个表达式都引用组成复合浮点数组变量 *point_3d* 的三个浮点变量之一。

The *constant-expr* specifying array size may be omitted when an initializer is present and the size is implied by the number of values supplied. Initializers for arrays are discussed in [2.4]. It also is permissible to omit the size when declaring the existence of an array that is defined elsewhere, perhaps in another program file. It is possible to declare variables that are arrays of arrays, and so on, as in

指定数组大小的 *constant-expr* 在存在初始化器且大小由提供的数值数量隐含时可以省略。数组的初始化器在 [2.4] 中讨论。当声明在其他地方定义的数组的存在时，例如在另一个程序文件中，省略大小也是允许的。可以声明数组的数组等变量，如

`char page[50][80];`

which makes *page* the name of an array variable composed of 50 like variables of size 80 characters. Then *page[0][0]* and *page[49][79]* denote the northwest and southeast corners, respectively. When a declaration contains array of array, and so forth, only the first size specification may be omitted, for otherwise the contained arrays would not be objects of known size.

使 *page* 成为一个数组变量的名称，由 50 个大小为 80 个字符的相似变量组成。此时 *page[0][0]* 和 *page[49][79]* 分别表示西北角和东南角。当声明包含数组的数组等时，只能省略第一个大小说明，否则包含的数组将不是已知大小的对象。

The character strings described in [0.4] are literal arrays of characters and behave like *char* array names, except when used as initializers of named *char* arrays. For example, the string "C-compiler" really acts like the secret declaration `_string1` where `_string1` has been predeclared by

[0.4] 中描述的字符字符串是字符的字面数组，其行为类似于 *char* 数组名称，除非用作命名 *char* 数组的初始化器。例如，字符串 "C-compiler" 实际上等同于秘密声明 `_string1`，其中 `_string1` 已被预声明为

`static char _string1[] = "C-compiler";`

The `_string1` implies that the name generated for the string is not specifiable by the programmer, so there can be no conflicts with string names secretly created by the compiler. See [2.4] for more on this.

`_string1` 意味着为字符串生成的名称不能由程序员指定，因此不会与编译器秘密创建的字符串名称冲突。有关更多信息，请参阅 [2.4]。

### 1.5 Structure or union declarations

### 1.5 结构或联合声明

An external structure declaration is a data declaration with a type specifier of the flavor structure or union type, which is given by the syntax

外部结构声明是一种数据声明，其类型说明符为结构或联合类型，其语法为

```
structure-or-union-type =
    / struct | union / tag_opt
    parts-specification_opt

parts-specification =
    { type-specifier
      declarator-list ; }
```

and a declarator that is a simple identifier. An example is

并且声明符为简单标识符。示例为

```
struct point { float x[2]; struct point *next; } first_point, last_point;
```

which declares first_point and last_point to be variables of a structured type identified by the tag point. The parts-specification enclosed in curly brackets defines a struct point to consist of an array of two floating values named x and a pointer to struct point named next. The variable first_point consists of two sub-variables that are denoted first_point.x and first_point.next. The variable-name-expr first_point.x names an array variable so first_point.x[1] names a float variable within the x part of the structured variable first_point. The complete story on variable-name-exprs must await Chapter 3.

声明 first_point 和 last_point 为由标签 point 标识的结构化类型变量。花括号中包含的 parts-specification 定义 struct point 由一个名为 x 的两个浮点值数组和一个名为 next 的指向 struct point 的指针组成。变量 first_point 由两个子变量组成，分别表示为 first_point.x 和 first_point.next。变量名表达式 first_point.x 命名一个数组变量，因此 first_point.x[1] 命名结构化变量 first_point 的 x 部分内的一个 float 变量。关于 variable-name-exprs 的完整说明必须等待第 3 章。

The above declaration could have been written in the form

上述声明也可以写成以下形式

```
struct point {float x[2]; struct point *next;} ;
struct point first_point, last_point;
```

The first line serves to define the content of the new type struct point but does not declare any names as variables of this type. The second line declares two variables of the new type. The structure tag point serves as an abbreviation for the content described, as well as allowing self-referential pointers within a structure. The parts-specification is only optional if the structure tag already has been defined by a parts-specification in an earlier declaration. The structure tag is optional only if a parts-specification is present.

第一行用于定义新类型 struct point 的内容，但不声明该类型的任何变量名称。第二行声明了两种新类型的变量。结构标签 point 作为所描述内容的缩写，同时允许结构内部的自引用指针。parts-specification 只有在结构标签已由早期声明中的 parts-specification 定义时才是可选的。结构标签只有在存在 parts-specification 时才是可选的。

When the keyword union is used instead of struct, the parts are made to overlay each other so that variables of such a union type at any point in time are holding a value corresponding to just one of the parts. For example,

当使用 keyword union 代替 struct 时，各部分被重叠放置，使得此类联合类型变量在任何时刻都只保存对应于其中一个部分的值。例如，

```
union { double d; float f[2]; } u;
```

declares u to be a variable whose value is at any instant either double or an array of two floats. Sometimes, it is meaningful to say u.d and sometimes u.f[1].

声明 u 为一个变量，其值在任何瞬间要么是 double 要么是两个 float 的数组。有时说 u.d 有意义，有时说 u.f[1] 有意义。

It is necessary to define some predicate, independent of the union, to determine its current contents. Unions can be safely used as part of a structure, one of whose parts is a small variable (char or short int), identifying which variant is actually present. Each value of the union type then is associated with a datum that tells which part names are appropriate to use. An example is

有必要定义一个与联合无关的谓词，以确定其当前内容。联合可以安全地用作结构的一部分，其中一个部分是小型变量（char 或 short int），用于标识实际存在的变体。然后联合类型的每个值都与一个数据相关联，该数据指示应使用哪些部分名称。示例为

```
struct {
  char vtag;
  union {
    double d;
    float f[2];
    char str[4];
  }
  var;
}
u,v;
```

Now the program can test if u.vtag is 1, say, before allowing any references to u.var.d, and similarly check u.vtag against 3 before using u.var.str. Note, however, that the language does not require such a tag variable to be associated with a union; any form of predicate is acceptable.

现在程序可以在允许任何对 u.var.d 的引用之前测试 u.vtag 是否为 1，例如，并在使用 u.var.str 之前类似地检查 u.vtag 是否为 3。然而请注意，语言并不要求此类标签变量与联合相关联；任何形式的谓词都是可接受的。



### 1.6 函数声明

外部函数声明要么定义函数的实例，要么仅声明一个在别处定义的函数的存在。在后一种情况下，声明采用简单形式声明符 ()，其中声明符必须是标量类型。注意，这种函数声明形式不指定关于参数数量或类型的任何信息。

```
declarator ()
```

函数的定义实例采用更复杂的形式

```
[ extern | static ]_opt
type-specifier_opt declarator ( argument-list_opt )
argument-declaration-list_opt
compound-statement
```

其中声明符必须再次是标量类型，argument 是简单标识符，并且

```
argument-declaration = type-specifier declarator-list ;
```

因此，函数中的参数被指定为以逗号分隔的标识符列表，括在圆括号中，并且后面可能跟着为参数提供类型信息的声明列表。

参数必须是标量类型，或可强制转换为标量（即不是结构），并且名称彼此不同。参数声明列表必须只包含紧接在前面的参数列表中参数的声明；参数可以按任意顺序声明，但最多只能声明一次。参数列表是可选的，在这种情况下没有参数。

复合语句的含义以及如何定义函数体将在[2.6]中讨论。

#### 1.6.1 声明

```
double sqrt (d)
    double d;
    |------|
```

将 sqrt 声明为一个函数，当以单个 double 类型参数调用时返回 double。下面是一个更复杂的例子：

```
char * p (ac,c)
    char ac [] ;
    char c;
    { body }
```

它将 p 声明为一个返回指向 char 的指针的函数，调用时使用一个 char 数组的名称（对应于 ac）和一个 char（对应于 c）。

请注意，由于多种原因，这两种参数声明都具有误导性，因为 C 求值表达式的方式，尤其是函数调用的实际参数的方式。因此，ac 实际上是指向 char 的指针，而 c 很可能是 int。这些奥秘将在[3.6]中探讨。

### 1.7 复合类型

到目前为止，我们考虑的是非常简单的声明符形式，主要是单独出现的标识符或带有某种简单限定的标识符。声明符的完整语法规则是

```
declarator =
    identifier
  | * declarator                % pointer
  | declarator ( )              % function
  | declarator [ constant-expr ] % array
  | ( declarator )              % association control
```

该规则的形式表明，声明符由一个唯一标识符通过一系列限定（指向……的指针、返回……的函数或……的数组）以及偶尔用于覆盖声明符中默认关联的圆括号构成。声明符的语法与涉及嵌入标识符的有效表达式的语法相匹配；因此，复合声明符的含义可以从标识符开始由内向外解读，如下面给出的示例所示。

```
int *api[4], *fpi();
```

使 api 成为指向整数的指针的数组，并使 fpi 成为返回指向整数的指针类型值的函数。声明

```
struct { int left, right; } *(*past)[];
```

使 past 成为这样一个变量的名称：该变量的类型是指向数组的指针，而该数组的元素是指向结构的指针，这些结构由整数部分 left 和 right 组成。需要圆括号来强制标识符 past 与首选的 [] 更紧密地关联。后缀数组或函数括号比前缀指针符号结合得更紧，因此在以下声明中也需要圆括号

```
int (*pai)[3], (*pfi)();
```

使 pai 成为指向整数数组的指针，并使 pfi 成为指向返回整数的函数的指针。

- (1) 如果 τ 是类型说明符且 id 是标识符，那么声明 τ id ; 使 id 成为类型为 τ 的变量。
- (2) 如果 D 是带有唯一标识符 id 的声明符，且 τ D_id ; 使 id 成为类型为 T_τ 的变量，而 D_x 表示将 D_id 的唯一 id 替换为 x 后的声明符，那么
  - (a) τ D_(id) ; 使 id 成为指向 T_τ 的指针
  - (b) τ D_id[] ; 使 id 成为 T_τ 的数组
  - (c) τ D_id() ; 使 id 成为返回 T_τ 的函数
  - (d) typedef D_id ; 意味着只要 id 作为类型名出现，id 就等价于 T_τ。

这些规则的意图是使声明的绑定紧密模拟它们在表达式中的使用方式（见第 3 章）。运算符 []（下标）和 ()（带参数调用的函数）从标识符向外绑定。类型定义和加圆括号都要求偏离这种隐含的绑定顺序，因此导致概念上的困难。然而，类型定义提供了巨大的优势，即允许一次一点地构建复杂类型。

类型定义具有以下语法

```
type-definition =
    typedef type-specifier declarator-list ;
```

类型定义

```
typedef float *pf_type ;
```

使名称 pf_type 成为类型名，它是指向 float 的指针的缩写。随后的声明

```
pf_type apf[5], *ppf;
```

使 apf 成为包含五个指向 float 的指针的数组，并使 ppf 成为指向 float 指针的指针。

下面一系列类型定义展示了如何避免上一页所示的像 papst 这样非常复杂的声明符：

```
typedef char FCH() ;          /* function returning char */
typedef FCH *PFCH ;           /* pointer to FCH */
typedef PFCH APFCH[] ;        /* array of PFCH */
typedef APFCH *PAPFCH ;       /* pointer to APFCH */
PAPFCH papfch ;               /* papfch is pointer to APFCH */
```

利用 PAPFCH 的既定含义，我们可以轻松地声明一个返回此类型值的函数：

```
PAPFCH fpapfch();
```

类型定义、结构和指针声明等更有用的示例如下：

```
typedef struct {float real, imag;} COMPLEX;
typedef COMPLEX CVECTOR[4];
typedef CVECTOR CMATRIX[4];
typedef CMATRIX *PCM;
typedef PCM PCMFUNC();
```

这些定义最终将类型名 PCMFUNC 定义为表示返回指向复数矩阵的指针的一类函数，其中后者是一种由四个向量组成的数组的类型，而向量是四个复数的数组，复数是具有两个浮点部分的结构。名为 PCM 的类型作为操作这些 4×4 复数矩阵的函数的参数类型和返回类型将经常有用。

下面总结外部声明语法：

```
C-program =
    { program-file }
program-file =
    { [ function-declaration ] type-definition
      | data-declaration
    }
data-declaration =
    [ extern | static ]_opt
    type-specifier_opt initializable-declarator-list_opt ;
type-specifier =
    { integer-type | floating-type
      | type-name | structure-or-union-type }
initializable-declarator =
    declarator initializer_opt
integer-type =
    { char | unsigned | short | long [ int ]_opt }
floating-type =
    { short_opt double | long_opt float }
structure-or-union-type =
    { struct | union | tag_opt
      parts-specification_opt
    }
% parts-specification optional only if identifier
% present and predeclared as struct-or-union tag
parts-specification =
    { [ type-specifier declarator-list ; ] }
% no declarators allowed for functions
% or arrays of indeterminate length
declarator =
    { identifier
      | * declarator               % pointer
      | declarator ( )             % function
      | declarator [ constant-expr_opt ]  % array
      | ( declarator )             % association control
    }
type-definition =
    typedef type-specifier declarator-list ;

function-declaration =
    [ function-definition | declarator ( ) ]

function-definition =
    [ extern | static ]_opt
    type-specifier_opt declarator ( argument-list_opt )
    argument-declaration-list_opt
    compound-statement

argument-declaration =
    type-specifier declarator-list ;
```

## 2：初始化器

> *开头是如此危险的时期。*
> 
> — 弗兰克·赫伯特，《沙丘》

### 2.0 引言

*初始化器* 是一种方便的方式，可确保某些变量在程序执行开始时具有有意义的值，或构造常量表以辅助运行时计算。函数声明构成了大多数 C 程序的核心，也可以看作是对类型为函数的对象的初始化器。

数据初始化器的语法是

```
initializable-declarator =
  declarator initializer_opt

initializer =
  =_opt { expr | { initializer-list } , }_opt
```

注意尾随逗号被明确允许，以简化长列表的书写。一个非常简单的 *initializable-declarator* 是

```
double x = -0.2E3;
```

而在下面的声明中：

```
COMPLEX vector[3] =
  {{0, 1}, {-3.14, 2.718}, {0.3, 4.1E-13}};
```

存在一个复杂的初始化器，它由三个初始化器的列表组成，每个初始化器对应于三个 COMPLEX 数组的一个元素。列表中的这三个初始化器本身又是 **COMPLEX** 结构体的两个部分初始化器的列表。参见 [1.7] 中对名为 **COMPLEX** 的类型的定义。

在外部声明中出现的任何初始化器都必须是常量表达式，但这可能包括像这样的指针表达式

```c
&c[2].real
```

其中 c 已被声明为 **COMPLEX** 的静态数组。& 运算符给出变量 c[2].real 的位置，该位置可在编译时计算。此表达式的类型为指向 float 的指针，可能出现在声明中

```c
static float *fptr = &c[2].real;
```

局部声明中的初始化器（参见第 4 章）必须只涉及可在包含声明的复合语句入口处计算的表达式。外部变量不得在局部声明中初始化。

初始化器中的常量有效地赋给相应的变量，尽管并非所有在赋值中允许的类型转换都会执行（参见 [3.1]）。例如，在 vector 的上述初始化器中，变量 vector[0].real 和 vector[0].imag 由指定的整数常量 0 和 1 的浮点等价物 0.0 和 1.0 初始化。另一方面，用浮点字面量初始化整数通常不受支持。

外部名称不得被初始化多次，尽管在程序文件之间允许甚至需要多次声明，以便提供程序文件间的通信。

某些实现要求每个外部声明必须恰好初始化一次，以确定对象的定义实例；其他实现至少要求其中一个声明使用 extern 关键字，而另一些实现通常会接受缺少任何初始化器的情况。最安全的做法似乎是挑选一个被多次声明的变量的一个实例作为定义实例；显式地赋予它 extern 属性，并赋予它一个初始化器，即使它只是 0。

### 2.1 整数初始化器

*整数初始化器* 有以下简单形式之一

```
    =opt { expr }
```

其中 *expr* 的类型为整数或字符，并且对于静态或外部初始化器是常量。例如，

```
    static int number = 2 + 3, k = 'A'
```

使得 **number** 的初始值为 5，而 *k* 的初始值为字符常量 'A' 扩展为整数类型后的结果（参见 [3.1]）。

如果表达式的值太大而无法正确表示，则会在左侧截断——不会发出警告。一般不允许使用浮点字面量作为整数初始化器。

### 2.2 浮点初始化器

*浮点初始化器* 有以下形式之一

```
    =opt { expr }
```

其中 *expr* 的类型为浮点，或可以扩展为浮点。静态或外部声明的初始化器必须求值为常量，就像整数一样；但编译器只执行整数运算，因此 2 × 3.142 是不允许的。浮点字面量初始化器中唯一允许的运算符是单目减号。

有效的浮点初始化器的示例是

```
    float x = 0.23E-5, y = 2 * 3, z = '0';
```

请注意，*z* 将被初始化为字符零的内部字符代码（机器相关）的整数的浮点表示。如果在浮点字面量中指定了过多的精度，或该值无法在目标机器中正确表示，编译器通常不会抱怨。

### 2.3 指针初始化器

指针初始化器有以下形式之一

= { expr }

其中 expr 是指针类型的表达式，并且在静态或外部声明的情况下可在编译时计算。一般来说，这意味着表达式必须简化为整数或先前声明变量的地址，再加上或减去一个整数。一些示例是

```
COMPLEX vector[4];
float *fptr = &vector[2].imag;
```

表达式 &vector[2].imag 是指向浮点的指针表达式，因为 vector[2].imag 是一个名称表达式，表示数组 vector 的第三个元素的 imag 部分，而 & 运算符给出命名变量的位置。由于 2 是常量且 imag 在 vector[2] 内的偏移是固定的，因此指针值在编译时已知。以下指针表达式也允许：

```
int k[5];
int *iptr = &k[1] + 2, *jptr = &k[4] - 1;
```

表达式 &k[1] 和 &k[4] 的类型为指向 int 的指针，且 ptr ± 被允许作为指针表达式（参见 [3.3]），因此这些初始化器是常量指向整数的指针。

每当出现未下标的数组名、函数名、字符串常量、结构名、联合名或无参数的函数名时，它们都被解释为指针。因此以下也是有效的初始化器：

```
int (*p)() = distance;
char *pch = "what?";
float vector[10], *fptr = vector;
```

允许将指针初始化为指向未声明的标识符，但这种做法不推荐。同样，指针可以初始化为整数值，但这种做法对于零以外的所有值都极度依赖机器，应保留用于编写系统代码。

### 2.4 数组初始化器

数组初始化器的形式为

```
= expr | { initializer-list , opt }
```

其中 expr 仅初始化第一个元素，或其中 initializer-list 中的每个初始化器都是数组元素的适当初始化器。例如，

```
float x[4] = {0.0, 1.0, 3E-6, -1};
```

是正确的，因为 0.0 是浮点常量且 x[0] 是数组 x 中的浮点变量，等等。当数组的元素本身是数组时，初始化器必须用括号括起的初始化器列表，如下所示：

```
char page[3][5] = { "xxxx", {'y', ':', ':', 'y', '\0'} }
```

这里字符串 "xxxx" 是初始化器列表 {'x', 'x', 'x', 'x', '\0'} 的简写。page 的第一行（即 page[0]）被初始化为 "xxxx"，第二行被初始化为 "y..y"，第三行默认被初始化为零（即 '\0' 的一行），因为外部初始化器列表过早结束。请注意，大小为 4 的字符串需要 5 的行大小，以包含终止的 '\0'。

初始化器

```
int matrix[3][3] = {{1}, {2,3}, {4}};
```

按指定将 matrix[0][0] 初始化为 1，行 0 的其余部分默认初始化为 0；matrix[1][0] 设为 2，matrix[1][1] 设为 3，matrix[1][2] 设为 0；最后，matrix[2][0] 设为 4，行的其余部分设为 0。

在满足所有初始化器都存在且所有数组大小都已指定的前提下，可以省略内部大括号。以下初始化器虽然不推荐，但与上面具有相同的效果：

```
int matrix[3][3] = {1, 0, 0, 2, 3, 0, 4, 0, 0};
```

此外，外层数组的大小可以由初始化器列表的大小隐式给出，如

```
float vector[] = {0.1, 0.2, 0.3, 0.4};
```

这与 vector[4] 的相同声明相同。应仅使最左边的数组大小规范为空，如

```
int matrix[][3] = {{1}, {2, 3}, {4}};
```

这再次等同于上述内容。自动数组不得初始化；必须在函数体中进行单独的标量赋值。

### 2.5 结构初始化器

结构初始化器与数组初始化器类似，具有以下形式：

```
= _opt_ expr | { initializer-list , _opt_ }
```

其中 expr 仅初始化第一个元素，或其中列表中的每个初始化器按顺序必须是结构对应部分的<|message|> 有效初始化器；各部分按结构声明给出的顺序排列。例如，

```
struct node {int degree; char name[5];
float weight; struct node *next;};

struct node first_node =
{2, "Node", 3.7E4, &other_node};
```

这些声明使 first_node 成为 struct node 类型的变量并初始化各部分，如下所示：

| first_node.degree | 是 | 2 |
|---|---|---|
| first_node.name | 是 | "Node" or {'N','o','d','e','\0'} |
| first_node.weight | 是 | 3.7E4 |
| first_node.next | 指向 | other_node |

一个更复杂的示例是

```
struct {COMPLEX matrix[2][2]; char tag;}
cmat =
{/* first the matrix */
{
{[-1, 0], [0, 1]}, /* row 0 */
{[-3.2, 5.]}, /* row 1 */
},
/* then the tag */
'M'
};
```

## 2：初始化器

这里 cmat 已被声明为具有 parts matrix 和 tag 的结构类型变量。因此，其初始化器的一般形式为

```c
{ initializer-for-matrix, char-constant }
```

由于 matrix 是 COMPLEX 类型的数组，其初始化器的形式为

```c
{ initializer-for-row-0,
  initializer-for-row-1
}
```

等等。最后，每个 COMPLEX 结构的初始化器形式为

```c
{ initializer-for-real-part, initializer-for-imag-part }
```

等等，cmat 的完整初始化器由一系列逐步细化得出。注意 cmat.matrix 的第一行的第一个元素并未显式初始化。在外部声明的情况下，默认情况下它将为 {0.0, 0.0}。

如果为联合指定了初始化器，它必须对应于声明的第一个部分。联合和结构都不能在自动声明中初始化。

### 2.6 函数定义

函数定义看起来有点像被初始化的数据声明——因此在本节中讨论它。事实上，参数和函数体构成了与函数名关联的值，因此它们确实起着类似于初始化器的作用，只是函数名代表常量（不可更改）值，而不是变量。函数指针类型的变量可能会改变其归属，但函数不会！

函数定义的语法是

```c
function-definition ::= { extern | static }opt
type-specifier opt declarator ( argument-list opt )
argument-declaration-list opt
compound-statement
```

复合语句最简单的形式是被大括号括起来的语句序列（命令式命令）。下面是一个完整的函数定义：

```c
double length(x, y)
double x, y;
{
    return sqrt(x * x + y * y);
}
```

名称 x 和 y 是函数 length 的形式参数，它们表现得像特殊变量，每次调用函数时都会初始化为不同的值。因此，在参数规范中不允许有显式初始化器。length(0.0, p[2]) 的出现等价于 sqrt(0.0 * 0.0 + p[2] * p[2])。

像 (*fpa())[] 这样的复杂函数声明符可以通过类型定义来避免，如 [1.7] 中所述，因此其解释将推迟到第 4 章。

在详细检查复合语句之前，区分指针参数和其他参数是有启发性的。一个函数改变调用该函数的环境中某个变量 x 的值的唯一方法是将 x 的位置 &x 传递给它，其中相应的形式参数是指针类型。此外，聚合类型（struct、union 或 array）不能直接作为参数传递，但指向它们的指针可以。下一页所示的函数旨在用 value x 等于数组 table 的元素的第一个下标位置替换 index：

```c
float table[6] = {0, 0, 1, 2, 3, 7}, x = 2;
int index;
main() {
    lookup(&table[0], x, &index);
}
```

```c
lookup(t, val, i)
float *t;
float val;
int *i;
{
    int k;
    for (k = 0; k < 6; ++k)
        if (*(t + k) == val)
        {
            *i = k;
            return;
        }
    *i = -1;
}
```

其中一些内容在完全理解指针表达式和 variable-name-exprs 之前不会很清楚；请特别参见 [3.1] 和 [3.3]。重要的是要认识到，在 &index 之后，对应于形式指针参数 i 的实际参数被给出；然后，像 *i = k; 这样的赋值实际上意味着对 index 的赋值，因为前缀指针操作 * 使表达式 *i 成为内存中可更改对象的有效 name-expr。

上面的程序可以重写，将 &table[0] 改为 table，将 float *t 改为 float t[]，将 *(t + k) 改为 t[k]，而不会改变含义。这是因为未下标的数组名被视为指向第 0 个元素的指针的值，因为形式数组参数被解释为指向数组元素类型的指针，并且因为 t[k]  anyway 被实现为表达式 *(t + k)（参见 [3.4]）。

现在是时候描述一些语句了。函数定义的基本单位是复合语句，其语法如下所示：

```c
compound-statement =
{ { local-declaration | type-definition }
  { statement } }
```

这些局部声明和类型定义的详细讨论——它们在很大程度上与外部声明相同——在第 4 章中。对于现在，我们将集中于 C 语言的语句，或命令式命令。

```c
statement =
| expr ;     % assignments and function calls
| compound-statement % for grouping
| selection-statement
| repetition-statement
| interruption-statement
| labeled-statement % null statement
;
```

尽管表达式（即 exprs）的详细讨论必须等待第 3 章，但我们将介绍简单的赋值表达式（大多数语言中的语句）和函数调用（其他地方的 procedure 或 subroutine 调用），因为它们是大多数 C 程序的活跃主力。一些已经遇到的表达式语句是：

```c
k = 0;
/* same as k = k + 1; */
lookup(table, x, &index);
```

无法做出选择的程序确实很弱，因此 C 有两种选择语句：

```c
selection-statement =
| if ( logical-expr ) statement
| if ( logical-expr ) statement else statement
| switch ( expr ) switch-statement-group

switch-statement-group =
| { { local-declaration | type-definition } }
| case-prefixed-statement

case-prefixed-statement =
| case constant-expr : statement
| default : statement
```

if 语句要求在 logical-expr 为“真”（非零）时精确执行第一个子语句；否则，它要求在 else 之后执行第二个子语句。当省略 else 短语时，就好像显式指定了 else /* null */; 一样。例如，

```c
if (k < 2)
    p = f(k);
else
    p = g(2 - k);
```

将根据 k 相对于 2 的大小执行两个赋值中的恰好一个。关系运算符提供 1 表示“真”，0 表示“假”，将在第 3 章中更详细地讨论。常见形式是

```c
if (p)
...
else if (q)
...
else if (r)
...
else
/* none of the above */
...
```

并且推荐这种缩进风格。

经常 enough，逻辑表达式 p、q、r 等具有 k == 1、k == 2、k == 5 等形式，其中 == 是 C 中的相等比较运算符。switch 语句可处理此类情况，例如

```c
switch(k - 2)
{
case 3: j = k*k; break;
case 5: case 2: ++k; do_something(k); break;
default: error("bad k");
}
```

由于 case 前缀只允许常量表达式，switch 语句可以非常高效地实现。break 语句对于在每个可选择部分之后终止 switch 语句是必要的；否则，控制会以最不令人满意的方式从一个 case 流向下一个 case。case 标签可能出现在复合语句中嵌入。只有嵌入的 switch 语句限制了这种有问题的功能。

C 的重复语句由以下给出

```c
repetition-statement =
| while ( logical-expr ) statement
| do statement while ( logical-expr );
| for ( expr_opt ; logical-expr ; expr_opt ) statement
```

while 语句重复执行其子语句，直到 logical-expr 不再为“真”，如果 logical-expr 为“假”，则永远不会开始执行子语句。如果 logical-expr 最初为“假”，它可能是一个重数为 0 的重复。

do 语句类似，只是测试是在每次执行子语句之后进行，并且重复可能在此时终止。因此它至少执行一次其子语句。

for 语句是以下内容的简写

```c
expr1;
while ( logical-expr )
{ statement ; expr2 }
```

因此第一个表达式通常是初始化；第二个是逻辑预测试；第三个是某种形式的后增量。示例是

```c
while (c[i] == ' ' && i < SIZE)
    ++i;
do
{
    swap (c, i, j);
    ++i;
    --j;
}
while (i < j);
/* array c now reversed */
for (i = 0; i < SIZE; ++i)
{
    a[i] = b[i];
    c[i] = -1.0;
}
/* array b copied to a and c set to -1.0 */
```

如果 for 语句中的 logical-expr 缺失，则假定为常量“真”值（1）。



有时中断语句的正常顺序很方便，可以使用以下之一：

```
interruption-statement =
| break ;
| continue ;
| return expr ;
| goto identifier ;
|
```

break 语句导致最小的外层重复或 switch 语句终止。

continue 语句导致最小的外层重复语句的可重复子语句终止。执行将从 for 的增量部分或 do 或 while 的测试部分恢复。

return 语句终止包含函数的执行。如果指定了 expr，则它在转换为函数声明的类型后成为函数的返回值；如果没有表达式，则函数返回的值是垃圾。在每个函数体的末尾，都有一个隐式的无表达式 return。

goto 语句指定执行应从标识符标记的语句处恢复。最后，带标签的语句的语法为

```
labeled-statement =
    identifier : statement
```

并作为 goto 语句的目标。在同一个函数中，只能出现给定标签的此类定义之一。由于带标签的语句是语句的合法形式，因此可以按顺序出现任意数量的标签。实际上，break 很少需要，continue 从不需要，而 goto 的需要比那还要少。由此可知，如果避免使用 goto，则永远不需要使用标签。同样，将 return 语句的数量最小化也是良好的风格；为了可读性，在函数末尾恰好有一个是最好的。

### 2.7 初始化器语法

所有数据初始化器采用以下形式

```
initializer ::= =opt { expr | initializer-list ,opt } |
```

并且所有函数初始化器都是以下形式的复合语句

```
compound-statement ::= { [ { local-declaration | type-definition } ]opt { statement }opt }
```

```
statement =
| expr ;                 % assignments and function calls
| compound-statement     % for grouping
| selection-statement
| repetition-statement
| interruption-statement
| labeled-statement
| ;                      % null statement
|
```

```
selection-statement =
| if ( logical-expr ) statement
  ( else statement )opt
| switch ( expr ) switch-statement-group
|
```

```
switch-statement-group =
{ [ { local-declaration | type-definition } ]opt
  { case-prefixed-statement } }
```

```
case-prefixed-statement =
{ case constant-expr | default : } statement
```

```
repetition-statement =
| while ( logical-expr ) statement
| do statement while ( logical-expr ) ;
| for ( expr opt ; logical-expr opt ; expr opt ) statement
|
```

```
interruption-statement =
| break ;
| continue ;
| return expr opt ;
| goto identifier ;
|
```

```
labeled-statement =
identifier : statement
```

## 3：表达式

> 我们将要除的结果，如你所见，
> 除以九百九十和九十二：
> 然后减去十七，答案必须
> 完全且完美地正确。
>
> —— 刘易斯·卡罗尔，《寻觅史纳克》

### 3.0 引言

C 的表达式实际上执行程序的工作（变量状态的改变）。特别是，简单赋值用新计算的值替换某个变量的当前值，其语法为

```
variable-name-expr = expr
```

variable-name-expr 的复杂程度从整数变量的简单标识符到像这样的复杂名称表达式不等

pcm -> matrix[1][k].imag

它标识由指针变量 pcm 指向的结构的 matrix 部分中第 1 行第 k 列的 complex 成员的 imag 部分。本章的其余部分将解释此类表达式。

表达式本身是一个更广泛的类，允许将许多不同的运算符与 variable-name-expr 和常量结合起来，从而提供语言的计算能力。这些表达式的复杂程度从简单的整数常量到诸如
(mlk +2) >>3) | (p -> f * (*pfun)(2,j))
之类的东西，后者难以用简单的语言描述。

在我们踏上穿越运算符空间的漫长旅程之前，有几个具有普遍兴趣的话题至少应简要讨论一下。首先是运算符的优先级和结合性。

每当出现序列
operand1 binop1 operand2 binop2 operand3
时（例如 a + b * c），表达式的解释就会存在潜在的歧义 [例如 (a + b) * c 或 a + (b * c)]。C 中的每个运算符都有相对于其他运算符的优先级级别，如果两个运算符的级别不同，则该级别可明确确定结合性。由于乘法运算符 * 的级别高于加法运算符 +，因此表达式 a + b * c 的含义为 a + (b * c)。程序员可以使用括号来覆盖这些规则 [例如通过写成 (a + b) * c]。

在同一优先级级别内，大多数二元运算符将“从左到右”结合。例如，
a + b - c + d 的含义为 ((a + b) - c) + d

然而，赋值运算符则恰恰相反：
x = a[2] = j = 0 的含义为 x = (a[2] = (j = 0))

所有一元运算符都在同一级别，并且高于所有二元运算符。它们从右到左结合，正如人们所期望的那样，因为它们大多处于前缀位置。例如，
-*pi
表示 pi 所指向的整数的负值。在大多数情况下，语言不规定子表达式的求值顺序，因此 a * b + c * d 可能是先计算 (a * b)，然后计算 (c * d)，或反之亦然。这对于像
(t = f(a)) + g(t)
这样的表达式具有明确的意义，其值不保证可重复计算。程序员在使用计算中的赋值表达式时应谨慎。语言还允许实现重新排列具有相同可交换运算符的表达式：

```
a + b + c is (a + c) + b or (a + b) + c. etc.
```

算术类型（整数和浮点）从 char 到 double 形成一个自然的层次结构，称为扩展层次结构：

```
char → short → int → unsigned → long → float → double
```

它决定了当两个操作数具有不同的算术类型时，许多运算符返回的值的类型。例如，在

```
(i + '0') - x  /* i is int, x float */
```

char 值 '0' 被扩展为整数，然后可以与 i 相加；然后该整数结果被扩展为浮点数，以便可以减去浮点数 x，从而产生最终的浮点结果。语言还具有强制转换运算符，可显式请求此类扩展，因此上面等价于

```
(float)(i + (int)'0') - x
```

二元算术运算符的正常规则要求将较窄的操作数扩展到较宽的操作数。语言保留了通过扩展操作数超过必要的程度来执行算术运算的权利，只是为了满足此规则。因此，char 和 short 操作数经常被扩展为 int，而 float 算术通常在 double 中执行。这种区别通常对程序员来说并不明显。

当 variable-name-expr 的类型比赋给它的表达式的类型更宽时，会发生正常的扩展；当它更窄时，转换取决于机器且容易丢失信息，因此应谨慎使用窄化赋值。

C 程序可能包含语法如下的 conditional-expr

```
conditional-expr =
logical-expr ? expr : expr
```

它们用于在 if else 中避免重复大部分表达式，当只有一部分取决于某些条件时。例如，

x = (y < 3.0) ? -1.0 : 1.0 ;

将 -1.0 的值赋给 x，如果 y 小于 3.0；否则，将 1.0 的值赋给。语言规则规定只评估其中一个而不是两个 expr。结果始终是两个 expr 类型中较宽的类型，因此上面的整数 1 在赋给 x 之前会被扩展为 1.0。

```
assignment-expr = |
| variable-name-expr binop = expr
| ++ | -- | scalar-variable-expr ++ | -- |
% scalar means arithmetic or pointer

binop = + | - | * | / | % | & | | | ^ | << | >> |
```

类似 x += y 的赋值用 x + y 的值替换 x，但 x 不会被计算两次。要将 x、i、j 加倍，只需写成
x, i, j *= 2

类似 ++x、--x 的赋值分别等价于 (x += 1)、(x -= 1)。所有 assignment-expr 都返回一个值，该值是赋值发生前或后的变量值。在 assignment-expr 的三种形式中，只有后缀增量运算符 (++、--) 在赋值前返回值。

```
k = 0; /* k is 0 */
n = k++; /* n is 0, k is 1 */
m = (k * 2); /* m and k are 2 */
k = --n; /* k and n are 1 */
k += (n++) - n /* ouch! no promises */
```

应该记住，语言不指定赋值的两个操作数的求值顺序，因此

i = 2; a[i] = x + (i == 3) /* a[i] is a2 or a3 ? */

不是确定的。



C语言具有序列表达式，它由逗号分隔的表达式序列组成，即表达式列表。建议将序列表达式用括起来的括号括起来，因为有时它们可能出现在逗号也有其他含义的上下文中，例如在参数列表中。其含义为

```
(t = x, s = y - f(t), s*7.3)
```

与我们写复合语句的情况非常相似

```
{t = x, s = y - f(t); s*7.3}
```

用来代替表达式。三个子表达式按从左到右的顺序求值，就像在类似的复合语句中分号所暗示的那样；返回的值是列表中最后一个（最右边的）表达式的值。

### 3.1 整数表达式

基本的整数表达式是所谓的整数原语，包括整数常量、整数和字符变量名、整数函数调用（参见 [3.6]）以及带括号的整数表达式。以下是整数原语：

- 25
- k
- count(p,3)
- (i - 2 * k)

更复杂的名称表达式如 p->qlk1.n 将在后续章节中处理。

整数原语可以用一元运算符 + 和 -，或二元运算符 +、-、*、/、% 中的一个与其他整数表达式组合。整数商（/）和余数（%）运算符在两个操作数都为正时产生预期的商和余数（向零截断）。否则结果在某种程度上依赖于机器。其他三个运算符是正常的整数算术运算符。例如，3+6 是 9，3-5 是 -2，3*12 是 36，17/5 是 3 且 17%5 是 2。

以下是一个整数算术表达式：

```
25 + k % count(p,3) - 7 / (i - 2 * k)
```

也可以使用按位二元运算符 &、|、^、<<、>> 以及一元按位运算符 ~ 来组合整数表达式。它们分别称为“与”、“或”、“异或”、“左移”、“右移”和“补码”。“补码”将操作数视为二进制数字序列并翻转每个“位”的状态。“与”、“或”和“异或”将两个操作数视为二进制数字序列并执行众所周知的按位操作。移位将第一个操作数视为二进制数字序列，根据第二个操作数给出的位数进行左移或右移，第二个操作数应为正以获得最大可移植性。左移从右侧引入零位，但对于第一个操作数为负值的情况，右移通常不保证这样做。例如，

- (000101) & (010110) 是 (000100)
- (000111) | (110100) 是 (110111)
- (000111) ^ (110100) 是 (110011)
- (000101) << 2 是 (010100)
- (001100) >> 3 是 (000001)
- ~(001100) 是 (110011)

以下语句从 k 中提取低八位字节并将其插入到 p 的高八位字节中，假设整数变量为 16 位：

```
p = (p&0377) | (k&0xFF)<<8
```

表达式 p&0377 保存 p 的低字节且高字节为零。表达式 (k&0xFF)<<8 的高字节为 k 的低字节且低字节为零。因此，按位“或”的高字节等于 k 的低字节，低字节等于 p 的低字节。以下两个表达式在 16 位计算机上也是相同的：

```
p ^ 0xFFFF is ~p
```

整数表达式也可以通过取同一类型的两个指针表达式的差值得到。例如，如果 a 是 int 数组，则

```
&a[3] - &a[1]
```

是两个指针之差除以 int 的大小。因此，值是 2。如果两个指针不指向同一个数组，则可能出现奇怪的结果。有关指针表达式的细节请参见 [3.3]。

还有形式为的整数常量

```
sizeof ( expr )
sizeof ( type-expr )
```

它们返回操作数 expr 的字节大小，或由强制转换 ( type-expr ) 指定类型的大小。sizeof 函数应用于数组变量名或字符串时，会给出整个数组的大小，正如预期的那样。

最后，在整数表达式中可以找到非常重要的逻辑表达式，其语法为

```
logical-expr =
{ logical-expr && logical-expr
| logical-expr || logical-expr
| ! logical-expr
| expr { == | != } expr
| expr { < | > | <= | >= } expr
| expr interpreted as (expr != 0)
| ( logical-expr )
}
```

逻辑与 &&、逻辑或 || 和逻辑非 ! 运算符定义为等价于某些条件表达式，如下所示：

```
a && b ≡ a ? ( b ? 1 : 0 ) : 0
a || b ≡ a ? 1 : ( b ? 1 : 0 )
! a ≡ a ? 0 : 1
```

这些运算符的结果始终为 0 或 1；因此，保存这些运算符生成的值的整数变量可以充当布尔或逻辑变量。这是因为在测试上下文中遇到的整数表达式在非零时被解释为“真”，否则为“假”。请注意，&& 和 || 确定了继承自条件表达式含义的求值顺序。基本上，它们保证从左到右求值，并在值确定后立即终止。

相等运算符（等于 == 和不等于 !=）以及关系运算符（小于 <、大于 >、小于等于 <=、大于等于 >=）在不等式为“真”时产生 1，否则为 0。如果一个操作数比另一个窄，则在比较前会适当扩展。

形式为的强制转换表达式

```
(int) arithmetic-expr
```

给出的整数值与将 arithmetic-expr 分配给 int 变量所得到的值相同。

### 3.2 浮点表达式

基本的浮点表达式是浮点原语，包括浮点常量、浮点变量名、浮点函数调用以及带括号的浮点表达式，如 3.14159E-5、xlk、-l1、length(x, y)、(2.0 * z + y)

更复杂的浮点表达式由浮点原语和其他浮点表达式通过一元运算符 + 和 - 以及熟悉的二元算术运算符 +、-、* 和 / 构建。例如，

```
3.14 * (xlk - l1 - length(x, y)) + z/1.1
```

增量运算符 ++ 和 -- 要求将 1.0 或 -1.0 加到指定的浮点变量上。与整数一样，前缀和后缀形式都适用。浮点计算的精度至少与两个操作数中较宽（更精确）的操作数一样精确。某些实现在计算期间可能使用额外的精度。

形式为的强制转换表达式

```
(float) arithmetic-expr
```

在必要时将 arithmetic-expr 扩展为 float。

整数可以自由地与浮点操作数混合使用，并在需要时进行扩展。

### 3.3 指针表达式

严格来说没有指针常量，因此指针类型的原语是指针变量名、指针函数调用以及带括号的指针表达式。基本的指针表达式形式为

```
&variable-name-expr
```

示例为

```
&k
&c[2].f
&(p->name)
```

如果 k 和 c 是 static 或 extern 变量，则前两个是常量指针表达式。

唯一的其它指针表达式形式为

```
pointer-expr [ + | - ] integer-expr
```

其值由指针表达式的当前地址值加上或减去按指针所指向类型大小缩放的 integer-expr 值给出。例如，如果 a 是 int 数组且 int 的大小为 2，则 &a[0]+2 将比数组 a 开头的机器地址大 4。因此，&a[0]+2 ≡ &a[2]，这就是指针算术如此定义的动机。

增量赋值（++ 和 --）可以应用于指针变量名，在这种情况下，上述加法和减法的含义生效。例如，

```
p = &a[0]; ++p;  /* p points at a[1] */
p += 2; --p;     /* now at a[2] */
```

如果将整数赋给指针变量，则不执行缩放。这是语言类型检查中故意留下的一个漏洞，以便于系统编程。指针表达式因“解引用”运算符 * 而出现在其他类型的表达式中，该运算符作为指针表达式的前缀，提供由指针表达式的值指向的变量的名称。




在 C 语言中，指针较为重要的用途之一是使用指针增量赋值来高效地遍历数组。下面的代码将在字符数组中查找第一个 x。

```
p = &str[0];
while (*p != 'x')
    ++p;
/* now p points at first str[k] == x */
```

### 3.4 涉及数组的表达式

C 语言所允许的复杂变量名表达式（variable-name-expr）由以下部分构建而成：对指针表达式（pointer-expr）应用解引用运算符 *（参见[3.3]）、对结构和结构指针应用部件选择运算符 . 和 ->（参见[3.5]），以及本节将要讨论的数组元素选择表达式。以下形式的表达式

```
array-variable-name-expr [ integer-expr-list ]
```

表示由 integer-expr-list 的值所选择的元素变量。与数组声明的情况相同，a[5][j, x+3] 完全等价于 a[5][j][x+3]。每个值显然都应为非负数，并且小于数组中相应声明的最大元素数量。例如，

```
int a[5], k;
k = 3;
a[4] = a[k] + a[k+1];   /* okay */
a[k+2] = 9;             /* no good, a[4] is last */
```

一个具有多个维度的声明，例如

```
float x[5][3][2][2];
```

将 x 声明为类型为“float 的数组的数组的数组”的变量，因此 x[3] 本身就是一个合法的数组变量名表达式（array-variable-name-expr），x[3][2] 也是如此。最后，x[3][2][1][0] 是一个 float 变量名表达式（float-variable-name-expr），可以在计算中使用，也可以被赋予新值。

虽然通常不会引起程序员的兴趣，但下标表示法满足等价关系

```
a[e] ≡ *((a) + (e))
```

其中不带下标的数组名 a 被视为等价于 &a[0]，即指向 a 的第一个元素的指针，而 + 表示指针运算。

当数组名和字符串作为未加下标的表达式出现、且不作为数组初始化器时，它们会被转换为指向第一个元素的指针表达式（pointer-expr）。例如，下面的函数调用

```
printf("Here is a string %s", ch_array);
```

传递两个指针参数：第一个是指向字符 'H' 的 char 指针；第二个是指向（假定为）char 数组 ch_array 的第一个元素的指针。

### 3.5 结构和联合表达式

以下形式的表达式 structure-or-union-variable-name . part-name 表示指定结构或联合变量中由 part-name 标识的子变量。类似地，以下形式的表达式 structure-or-union-pointer-expr -> part-name 表示由指针表达式当前值所指向的结构或联合中的部件变量。例如，

```
struct point {float x[2]; struct point *next;}
first_point, last_point, *top;
top = &first_point;
first_point.x[0] = 3.2; /* same as top -> x[0] = 3.2; */
first_point.next = &last_point;
first_point.next -> x[0] = -1.0;
last_point.next = 0; /* null pointer */
top -> x[1] = 3.9;
top = &first_point; /* changes nothing */
```

使得指针 top 指向结构 first_point，然后将 first_point 的部件 x 的第 0 个元素改为 3.2，将 first_point 的 next 部件指向 last_point，将 first_point 的 next 部件所指向结构的部件 x 的第 0 个元素设为 -1.0，将 last_point 的 next 部件设为不指向任何地方，并将 top 所指向结构的部件 x 的第 1 个元素设为 3.9。最后的赋值除了浪费时间外什么都没做，因为 top 已经指向 first_point。

当表达式需要标量值的位置出现结构和联合引用时，它们不会像数组和函数引用那样被转换为指针。因此，对于结构或联合，你几乎只能选择它的某个部件或取其地址。下面的示例展示了如何安全地使用联合：

```
struct card_variant {char vtag; char rank, suit;};
struct joker_variant {char vtag; int num;};
union {struct card_variant card;
struct joker_variant joker;} deck[54];
/* initialize the deck of 52 cards & 2 jokers */
if (deck[k].card.vtag == 'C')
{if (deck[k].card.suit == 'H') ...etc.}
else if (deck[k].card.vtag == 'J')
{if (deck[k].joker.num < 3) ...etc.}
else
{error ("bad card");}
```

### 3.6 函数调用

C 语言的函数通过以下形式的函数调用进行调用：

```
function-name-expr ( expr-list )_opt
```

其中 function-name-expr 的语法规则为

```
function-name-expr =
{ function-name
| (* function-pointer-expr )
}
```

function-name-expr 的复杂度范围从像 sqrt 这样的简单名称，到像 (*p->c[k-2].pfch) 这样复杂的表达式，后者表示由指针变量 p 所指向的结构中数组部件 c 里第 (k - 2) 个元素的指针部件 pfch 所指向的函数。部件选择运算符 -> 和 . 具有最高的优先级（与 [] 和 () 一样），因此解引用运算符 * 是上述表达式中最后应用的。运算符优先级和结合性的完整说明请参见[3.7]。

允许 function-name-expr 是未声明的标识符，在这种情况下，它被视为返回整数类型的外部函数。没有返回语句的函数（称为“void”函数）绝不应在返回值会产生影响的表达式中使用；换句话说，它只能作为表达式语句出现，或作为序列表达式（sequence-expr）中除最后一个表达式以外的任意表达式，或作为 for 循环中除测试部分以外的任意部分。

函数名表达式后面括号列表中的表达式称为函数调用的实际参数，它们在数量和类型上应与函数定义中指定的形式参数列表相对应。例如，如果 lookup 被声明（参见[2.6]）为具有以下参数规范的函数

```
(float *t, val; int *i;)
```

那么每次调用 lookup 的形式应为

```
lookup(e₁, e₂, e₃)
```

其中 eᵢ 分别是类型为指向浮点数的指针、浮点数和指向整数的指针的表达式。

在没有任何参数声明的情况下，例如对于未声明的 function-name-expr、声明为无参数的函数，或超出参数列表中已声明部分的参数，会应用某些默认的类型转换。char 和 short 类型会加宽为 int，float 类型会加宽为 double。如果函数期望接收 char、short 或 float 类型，那么调用函数必须知道参数声明。只要调用方和被调用方都知道预期结果，就允许实现根据其认为合适的方式加宽参数。

作为实际参数，未加下标的数组变量名表达式（array-variable-name-expr）或字符串会被解释为指向数组第一个元素的指针值；同样，没有括号参数列表的函数名表达式（function-name-expr）也会被视为指向该命名函数的指针值。

在函数定义中，形式数组参数被解释为指向数组元素类型的指针；因此，所有数组参数本质上都是可变参数（即其元素可以被修改）：在函数定义内部，形如 a[k] = e; 的赋值会改变作为实际参数 a 出现的数组中第 k 个元素的值。例如，

```
clear_array(float a1[]; int n;)
{
	int i;
	for (i=0; i<n; ++i)
		a1[i] = 0.0;
}
float x[5][5];
main()
{
	clear_array(x[2], 5); /* clear 2nd row */
}
```

将矩阵 x[5][5] 的表达式 x[2] 清零为浮点零。表达式 x[2] 是一个合法的数组变量名表达式，包含 5 个 float 类型的元素，与形式参数 a1（类型为 float 数组）相匹配。在调用 clear_array(x[2], 5); 执行 clear_array 期间，clear_array 中的每个赋值 a1[i] = 0.0; 实际上都意味着 x[2][i] = 0.0;。

C 语言中的所有函数都可以递归地调用自身，也可以调用其他最终会调用回它们的函数。作为递归的一个示例，以下函数返回前 n 个整数的和：

```
int sum (int n;)
{
	return (n <= 1 ? 1 : n + sum(n - 1));
}
```

### 3.7 表达式语法

以下总结了 C 语言中表达式的语法：

```
expr = | conditional-expr | assignment-expr | sequence-expr | arithmetic-expr | pointer-expr | cast-expr |
```




```
arithmetic-expr =
    { integer-expr | floating-expr }

integer-expr =
    { integer-arithmetic-expr
    | bitwise-expr
    | logical-expr
    | pointer-difference
    | object-size-value
    | integer-cast-expr
    | integer-primary
    }

integer-arithmetic-expr =
    { [ + | - ] integer-expr
    | integer-expr [ + | - | * | / | % ] integer-expr
    }

bitwise-expr =
    { ~ integer-expr
    | integer-expr [ & | | | ^ | << | >> ]
        integer-expr
    }

pointer-difference =
    pointer-expr - pointer-expr

object-size-value =
    sizeof { expr | ( type-expr ) }

logical-expr =
    { logical-expr && logical-expr
    | logical-expr || logical-expr
    | ! logical-expr
    | expr [ == | != | < | > | <= | >= ] expr
    | expr % interpreted as (expr != 0)
    | ( logical-expr )
    }

integer-cast-expr =
    ( { char | short | unsigned | long | opt int } ) arithmetic-expr

floating-expr =
    { floating-expr [ + | - | * | / ] floating-expr
    | [ + | - ] floating-expr
    | floating-cast-expr
    | floating-primary }

floating-cast-expr =
    ( long_opt float ) | ( short_opt double ) | floating-expr

conditional-expr =
    logical-expr ? expr : expr

assignment-expr =
    { variable-name-expr binop_opt = expr
    | ++ | -- | scalar-variable-name-expr
    | scalar-variable-name-expr [ ++ | -- ]
    } % scalar means arithmetic or pointer

binop =
    { + | - | * | / | %
    | & | | | << | >>
    }

sequence-expr =
    expr , expr

pointer-expr =
    { pointer-primary
    | & variable-name-expr % but not array name
    | pointer-expr [ + | - ] integer-expr
    }

cast-expr =
    ( type-expr ) expr

type-expr =
    type-specifier abstract-declarator

abstract-declarator =
    { empty | * abstract-declarator
    | abstract-declarator ( )
    | abstract-declarator [ constant-expr_opt ]
    | ( non-empty-abstract-declarator ) % a declarator with its identifier deleted
    }

primary =
    { constant | variable-name-expr | string
    | function-name-expr ( expr-list_opt )
    | ( expr )
    }

function-name-expr =
    { function-name | * pointer-expr
    | structure-or-union-variable-name-expr . part-name
    | structure-or-union-pointer-expr -> part-name
    | array-variable-name-expr [ expr ]
    }
```

## 运算符优先级和结合性

| 类别 | 运算符 | 结合性 |
|---|---|---|
| 主表达式 | . -> ( 参数 ) [ 下标 ] | → |
| 一元 | * & + - ! ~ ++ -- ( 强制转换 ) sizeof | → |
| 乘法 | * / % | → |
| 加法 | + - | → |
| 移位 | << >> | → |
| 关系 | < > <= >= | → |
| 相等 | == != | → |
| 按位与 | & | → |
| 按位异或 | ^ | → |
| 按位或 | \| | → |
| 逻辑与 | && | → |
| 逻辑或 | \|\| | → |
| 条件 | e1 ? e2 : e3 | → |
| 赋值 | = binop= | ← |
| 序列 | e1 , e2 | → |

允许重新排列的运算符有

## 可交换的二元运算符

\* + == != & ^ |

以下运算符隐含固定的求值顺序：

## 强制求值顺序运算符

&& || e1 ? e2 : e3 e1 , e2

## 4：局部声明

> 如果有人缺少什么
> 他会发现一切都已堆放在那里。
> 
> —— W.S. Gilbert，《巫师》

### 4.0 引言

C 程序中的每个复合语句都可能以一系列局部声明或类型定义开始，这些声明或定义用于引入对象或类型的名称，其声明的属性在封闭的复合语句之外未知或不相关。局部类型定义与外部类型定义的语法相同，而局部声明的语法为

```
local-declaration =
    { auto_opt | static | extern | register }
    type-specifier_opt initializable-declarator-list_opt ;
```

它与类似的外部名称声明相似，只是存在四个可能的属性来控制变量的可见性、生命周期和存储类。automatic 属性是默认值，表示变量仅在其声明所在的最近封闭复合语句内可见，并且在复合语句的每次单独执行时，变量的先前值将被遗忘。register 属性与 automatic 含义相同，并且额外请求将变量保存在通用计算机上通常可用的高速寄存器中。对 automatic 或 register 变量的任何初始化都在每次正常进入复合语句时执行。通过 goto 或 switch 将控制转移到复合语句中间会绕过此初始化。

static 属性意味着仅在最近封闭的复合语句内可见，而 static 变量的值在复合语句的单独执行之间保持不变。任何初始化只执行一次，在程序执行开始之前（可能在编译时）。external 属性表示当前复合语句中该名称的所有后续出现都被视为引用该名称的外部声明或定义。显式导入函数中使用的所有外部引用是良好的做法。在局部声明处对外部变量进行初始化是不允许的。

与外部声明不同，局部声明中必须存在存储类或类型说明符。块内的局部声明以第一个不是局部声明的语句结束。

以下荒谬的示例说明了这些各种可能性：

```
int n = 0;      /* external by default */
static x;       /* only visible in current program-file */
extern float y[3] = {-1.0, 1.0, 0.0};
glob ()
{
    float q;        /* automatic known only in glob */
    int *iptr = &n; /* refers to external n */
    extern float y1; /* can't initialize here */

    while (*iptr != '\0')
    {
        static int count;   /* count and ch */
        register char ch = 'A'; /* only known here */
        if (*iptr == ch)
            return(count);
        ++count;    /* ch dies each time */
        ++iptr;     /* around loop. */
    }               /* but count lives on */
    ...
}
```

具有 automatic 或 register 属性且未初始化的变量在复合语句执行开始时将具有未定义值（即垃圾值）。这与 static 或外部声明的变量形成对比，后者的默认初始化为零。

重新声明一个名称是合法的，该名称在复合语句中是局部的，而该名称已因外部声明符（在封闭复合语句中的声明）而具有声明的含义。在整个内部上下文（复合语句）中，该名称将具有更局部的声明含义，而在此内部上下文之后，其含义将恢复为更全局的含义。以下示例展示了其工作原理：

```
int n;
float x;
main ()
{
    if (n > 0)          /* global n */
    {
        char x = 'A';
        printf("%c", x);   /* local x char */
    }
    x = -1.0 / 2.5;      /* global x float */
}
ff(int n;)            /* argument is implicit local */
{
    printf("%d", n);   /* not the global n */
}
```

请注意，形式参数名称构成隐式局部声明。

用于局部声明的 automatic 或 register 变量初始化器的表达式应仅包括当前已声明并具有值的变量。在定义函数体的复合语句内，参数可被视为具有已定义的值，因此可用于初始化函数体的局部变量。例如，

```
float z = 1.0;
what(int a; char b;)
{
    float x = a/z;
    int q = b&0377;
    float *fptr = &z;
    ...
}
```

经特别许可，函数的形参可以赋予 register 存储类。这并不意味着相应的参数必然以快速寄存器传递，而是在进入函数时，如果有可用寄存器，则将其复制到其中以供后续使用。与 register 存储类的所有使用一样，这应被视为对编译器的建议，以帮助其更好地优化代码。如果没有足够的（或没有）寄存器可供分配，它永远不会导致诊断信息。

Register 变量的行为与任何 automatic 变量类似，只是不能取寄存器的地址；这意味着它们不能与一元 & 或二元 . 运算符一起使用，并且不能保存复合项（数组、结构体、联合体、函数）。

### 4.1 局部整数变量

整数变量可以用 auto、register、static 或 extern 中的任何一种存储类进行局部声明。前两种可以用在进入复合语句时已定义并且可以赋给整数变量的任何表达式进行初始化。static 局部变量遵循与外部声明相同的规则 [2.1]；extern 不能被初始化。

### 4.2 局部浮点变量

浮点变量可以用 auto、register、static 或 extern 中的任何一种存储类进行局部声明。前两种可以用在进入复合语句时已定义并且可以赋给浮点变量的任何表达式进行初始化。static 局部变量遵循与外部声明相同的规则 [2.2]；extern 不能被初始化。

### 4.3 局部指针变量

指针变量可以用 auto、register、static 或 extern 中的任何一种存储类进行局部声明。前两种可以用在进入复合语句时已定义并且可以赋给整数

变量。静态局部变量遵循与外部声明相同的规则 [2.3]；extern 变量不可以被初始化。

请注意，有很多机会可以把自动变量的地址赋给指针，使得该指针的生命周期长于它所指向的对象。系统不会检查这种情况，对于随后使用无效指针的行为也只有零星的硬件保护。买者自慎。

### 4.4 局部数组

数组变量可以在局部以 auto、static 或 extern 中任一存储类声明。register 请求将不会被接受。也不能在局部声明中初始化 auto 数组；必须编写显式循环或一系列赋值。局部数组的大小必须在编译时已知。

静态数组按照 [2.4] 中给出的相同规则进行初始化。

### 4.5 局部结构体和联合体

结构体或联合体变量可以在局部以 auto、static 或 extern 中任一存储类声明。register 请求将不会被接受。也不能在局部声明中初始化 auto 结构体或联合体；必须编写显式赋值。

静态结构体和联合体按照 [2.5] 中的相同规则进行初始化。

### 4.6 局部函数声明

函数可以在局部声明为无存储类，或声明为存储类 extern 或 static；任何其他声明都是非法的。缺少存储类时被视为 extern，而不是像所有其他局部声明那样视为 auto。如果函数未声明，则被视为返回整数的函数。如果它的任何参数未声明，则相应的实参遵循 [3.6] 中给出的默认强制转换规则。

局部函数声明只是向编译器表明，局部上下文中的该名称意图（通过调用）指代一个同名的外部定义函数。

不允许在另一个函数内部定义函数。

### 4.7 局部声明语法

局部声明的语法是

```
local-declaration = [auto | static | extern | register]_opt type-specifier_opt initializable-declarator-list_opt ;
```

其中存储类和类型说明符必须各自至少出现一个。只有标量项可以被初始化。未初始化的项包含垃圾值。

## 5：参数

> *仅仅是为了提供佐证性的细节，意在给原本平淡无奇、缺乏说服力的叙述增添艺术上的逼真感。*
>
> — W.S. 吉尔伯特，*《日本天皇》*

### 5.0 预处理器

在编译之前，C 程序会被送入预处理器；预处理器在文本中作为控制行提供的显式指令影响下进行文本替换。每个控制行都以 # 开头，位于源代码文本某一行的第 1 列。

最简单的控制行形式是如下形式的简单定义

```
#define identifier {token}
```

或

```
#include file-name
```

例如，

```
#define SIZE_LIMIT 10
```

会使随后出现的标识符 SIZE_LIMIT 被替换为常量 10，而 `#include my_macros` 本身也会被替换，依此类推。例如，如果文件 `lib1` 包含以下行

```
#include defs
#include mylib
```

而文件 `defs` 为

```
#define NMAX    10
#define NEXTCH  getchar( )
#define NMAX2   2*NMAX
```

文件 `mylib` 为

```
char chai[NMAX], matrix[NMAX][NMAX2];
for (i = 0 ; i < NMAX ; ++i)
    chai[i] = NEXTCH;
```

那么以下行

```
#include lib1
```

最终将被替换为

```
char chai[10], matrix[10][2 * 10];
for (i = 0 ; i < 10 ; ++i)
    chai[i] = getchar( );
```

现在可以通过将文件 `defs` 中的前两行改为以下内容来重新定义 `NMAX` 和 `NEXTCH`

```
#define NMAX    5
#define NEXTCH  upper_case(getchar( ))
```

于是，无需改动 `mylib`，这种修改会在重新编译时通过 `mylib` 的文本传播。如果函数 `upper_case` 原先不存在于任何被包含的库中，那么必须以某种方式将其包含进来，但 `mylib`（它可能相当大）不必直接修改。

即使存在 `#include` 语句，编译器诊断信息仍以原始源代码行号为准。事实上，某个被包含文件特有的所有诊断信息都会使用该 `#include` 语句所在的行号。

### 5.1 整数参数

在 C 程序中，通常的约定是使用大写字母命名*参数*，使用全小写字母命名变量。良好的做法是对源代码中除偶尔出现的 0 或 1 之外的所有数字都用 `#define` 定义。应当指出，许多 0 和 1 实际上是神秘值“否”和“是”，因此应相应地标注。

每个程序文件都必须 `#include` 一个标准参数文件，以便即使在中等规模的项目中也能实现充分的源代码控制。

### 5.2 浮点参数

像 e 和 π 这样的值非常适合用于 `#define` 语句，以下这些也是如此：float 和 double 值得保留的位数；可安全求倒数的最大数；以及加到 1.0 上能使其变大的最小数。虽然在编写真正可移植的浮点运算时有许多需要注意的地方，但这些参数朝着这个目标大有帮助。

### 5.3 指针参数

表达式 `&a[MAX-1]` 虽然冗长但很有用。通常值得按如下方式进行参数化：

```
#define MAX 100
#define MAXP &a[MAX-1]
int a[MAX], *p;
for (p = a; p <= MAXP; ++p)
    < do p-th element >
```

用作指针的机器地址，例如在依赖机器的设备驱动程序中，也能受益于恰当的助记符：

```
#define CONSOLE 0177560
if (CONSOLE->status == DONE)
    resume();
```

### 5.4 数组参数

所有数组大小都应使用 `#define` 进行参数化，哪怕只是为了给所选定的上限赋予助记含义。

```
#define MAXLINE 256
char line[MAXLINE];
    for (i = 0; i < MAXLINE; ++i)
        putchar(line[i]);
```

或者，可以巧妙地利用 sizeof 运算符，如下所示

```
#define MAX  (sizeof a / sizeof a[0])
char a[10];
    for (i = 0; i < MAX; ++i)
        a[i] = '\0';
```

注意 `#define` 中使用了圆括号，这样 `MAX` 就可以像表达式中的任何其他项一样使用。除以 `sizeof a[0]` 是从字节数转换为元素个数所必需的。（参见 [3.1]。）

### 5.5 结构体和联合体参数

在多个程序文件中使用的复杂结构体声明，最好保存在一个参数文件中，并按需通过 `#include` 引入。事实上，联合体几乎专门被用作一种以与机器无关的方式参数化多用途结构体的手段。（参见 [0.5.1]。）

sizeof 运算符可用于以高度可移植的方式读写结构体和联合体：

```
write (BINOUT, structure_a, sizeof structure_a);
```

### 5.6 条件编译和参数

控制行也可用于条件编译：

```
#ifdef PDP
    n++;
#else
    n--;
#endif
```

当前有效的定义可以通过如下形式的控制行取消

```
#undef identifier
```

此后，该标识符将不会被替换，直到该标识符随后再次出现定义。经过这样的取消定义后，就 `#ifdef` 或 `#ifndef` 控制行而言，该标识符被视为未定义。例如，

```
#define N 2
int a[N];
#undef N
{float N; ... N = 1.3; ...}
#define N 4
int k = 2 * N;
```

最终会变成

```
int a[2];
{float N; ... N = 1.3; ...}
int k = 2 * 4;
```

请注意，定义会层叠，因此一个参数可以在一个短区间内被 `#define`，然后被 `#undef`，而不会影响该参数在这个区间之前或之后的使用。

`#define` 还可以指定在展开定义时使用的参数。因此，

```
#define swap(x,y) {int t; t = x; x = y; y = t}
```

在每次调用时，其行为就如同

```
swap (a,b)
```

被写成

```
#define x a
#define y b
{int t; t = x; x = y; y = t;}
#undef x
#undef y
```

注意，在定义中，分隔参数列表的左圆括号必须紧邻被定义的标识符，否则该列表将被视为无参数定义的一部分。





### 5.7 语法

预处理控制的完整语法由以下规则给出：

```
program-file =
    {line-group}
line-group =
    [ {source-line} | control-group ]
control-group =
    { #define name {token}
      #define name ( arg-list ) {token}
      #include file-name
      #if | ifdef | ifndef { name } {line-group}
      ( #else {line-group} )opt
      #endif
    }
```

**record_size** 参数是可选的。在某些系统上，当以“直接”（即随机）访问方式打开文件时需要该参数。在这种情况下，约定是先以模式 `"a"` 并指定 **record_size** 创建文件，之后再用模式 `"a"` 和相同的大小读取该文件。

文件通过调用

```
    close(fd)
```

来关闭，其中 **close** 的虚拟声明为

```
    int close(int fd);
```

该调用使文件描述符 **fd** 与外部命名文件解除关联，而这个关联是由之前的 **open** 调用建立的。同样，负返回值表示操作失败。

C 运行时环境提供了三个标准文件，分别用于输入、输出和错误消息，并由以下文件描述符引用：

```
    #define STDIN  0
    #define STDOUT 1
    #define ERROR  2
```

前两个通常与用户的远程终端关联，但可以被重定向；最后一个几乎总是与终端关联，用于错误报告。用户无需打开或关闭这些文件，并且存在默认从 **STDIN** 读取或向 **STDOUT** 写入的 I/O 函数。

函数 **getc** 和 **putc** 的虚拟声明为：

```
    int getc(int fd);
    int putc(int fd, c);
```

其中第一个函数 **getc** 返回文件 **fd** 的下一个字符；如果文件 **fd** 到达文件末尾，则返回 **EOF**，其值为 -1。对 **getc** 的调用会将文件位置推进到所返回字符之后。此外，函数 **backc** 的虚拟声明为

```
    int backc(int fd, c);
```

它把字符 c 放回文件 **fd** 当前的前端，使得下一次调用 **getc** 会得到该被放回的字符。在不调用 **getc** 的情况下连续调用 **backc** 是不允许的，因为放回栈的大小为 1。**putc** 和 **backc** 都会返回发送的字符，这便于编写表达式。

注意，这些函数传输的字符以 int 类型实现。这使得 **EOF** 可以定义为一个不会被误认为有效字符的值。

为了方便经常使用标准文件 **STDIN** 和 **STDOUT** 的程序员，提供了函数 **getchar** 和 **putchar**：

```
getchar() ≡ getc(STDIN)
putchar(c) ≡ putc(STDOUT, c)
```

它们等价于使用默认文件描述符的 **getc** 和 **putc**。

### 6.2 浮点函数

函数 **sqrt** 的虚拟声明为：

```
double sqrt(double x);
```

它返回非负浮点值 x 的平方根的适当精确近似值。对于负数 x，结果是未定义的。

### 6.3 指针

为满足实现链接数据结构所需的动态存储分配，提供了函数 **calloc** 和 **cfree**，其虚拟声明为：

```
char *calloc(int number, size_in_bytes);
cfree(char *p);
```

函数 **calloc** 返回一个指针值，指向内存中大小为 (number * size_in_bytes) 的无类型对象；该指针值可由拥有它的程序操作，直到通过以相同指针值作为参数调用 **cfree** 将该对象释放。预期 **calloc** 和 **cfree** 将用于获取和释放较大的对象空间块，这些空间块将由用户程序进一步切分并进行存储管理。

下面的示例展示了一种可能的做法：

```c
typedef struct node {struct node *n[]; char color[];} NODE;
typedef NODE *NODE_REF;
typedef union {NODE nd; NODE_REF link;} EXTNODE;
static EXTNODE *next_avail;
make_avail(int num) /* make space available for num NODEs */
{
 int k;
 EXTNODE *p1, *p2;
 next_avail = p1 = calloc(num, sizeof(EXTNODE));
 for (k = 1; k < num; ++k)
 {
 p2 = p1 + 1;
 p1 -> link = p2;
 p1 = p2;
 }
 p1 -> link = NULL;
 /* next_avail points to linked list of num NODEs */
}
new(NODE_REF *ndr) /* get new NODE pointed at by ndr */
{
 *ndr = next_avail;
 if (next_avail != NULL)
 next_avail = next_avail -> link;
}
free(NODE_REF *ndr) /* *ndr rejoins available pool */
{
 ndr -> link = next_avail;
 next_avail = ndr;
 /* *ndr = NULL; /* really free it ! */
}
```

如果上述代码构成一个独立的程序文件，那么所有对 NODES 动态池的访问都通过调用 **make_avail**、**new** 和 **free** 完成。当然，类型名 NODE 和 NODE_REF 会在更大的范围内可见。

### 6.4 字符串输入输出

提供了两个函数 **gets** 和 **puts**，用于对整个字符数组进行输入和输出。它们的虚拟声明为：

```c
int gets(int fd, char line[], int max_size);
int puts(int fd, char string[], int size);
```

函数 **gets** 将从文件 fd 前端读取连续的字符来填充字符数组 line，最多不超过 max_size 指定的最大数量。如果在 fd 上遇到 EOF，返回值将为 NULL；否则，返回值是 1 到 max_size 之间的整数，表示实际读取的字符数。

函数 **puts** 会将字符数组 string 中的 size 个字符追加到文件 fd 的末尾。返回值应始终等于 size；否则，可以认为发生了写入错误。

### 6.5 格式化输入输出

提供了三个函数 **cprintf**、**sprintf** 和 **printf**，用于打印数值的字符形式。它们的虚拟声明为：

```
cprintf(int fd, char control[], arg-list);
sprintf(char destination[], char control[], arg-list);
printf(char control[], arg-list);
```

其中 arg-list 是长度可变、类型不可预测的参数序列；在一次调用中，这些参数的实际类型应与 control 对应实参中的某些输出控制项（out-control-item）匹配。函数 **printf** 就是使用默认文件 STDOUT 的 cprintf，而 **sprintf** 与 cprintf 相同，只是转换后的字符数组被放入 destination，而不是发送到文件。

用作 control 的实际参数的字符数组的值应由一系列非 % 字符、%% 或输出控制项组成，其语法为：

```
out-control-item =
% field-specification_opt (| | L)_opt
out-conversion-specification
```

```
field-specification =
  -opt  % left justification within field
  minimum-field-width
  (. subfield-size)opt
minimum-field-width =
  {digit}
subfield-size =
  {digit}  % fractional precision or
           % char array prefix size
```

```
out-conversion-specification =
  %d  % decimal notation
  | h  % short arg -> decimal
  | o  % unsigned octal (no leading 0)
  | x  % unsigned hexadecimal (no 0x)
  | u  % unsigned decimal
  | c  % character
  | s  % character sequence up to null char
       % or maximum subfield-size
  | e  % scientific notation for floating value
  | f  % whole . fraction notation
  | g  % the shorter of e or f
  %
```

arg-list 中的参数应在数量和类型上与相应的 control item 匹配。例如，调用

```
printf('x = %f,k = %d,%s\n',x,k,"what?")
```

可能会在 STDOUT 上打印如下输出行：

```
x = -3.140000,k=307,what?
```

而调用

```
printf('x = %-7.2f,k = %5d\n%-6.3s%\%\n',x,k,"what?");
```

可能打印：

```
x = -3.14   ,k =  307
wha %
```

注意，%% 表示字符 %，而不是 control item 的起始标记。

对于格式化输入，还有三个类似的函数 —— **fscanf**、**sscanf** 和 **scanf** —— 其虚拟声明为：

```
fscanf(int fd, char control[], arg-list);
sscanf(char source[], char control[], arg-list);
scanf(char control[], arg-list);
```

其中 *arg-list* 是指向未知类型的指针列表。

字符数组 **control** 必须具有如下形式：

```
[ % whitespace              % disregarded
| %% | non-%-character       % must match input
| in-control-item ]
```

其中

```
whitespace =
    { blank | newline | tab }

in-control-item =
    % *        % * suppresses assignment
      or
    maximum-field-width
    in-conversion-specification

maximum-field-width =
    {digit}

in-conversion-specification =
    | d        % decimal integer expected
    | o        % octal integer
    | x        % hexadecimal integer
    | s        % character sequence delimited by whitespace
    | c        % next character even if whitespace
    | f        % floating constant
    | [ ^ ] non-]char |
               % string of chars in the sequence
               % or (when ^ present) not in the sequence
    ]
```





### 6.6 退出

exit 函数

```
int exit(int code);
```

终止当前进程，并将控制权交还给最初激活该进程的进程。exit 永不返回。参数 code 是否被使用在很大程度上取决于操作系统。

## 7：机器相关性

### 7.0 机器与系统相关性

本章旨在介绍当前 C 语言实现（RSX-11M 或 UNIX† 下的 PDP-11）中那些未在语言可移植部分定义，但由 PDP-11 硬件或操作系统定义或使其更精确的方面。这些相关性将尽可能在适当的章节中讨论，但以下列表给出了主题的总体概述，并指出详细信息的所在位置：

- (1) 基本类型的硬件表示 [7.1, 7.2, 7.3]
- (2) 基本类型上运算符的硬件实现 [7.1, 7.2]
- (3) 八位字节中的 ASCII 七位字符 [7.1]
- (4) 标识符长度的限制 [7.0]
- (5) 外部或全局名称的处理及库约定 [7.0]
- (6) 加宽、收窄和转换 [7.1, 7.2, 7.3, 7.6]
- (7) 结构体和联合体的内存映射 [7.5]

† UNIX 是贝尔实验室的注册商标。

- (8) 求值顺序 [7.0, 7.6]
- (9) 算术溢出和下溢 [7.1, 7.2]
- (10) 默认约定 [7.1, 7.6]
- (11) 运行时环境；栈和帧的使用；机器寄存器使用；参数和返回值 [7.1]
- (12) register 属性的处理 [7.0, 7.6]

用户从一开始就应该注意的一个相关性涉及外部名称：外部名称将被截断为其前六个字符（在 UNIX 下为七个），因此它们在截断形式下应互不相同。在 RSX-11M 下，外部名称在提交给加载程序时，下划线 '_' 会被替换为 ':'。内部名称的有效长度为 127 个字符。运行时支持例程通常带有 "c." 前缀，因此不能显式调用它们。

编译器确实会利用其自由来选择子表达式的求值顺序，除非语言已定义了顺序。参数的求值顺序请参见 [7.6]。

在每个函数内部，最多有三个 16 位寄存器可用于存储整数值（long int 需要两个），以及两个 64 位浮点寄存器用于存储浮点值。这些寄存器可以通过局部声明中的 register 属性征用。

### 7.1 二进制整数

字符是八位二进制补码整数，但标准字符集是 ASCII 无符号七位值集合。表 7A 给出了带有十六进制等价形式以及常用非图形字符转义序列的 ASCII 字符集。ASCII 的排序顺序对应为从左到右读取各列，并在每列中向下读取。每个列标识符代表十六进制数的第一位数字，而每个行标识符代表第二位。粗体字符表示图形（即可打印）字符，在 C 程序中，它们用单引号括起来。例如，大写字母 zee 写作 'Z'，表示为十六进制形式为 0x5A 的八位整数。

### 表 7A
ASCII 字符和十六进制等价形式

0   1   2   3   4   5   6   7
0   nul dle space 0 @ P ` p
1   soh dc1 ! 1 A Q a q
2   stx dc2 " 2 B R b r
3   etx dc3 # 3 C S c s
4   eot dc4 $ 4 D T d t
5   enq nak % 5 E U e u
6   ack syn & 6 F V f v
7   bel etb ' 7 G W g w
8   bs can ( 8 H X h x
9   ht em ) 9 I Y i y
A   nl sub * : J Z j z
B   vt esc + ; K \ k |
C   np fs , < L \ l }
D   cr gs - = M ^ m ]
E   so rs . > N _ n -
F   si us / ? O - o del

### 表 7B
非图形字符、转义序列和含义

nul \0 空字符（终止字符串）
bs \b 退格
ht \t 水平制表符
nl \n 换行（linefeed）
cr \r 回车
ff \f 换页（新页）
can \30 取消
space \b 空白或空格

多于一个字符的字符常量在空间不足时将在左侧被截断。一个双字符常量将占据普通 int 的左侧（高序）字节和右侧（低序）字节。例如，以下两个赋值是等价的：

```
k = '?A'; k = 0x3F41; /* k an int */
```

因为 ? 对应 3F，A 对应 41。字符常量的长度不能超过 127 个字符。

普通整数和短整数是 16 位或两字节的二进制补码整数（请参阅 PDP-11 硬件手册），而 long int 是 32 位或四字节的二进制补码整数。无符号整数是模 2^16 的 16 位简单无符号正整数。下表给出了整数类型的取值范围：

| 类型 | 最小值 | 最大值 |
|---|---|---|
| char | -128 ... | +127 |
| int (short) | -32,768 ... | +32,767 |
| unsigned int | 0 ... | +65,535 |
| long int | -2,147,483,648 ... | +2,147,483,647 |

整数算术运算符是二进制补码机器上预期的那些运算符，位运算符也是标准的，只是 >> 会用原始左位（即符号位）填充左侧空出的位。

加宽规则保留真实的整数值，但将 int 加宽为 unsigned int 不会转换二进制表示，因此负数 int 将有效地变为 32,768 ... 65,535 范围内的正 int（例如，-1 变为 65,535）。

每当一个较宽的整数值被赋给一个较窄的整数变量或参数时，前缀会被截断；当该值实际上在较窄变量或参数的有效范围内时，此规则保留整数值，但将 unsigned int 收窄为 int 除外，这与上述加宽相反。

从 float 或 double 到整数的收窄转换将保留符号和整数部分（截断小数部分），前提是整数目标具有足够的范围。请注意，float 被认为比 long 更宽，尽管它在基数左侧保留的位数更少。这通常只会在 11/40 或 LSI-11 浮点中引起问题。

整数算术中不进行溢出或下溢检查；会设置位，但不会产生硬件中断，编译后的代码也不会测试这些异常位。

所有非字符值至少占用两个字节，因此从字（两字节）边界开始。这仅意味着变量第一个字节的地址是偶数整数位置。字符可以从任何字节地址开始。

### 7.2 二进制浮点数

类型为 float 或 short double 的值需要 32 位或四字节，分为一位符号、一个无符号八位指数和一个被抑制前导一位的无符号 23 位小数。指数以 128 余码表示，这意味着 128 对应 2 的 0 次幂，129 对应 1，127 对应 -1，依此类推。这让指数的范围约为 10^-38 到 10^+38，精度约为六位十进制数字以上。类型为 double 或 long float 的值具有无符号 55 位小数，精度约为 16 位十进制数字，指数形式和范围相同。

浮点值的算术运算是 PDP-11 硬件支持的标准规范化浮点运算。运行时例程会小心地保持这种形式；例如，如果尾数为零，则整个数为零。

从 float 加宽为 double 会保留值，int 或 char 加宽为 float 或 double 也是如此。如果 long int 的值超过 24 位，从 long int 加宽为 float 可能会丢失重要的数值信息。从 long int 转换为 double 始终保留正确的值。

从 double 收窄为 float 会丢失小数部分的最低有效位。根据指令集选项的不同，可能会或不会进行舍入。与整数算术的情况一样，不执行溢出或下溢检查。浮点值需要两字节边界。

假定在进入任何 C 函数时，FPP 的算术模式是 double（而非 float）和 int（而非 long）。这些模式设置会在从 C 函数退出时保留。在带有浮点选项的 11/40 和 LSI-11 上，浮点算术由硬件指令执行（参见 [7.6]）。所有涉及的算术选项均由对运行时例程的内联调用支持。




### 7.3 指针值

PDP-11 上的有效字节地址范围可以是 1 到 65,535，或十六进制的 0x1 到 0xFFFF；零被保留为空指针值。因此，unsigned int 类似于指针或位置值的表示。

由于所有地址都是字节级的，因此不检查指针类型之间的赋值。如果将一个指向 char 的指针用作指向 int 的指针，这可能引起问题，因为可能导致总线错误。以下赋值或隐含赋值（实参到形参）允许在不转换二进制表示的情况下进行：

- T₁*指针 → T₂*指针
- 指针 → int
- int → 指针

构造 int*expr → 部件名也是允许的。此类偏离正常类型限制的做法应当审慎使用。指针值按两字节边界对齐。

### 7.4 数组

数组不能（作为一个单元）赋值，也不能作为函数的实参或返回值出现，或带有 register 属性。

如果第一个初始化行的大小给出了所需大小，已初始化的数组变量可以有不止一个未指定的有效下标范围。例如，

```
int k[1] = {[2,3], [4], [5,6]};
```

等同于

```
int k[3][3] = {{1,2,3}, {4,0}, {5,6}};
```

不保证这具有可移植性，也不保证对 PDP-11 总是如此。

数组具有与其构造所用元素类型相同的边界要求。数组的 sizeof 是其元素类型的 sizeof 乘以元素个数。例如，

```
double dbl[3][2];
```

有 48 字节 = (3 * 2 * 8)。

字符串常量长度不得超过 127 个字符。

### 7.5 结构和联合

与数组一样，结构和联合不能作为单元赋值，不能作为函数的实参或返回值出现，也不能具有 register 属性。

结构部件到相对位置的映射是通过部件列表从左到右完成的，每个部件尽可能紧密地紧邻前一个部件的末尾对齐。这意味着偶尔可能有一个单字节空洞（即未使用的字节位置）。例如，声明

```
struct {char ch; int k; char str[3];}
```

具有以下布局：

| ch | 空洞 | k | str | 空洞 |

初始边界对齐为两字节，sizeof = 8。

结构继承其限制最严的部件的对齐方式（这里是 k），并且 sizeof 会调整为符合该对齐方式，以便同类型的结构能够无空洞地背靠背排列——因此上述结构末尾有额外的空洞。

联合继承其限制最严的备选部件的对齐方式，其大小等于各部件中的最大大小，并经过调整，以便联合也能背靠背排列。

### 7.6 函数和运行时环境

函数不能将数组、结构、联合或其他函数作为实参或返回值，但允许指向这些对象的指针。在缺少关于函数实参类型的声明信息时，编译器会分别将整数类型或浮点类型的实参假定为 int 或 double。当程序员声明外部函数的实参和返回类型的所有已知信息时，可以获得更好的控制。

特别是，只有通过显式声明所有浮点量为 float，才能最大限度地利用 11/40 或 LSI-11 浮点指令。否则，编译器将调用运行时代码进行许多到 double 的转换，以满足默认类型规则。

实际实参表达式按与调用中指定顺序相反的顺序计算，使得在转移到函数之前，运行时栈看起来像 argₙ、argₙ₋₁、...、arg₁、返回链接。

PDP-11 的八个整数寄存器和四个完全可寻址的双浮点寄存器的典型用法如下：

### 整数寄存器

| PDP-11 值 | 助记符 | 含义 |
|---|---|---|
| 0 | R0 | 整型返回值 |
| 1 | R1 | 或易失值 |
| 2 | R2 | 整型空闲寄存器 |
| 3 | R3 | 可征用 |
| 4 | R4 | 由用户使用 |
| 5 | FP | 函数的帧指针（R5） |
| 6 | SP | 栈指针 |
| 7 | PC | 程序计数器 |

### 浮点寄存器

| PDP-11 值 | 助记符 | 含义 |
|---|---|---|
| 0 | FR0 | 浮点返回值 |
| 1 | FR1 | 或易失值 |
| 2 | FR2 | 浮点空闲（!） |
| 3 | FR3 | 以及可征用 |

在这种寄存器使用方案中，每个 C 函数（无论是编译器构建的还是用户构建的！）都有责任在返回其调用者时，使寄存器 R2、R3、R4、FP、SP、FR2 和 FR3 保持与进入函数时相同的状态。此外，FPP 的模式位必须如 [7.0] 所述为 double 和 int。根据类型，返回值预期如下：

| 类型 | 寄存器 |
|---|---|
| char、int、short int、unsigned int、指针 | R0 |
| long int | R0/R1 |
| floating、double | FR0 |

在没有 FPP 的机器中，float 可以在 R0/R1 中返回，double 结果可以在全局声明的累加器 c.fe 中返回。c.fe 的行为将与 FR0 完全一样；也就是说，在函数调用中它被假定为易失的，并且必须与其他寄存器一起保存，以使代码可重入。还会有一个类似于 FR1 的 c.fe，但可能没有任何可分配且对应于 FR2 和 FR3 的 c.fe。

不假定任何 C 函数返回时条件码有意义。

在大多数实现中，编译器会细致地维护一个栈帧链，使得在任何时候

- 1) FP 是当前帧指针
- 2) 2(FP) 是最近一次调用的返回地址
- 3) 0(FP) 是前一帧指针

对此的例外是为 11/40、LSI-11 浮点选项编译的任何函数。在这种情况下，一种可能的实现如下：

- 1) FP 是当前帧指针
- 2) 6(FP) 是最近一次调用的返回地址
- 3) 4(FP) 是前一帧指针
- 4) 0(FP) 是一个浮点累加器
- 5) -4(FP) 是另一个浮点累加器

## 总结

任何编程语言都是各种装置的集合——字面量、名称、运算符、表达式、声明、数组和结构构造器、函数、顺序控制特性等。但这是一种极其有限的观点。作为构造良好程序的工具，语言应当支持、甚至鼓励现在与良好软件工程实践相关联的各种方法。最重要的是模块化、结构化控制以及数据的系统化组织。

真正的模块化意味着大型程序的各个部分相对独立，并且依赖关系被精确记录。每个部分内部的某些细节（程序逻辑或数据表示）因此对其他部分隐藏。这种封装细节的做法应用于程序逻辑已有一段时间（即子程序），而较近又应用于数据表示（即数据抽象模块）。C 的函数及其形参和局部声明的数据支持程序逻辑的封装；单独编译的程序文件以最少使用外部属性来支持数据表示的封装。

结构化控制意味着一种以顺序、选择和重复为主的程序逻辑规范。为了正确支持这种规范，语言需要一种通用设施，将一组语句组合成一个单元。C 的复合语句提供分组，而 if 和 switch 语句进行选择；重复的系统化控制由 while、do 和 for 语句完成。偶尔需要提前终止重复时，由 break 来满足。

数据的系统化组织包括同类元素的多个副本、由不同类元素构成的复合体、在任何时候可能是若干选择之一的项目，以及创建

访问数据项之间的链接。C 语言的数组、结构体、联合体和指针正是这样做的。

除了前面讨论的主要问题外，程序通过具有可维护性、可移植性和高效性而获益良多。C 语言中的程序可以通过使用定义的参数代替字面量、使用宏 [例如，swap (a,b)] 代替重复代码，以及通过定义常用数据类型（通过 typedef）来提高可维护性。由于 C 语言的大部分内容独立于机器和操作系统，C 程序可以具有很强的可移植性。最后，C 的基本数据类型和运算符在大多数机器上可以直接使用，从而能够生成相当高效的代码。

读者被鼓励将此摘要用作重新阅读 C Notes 的介绍——这次，将语言视为良好程序设计的工具并练习如何以这种方式使用它。

## 索引

-   抽象声明符，62
-   地址运算符，55，67
-   对齐，90
-   歧义，48，50
-   参数，14，27，40，59，66，67，74，85，91
    -   实际参数，59，80，90，91
    -   按值调用和，14
    -   声明，27，32
    -   列表，27，51，59，75，81
-   算术表达式，60，61
-   数组，4，10，11，89–90
    -   参数，59
    -   声明，24–25，56，68
    -   表达式，56–57
    -   初始化器，37–38
    -   重数和，11，24，44，89
    -   字符的，11，12
    -   参数，72–73
    -   语法规则，10–11
    -   变量，89
-   ASCII 字符集，2，3，84，85，86
-   汇编器，2
-   赋值表达式，41，48，50，55，59，62，63，86
-   运算符的结合性，48，63
-   扩充，55
-   自动，17，21，22，93
    -   局部声明，64，65，66，67，68，69
-   回退，77，78
-   二进制浮点数，88
-   二进制整数，85–88
-   位，6
    -   操作，52
-   按位表达式，61
-   break 语句，43，44，45，46
-   字节，6
-   calloc，78，79
-   case 前缀，42，43，46，53
-   强制转换表达式，54，60，62
-   强制转换运算符，49，54，61
-   cclose，77
-   cfree，78，79
-   char，22，24，26，28，32，49，87，92
-   字符：
    -   整数，4，6，7
    -   字面量，4，8，18
    -   字符串，3，11，24
-   C 机器，1
-   强制转换，34，59
-   注释，3，17
-   编译器，1，2，4，25，71，85，90，92
-   复合类型，5，21，23，28–32，67
-   复合语句，28，40–41，43，46，51，64，65，66
    -   语法规则，41
-   条件编译，73，74
-   条件表达式，49，53，60，62
-   常量表达式，24
-   continue 语句，45，46
-   控制行，70，73
-   copen，76
-   cprintf，80
-   cscanf，82
-   数据声明，20，22–26，32
    -   语法规则，22
-   十进制整数，7
-   十进制字面量，17
-   声明符，23，27，28，29
    -   抽象，62
    -   语法规则，28，31
-   默认，9，17，22，28，46，59，64，85
-   default，42
-   #define，70，71，72，74，75，77
-   分隔符，4，18
-   派生类型，5
-   维度，10
-   do 语句，44，45，46
-   双精度类型，4，9，28
-   double，16，23，32，49，87，88，90，92
    -   精度浮点类型，9，21
-   #else，73，74，75
-   else 语句，41，43，46
-   #endif，73，75
-   ERROUT，77
-   转义序列，7，11，18，86
-   exit 函数，83
-   表达式，41，45，47–60
    -   数组，56–57
    -   浮点，54，61
    -   函数，58–60
    -   整数，51–54，60，61
    -   列表，51
    -   指针，34，41，52，53，55–56，57，60，61
    -   结构体，57–58
    -   语法规则，60–62
    -   联合体，58
-   extern，17，21，22，34
    -   局部声明和，64，65，67，68，69
-   外部声明，20–32
    -   参数，27，31
    -   数组，24–25
    -   复合类型，28–32
    -   浮点，23，31
    -   函数，13，14，20，27–28，32
    -   整数，22，31
    -   指针，23
    -   结构体，25–26，31
    -   联合体，26，31
    -   变量和，20，21，22
-   外部声明符，66
-   文件，2，16
    -   程序，20，21，31，34，75，79
-   float，16，23，32，49，92
-   浮点：
    -   声明，23，31
    -   表达式，54，61
    -   函数，78
    -   初始化器，35
    -   字面量，9，18，35
    -   数字，8–9，88
    -   参数，72，88
    -   类型，4，5，8–9，16，23，32，51
    -   变量，25，67
-   for 语句，44，45，46，59
-   格式化输入输出，80–82
-   FPP，88，92
-   函数，4，5，13–16，90–93
    -   调用，41，51，58–60
    -   声明，13，14，20，27–28，31，32，33，68
    -   定义，32，39–45，60
    -   初始化器，45
    -   运行环境和，90–93
    -   语法规则，40
-   基本类型，5
-   getc，77，78
-   getchar，2，4，15，78
-   gets，80
-   全局声明，20–32
-   goto 语句，45，46，64
-   硬件依赖，68，84–89
-   十六进制整数，7
-   十六进制字面量，18
-   标识符，3，17，20，23，25，28，45，59，70，74
-   if 语句，41，43，46
-   #ifdef，73，75
-   #ifndef，74，75
-   #include，70，71，75
-   缩进，43
-   初始化器，20，21，24，33–46
    -   数组，37–38
    -   break，43–46
    -   continue，45–46
    -   浮点，35
    -   goto，45–46
    -   整数，34，35
    -   标签，45
    -   列表，36，37，38，46
    -   指针，36
    -   return，45–46
    -   结构体，38–39
    -   语法规则，33，45–46
    -   联合体，39
-   int，3，22，32，49，90，92
-   整数，4，5–8，14，61
    -   二进制，85–88
    -   字符，4，6，7
    -   十进制，7
    -   声明，22
    -   表达式，51–54，60，61
    -   函数，76–78
    -   十六进制，7
    -   初始化器，34
    -   字面量，4，6，8，17
    -   long，5，6，8，87，92
    -   八进制，7
    -   参数，70–71
    -   主表达式，51
    -   short，4，5，6，87，92
    -   有符号，7
    -   语法，5–8
    -   类型，4，5–8，16，22，32，51
    -   无符号，4，5，7，87，92
    -   扩展，9，35，49，54，59，84，87，88
-   中断语句，42，45，46
-   I/O 函数，76ff.
    -   格式化，80–81
    -   字符串，80
-   关键字，3，16，17，21，49
-   带标签语句，42，45，46
-   词法格式，17
-   程序库，76–83
-   生命周期，22，64
-   字面量，4
    -   字符，4，8，18
    -   十进制，17
    -   浮点，4，8，18
    -   十六进制，4，18
    -   整数，4，6，8，17
    -   long，4，8
    -   八进制，4，17
    -   字符串，4，18
    -   联合体，13
-   装载器，2，3
-   局部声明，41，64–69，85
    -   数组变量和，68
    -   auto，64–69
    -   extern，64–69
    -   浮点变量和，67
    -   函数，68，69
    -   整数变量和，67
    -   初始化和，65
    -   初始化器在，34
    -   指针变量和，67
    -   register，64–69
    -   static，64–69
    -   结构体或联合体变量和，68
-   位置，21
-   逻辑表达式，41，43，44，46，53，61
    -   语法规则，53
-   long，22
-   long int，85，87，88，92
-   长整数，4，5，8
-   长字面量，4，8
-   机器依赖，8，13，51，84–93
-   main，4，6，14，15
-   重数，11，24，44，89
-   名称，3，20，21，64
-   缩窄，49，54，87，88
-   换行，2，7，11，17，86
-   空字符，11，81，86
-   空指针，10，57，89
-   对象，4，10，20，21，64
    -   已知大小的，11，12，13，15，68
-   八进制整数，7
-   八进制字面量，17
-   运算符，4，18，21，29，63
    -   加，48，54，63
    -   地址，55，67
    -   算术，18，19，49，51，54
    -   赋值，48，55，59，63
    -   结合性，48，63
    -   扩充，19，50，54，55
    -   二进制，48，49，51，54，67
    -   按位，18，19，52，63，87
    -   强制转换，49，61
    -   解引用，18，19，55，56，58
    -   相等，19，54，63
    -   相等比较，43，54
    -   整数商，51
    -   位置，18，19
    -   逻辑，19，53，63
    -   乘，48，54，63
    -   部分聚焦，56，58
    -   部分选择，18，19
    -   优先级，48，58，63
    -   关系，19，43，54，63
    -   余数，51
    -   sizeof，6，53，61，73，89
    -   一元，35，48，51，54，63，67
    -   扩展，49
-   可选短语，16，17
-   溢出，8，85，87
-   参数，70–75
    -   数组，72–73
    -   浮点，72
    -   整数，71–72
    -   指针，72
    -   结构体，73
    -   语法，75
    -   联合体，73
-   部分说明，25，26，31
-   PDP-11，84，87，88，89，91，92
-   短语名称，16，17
-   指针，4，9–10，14，21，72，78，89，92
    -   声明，23
    -   表达式，34，41，52，53，55–56，57，60，61
    -   初始化器，36
    -   字面量，10
    -   空，10
    -   参数，72
    -   语法规则，9–10
-   运算符优先级，48，63
-   预处理器，70，71，75
    -   语法规则，75
-   printf，80–81
-   程序文件，16，20，21，23，32，34，75，79
-   程序库，76–83
    -   exit 函数，83
    -   浮点函数，78
    -   格式化输入输出，80
    -   整数函数，76–78
    -   指针，78–79
    -   字符串输入输出，80
-   标点符号，4，18
-   putc，77，78
-   putchar，24，78
-   puts，80
-   递归调用，15，60
-   register，17，21，22，67，85，91
    -   浮点，91
    -   整数，91
    -   局部声明和，64，67
-   重复语句，42，44，46
-   return 语句，45，46，59
-   舍入，88
-   RSX-11M，84，85
-   运行环境，85，90–93
-   标量类型，5，14，27，58
-   scanf，82
-   选择语句，42，46
-   序列表达式，51，62
-   short，22，32，49，87
-   短整数，4，5，26，87
-   有符号整数，7
-   精度损失，8
-   sizeof，6，53，61，73，89
-   sprintf，80
-   sqrt，78
-   sscanf，82
-   栈帧，92
-   语句，40，41，42，43，44，46，59
    -   语法规则，42
-   static，17，21，22
    -   局部声明和，64，65，67
-   STDIN，77，78
-   STDOUT，77，78，80，81
-   存储边界，12–13
-   存储类，4，21–22，64，65
    -   立即，4
    -   可声明，4
-   字符串，4，11，18，24，90
    -   字符，11
    -   输入输出，80
-   struct，23，26，31
-   结构体，12，13，25，32，56，68，73，90
    -   声明，25–26
    -   表达式，57–58
    -   初始化器，38
    -   映射，90
    -   指针，56，57
    -   语法，12–13
    -   标签，26
-   下标，16，56
-   switch 语句，42，43，46，64
-   语法：
    -   数组，10–11
    -   C 程序，16–19，31
    -   声明符，28，31
    -   表达式，60–62
    -   外部声明，20，32
    -   浮点数，8–9
    -   函数，13–16
    -   初始化器，33，46
    -   整数，5–8
    -   局部声明，64，69
    -   指针，9–10
    -   预处理器控制，75
    -   结构体和联合体，12–13，31
-   标记，3，4，9，16，17，20
    -   词法格式，17–18
-   尾随逗号，33
-   截断，87
-   typedef，16，21，29，30，31，32
-   类型，4，5，16
    -   复合，5，23，28–32，67
    -   派生，5
    -   double，4，9，28
    -   浮点，4，5，8–9，16，23，32，51
    -   函数，4，5
    -   基本，5
    -   整数，4，5–8，16，22，32，51
    -   标量，5，14，27，58




- 结构体, 12–13, 25–26
- 联合体, 13, 25
- 类型定义, 16, 20, 29–30, 31, 32, 40, 41, 64
- 语法, 30
- 类型说明符, 16, 22, 23, 64, 65
- #undef, 74, 75
- 下溢, 8, 85, 87
- 下划线, 3, 85
- 联合体, 13, 25, 68, 90
- 声明, 26, 31
- 表达式, 57, 58
- 初始化器, 39
- 内存映射, 84, 90
- 参数, 73
- 联合体, 26
- UNIX, 84, 85
- 无符号, 17, 22, 31, 49, 61
- 无符号整数, 4, 5, 7, 87
- 值, 14
- 变量, 20, 21, 22, 23, 26, 47, 66, 67, 68, 89
- 变量名表达式, 24, 25, 26, 41, 47, 48, 49, 56, 60
- 可见性, 22, 64, 65
- while 语句, 3, 44, 45, 46
- 空白, 3, 4, 9, 11, 82, 86
- 拓宽, 9, 35, 54, 59, 84, 87, 88
- 层次结构, 49

## C NOTES：C 程序设计语言指南

作者：C.T. Zahn

C NOTES 是一本关于高级编程语言 C 的参考手册和教程。正如本书所阐明的那样，C 语言支持结构化程序设计，允许模块分别编译，并包含便于程序维护的重要特性。C 语言与机器无关，却模拟了大多数现代计算机的基本运算符和操作数。因此，C 可以转换为在各种机器上高效且紧凑的代码。

本书主要关注 C 的可移植性方面，并详尽描述了该语言的语法、外部声明和局部声明以及宏预处理设施等主题。

在加入 YOURDON 担任高级顾问之前，C.T. ZAHN 曾就职于斯坦福直线加速器中心的计算研究组，并在那里开发了 SKOL 编程语言。

## YOURDON Press 专著丛书还包括……

### 结构化走查

作者：Edward Yourdon。

《结构化走查》深入探讨了这种新的、非常成功的同行小组评审方法，用于评审功能规格说明、系统设计和代码。在本书的十三章中，你将了解开展走查的流程，以及避免走查使用中常伴随的各种心理问题的方法。走查被认为大幅减少了 DP 系统中的错误数量，并显著提升了系统的整体质量。主题包括：走查类型；编程团队；角色；说服管理层；评估绩效；建设团队；评审练习；参考文献；索引。

152 页，第二版，平装本，1978 年
ISBN: 0-917072-09-X

