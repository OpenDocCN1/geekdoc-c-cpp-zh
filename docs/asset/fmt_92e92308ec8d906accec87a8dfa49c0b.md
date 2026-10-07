
```cpp
class A{
public:
    virtual void p() {
        cout << "A.p" << endl;
    }
    void q() {
        cout << "A.q" << endl;
    }
    virtual void r() {
        p();
        q();
    }
};
class B : public A{
public:
    void p() {
        cout << "B.p" << endl;
    }
};
class C : public B{
public:
    void q() {
        cout << "C.q" << endl;
    }
    void r() {
        q();
        p();
    }
};
```

# 202 第5章 面向对象编程

（续）

```cpp
...
A a;
C c;
a = c;
a.r();
A* ap = new B;
ap->r();
ap = new C;
ap->r();
```

![](img/2603bf9e3f79648236ccbed310226284_213_0.png)

这段代码打印了什么？为什么？详细解释为什么 Java 的多接口继承不会像 C++ 的简单类继承那样遇到问题。

Meyer [1997] 将参数化多态的重载区分如下（同书，第 38 页）：“重载是为客户端程序员提供的一种便利：它使得在运行不同模块对数据结构的不同实现时，能够编写相同的客户端代码。泛型[参数化] 是为模块实现者设计的：它允许他们编写相同的代码来描述同一种数据结构实现的所有实例，并应用于各种类型的对象。”讨论这种关于多态的观点。

## 注释与参考文献

面向对象编程技术的一本很好的参考文献是 [1997]，它使用了非常有意思的面向对象语言 Eiffel，你在本章中还没有学习过它。Budd [1997] 和 Bosch [1994] 以独立于语言的方式描述了面向对象原则。Bruce [2002] 对类型和类提供了有原则的检查。Java 然有很多参考文献，但其中两本强调面向对象原则的是 Arnold et et. [2000] 和 Horstmann [2006]；C++ 在 Stroustrup [1997] 以及 Lippman and Lajo [1998] 中描述。关于 Smalltalk 的书籍包括 Londe [1994]、Lewis [1995]、Sharp [1997] 以及 Lambert and Osborne [1997]。

此处未出的其他面向对象语言通过以下方式描述：Dylan 语言在 Feenberg et al. [1996] 中描述。Eiffel 是一种精心设计的语言，具有类似于 Pascal 的语法（Meyer [1997]）。Modula-3 是 Modula-2 的派生语言，具有面向对象特性（Carelli et al. [1989], Nelson [1991], 以及 Carelli et al. [1992]）。C 是 C 的扩展，带有 Cox [1984, 1986] 设计的面向对象特性。Pascal 的面向对象扩展在 Tesler [1985] 中描述。LISP 的面向对象版本包括 CLOS（Gabriel, White, and Bobrow [1991]）；Loops（Boop and Stetik [1983]）；以及 Flavons（Moon [1986]）。

关于 C++ 模板的使用及其面向对象技术交互的信息可以在 Alexanderescu [2001]；Koenig and Moo [1996]、Josuttitt [1999] 以及 Stroustrup [1997] 中找到。许多研究论文以及面向对象编程技术的报告已出现在 OOPSLA [1986ff] 中。面向对象技术在 C++ 埃拉托尼筛法的应用所示* 这在 Sethi [1996] 中。

# 第6章 语法

| 节次 | 标题 | 页码 |
| :--- | :--- | :--- |
| 6.1 | 编程语言的词法结构 | 204 |
| 6.2 | 上下文文法和 BNF | 208 |
| 6.3 | 解析树和抽象语法树 | 213 |
| 6.4 | 歧义、结合性和优先级 | 216 |
| 6.5 | EBNF 和语法图 | 220 |
| 6.6 | 解析技术与工具 | 224 |
| 6.7 | 词法 vs 语法 vs 语义 | 235 |
| 6.8 | 案例研究：为 TinyAda 构建语法分析器 | 237 |

语法是语言的结构。在第 1 章，我们注意到编程语言语法和语义之间的区别。在编程语言的早期，语言的语法和语义都是通过大量的英语解释和许多示例描述的。虽然语言的语义仍然用英语描述，但编程语言的巨大进展之一是开发了描述语法的正式系统，该系统现在几乎被普遍使用。在 1950 年代，No Chomsky 开发了上下文无关文法的思想，John Backus 在 Peter Naur 的贡献下开发了一种用于描述这些语法的符号系统。

## 6.1 编程语言的词法结构

标记（Tokens）通常分为几类：

- 留关键字，有时称为关键字
- 字面量或常量
- 特殊符号

程序的格式要求某些标记由标记分隔符或空白隔开。例如，正如你刚刚看到的，最长子串原则要求某些标记被隔开。文本行的结束可能具有双重含义，因为它是空白，但它也可以是一个结构实体的含义。缩进也可以在编程语言中用于确定结构。Python 的简单语法依赖于缩进的重要性。

自由格式语言是指对程序结构没有影响的语言（除了满足最长子串原则）。大多数现代语言都是自由格式的，但少数语言有显著的格式限制。

编程语言中的标记（Tokens）通常用英文描述，但也可以通过正则表达式（regular expressions）对其进行形式化描述，正则表达式是对字符模式的描述。正则表达式有三种基本操作：连接、重复和选择。重复通过对需要重复的项目使用星号 `*` 表示，选择通过在待选择的项目之间使用竖线 `|` 表示，连接则通过在不使用显式操作符的情况下排列项目来实现。通常还包含括号以允许对操作进行分组。例如，`[a|b]*` 是一个正则表达式，表示一次或多次重复字符 a 或 b 中的其一（选择），后跟一个单个字符 c（连接）；匹配此正则表达式的字符串包括 `abaac`、`aac`、`babbc` 以及其本身，但不包括 `aaa` 或 `bca`。

正则表达式符号通常通过额外的操作和特殊字符进行扩展，以便于编写。例如，带有连字符的方括号表示字符范围，`+` 表示一次或多次重复，`?` 表示可选，`.` 表示任意字符。通过这些符号，我们可以为相当复杂的标记编写紧凑的正则表达式。例如：

```
[0-9]+
```

是一个用于简单整数常量的正则表达式，它由一个或多个数字（字符 0 和 9）组成。此外，正则表达式：

```
[0-9]+\.\+ [0-9]*?
```

描述了无符号（浮点）字面量，它由一个或多个数字组成，后跟一个可选的小数点部分（使用反斜杠 `\` 即转义字符，以移除点作为匹配任意字符的特殊含义），最后是任意一个或多个数字。

许多工具在文本搜索中使用正则表达式。大多数现代文本编辑器以及各种文件搜索工具（如 UNIX 的 `grep`——"全局表达式打印"）都是如此。该 UNIX 工具还可以用于自动将语言标记的正则表达式描述转换为扫描器（scanner）。（lex 的继任者 flex，也称为 fast lex，可以免费获取并运行在大多数操作系统上。）

虽然研究 lex/flex 以及使用正则表达式构建扫描器超出了本文的范围，但在简单的情况下，可以相对容易地手动构建扫描器。为了让您对这种扫描器的构建有一个直观感受，我们在图 6.1 中展示了一个简单扫描器的代码。该语言中有六种标记（表示为枚举类型，第 4–5 行）：整数由一个或多个数字组成；特殊字符 `+`、`-`、`*`、`.`、 `(`、`)` 以及行尾（在 C 中表示为特殊字符 `\n` 或换行符）。这种语言可用于指定单行输入中带有加法乘法的简单算术表达式，例如：

```
(2 + 34) * 42
```

空白符将被跳过，任何未指定的字符（如 `#` 或 `-`）都被视为错误（因此在文件中需要额外的 `ERROR` 标记）。

在结束此部分并进入语法和解析理论之前，我们注意到图 6.1 代码的以下附加特性。首先，代码包含一个 `main` 函数（第 31–47 行）来驱动扫描器（第 8–30 行）。给定一行输入，`main` 函数只需简单地调用 `getToken()` 并打印每个识别出的标记；数字将打印其唯一的值，错误将打印其违规的第二个字符。我们注意到

## 6.1 编程语言的词法结构

扫描器通过这些全局变量 `numVal` 和 `currChar`（第 6 和 7 行）将额外的数字和字符传递给主程序。更高级的设计将消除这些全局变量并将这些信息封装到包含所有标记信息的数据结构中；参见练习 6.7。

```
(1) #include <ctype.h>
(2) #include <stdio.h>
```

```
(3) /* 作为枚举类型的标记 */
(4) typedef enum {TT_PLUS, TT_TIMES, TT_LPAREN, TT_RPAREN,
(5) TT_EOL, TT_NUMBER, TT_ERROR} TokenType;
```

```
(6) int numVal; /* 计算 NUMBER 标记的数值 */
(7) int currChar; /* 当前字符 * */
```

```
(8) TokenType getToken() {
(9) while (currChar == ' ') /* 跳过空白 *//
(10) currChar = getChar();
(11) if (isdigit(currChar)) /* 识别 NUMBER 标记 *//
(12) numval = 0;
(13) while (isdigit(currChar)) {
(14) /* 计算数值 *//
(15) numval = 10 * numval + currChar - '0';
(16) currChar = getChar();
(17) }
(18) return TT_NUMBER;
(19) }
(20) else { /* 识别特殊符号 */
(21) switch (currChar) {
(22) case '(': return TT_LPAREN; break;
(23) case ')': return TT_RPAREN; break;
(24) case '+': return TT_PLUS; break;
(25) case '*': return TT_TIMES; break;
(26) case '\n': return TT_EOL; break;
(27) default: return TT_ERROR; break;
(28) }
(29) }
(30) }
(31) main() {
(32) TokenType token;
(33) currChar = getChar();
(34) do {
(35) token = getToken();
(36) switch (token) {
(37) case TT_PLUS: printf("TT_PLUS\n"); break;
```

图 6.1 用于简单整数算术表达式的扫描器（续）

# 第 6 章 语法

（续）

```
(38) case TT_TIMES: printf("TT_TIMES\n"); break;
(39) case TT_LPAREN: printf("TT_LPAREN\n"); break;
(40) case TT_RPAREN: printf("TT_RPAREN\n"); break;
(41) case TT_EOL: printf("TT_EOL\n"); break;
(42) case TT_NUMBER: printf("TT_NUMBER: %d\n", numval); break;
(43) case TT_ERROR: printf("TT_ERROR: %c\n", curr_char); break;
(45) while (token != TT_EOL);
(47) return 0;
```

图 6.1 用于简单整数算术表达式的扫描器

# 6.2 上下文文法与 BNF

在英语中，简单句子由一个名词短语和一个动词短语组成，后面跟着句号。我们将其表示为图 6.2 中的语法规则 1。

(1) sentence → noun-phrase verb-phrase .

(2) noun-phrase → article noun

(3) article → a | the

(4) noun → girl | dog

(5) verb-phrase → verb noun

(6) verb → sees | pets

图 6.2 用于简单句子的文法

```
sentence => noun-verb-phrase . (rule 1)
  => article noun-verb-phrase . (rule 2)
  => the noun-verb-phrase . (rule 3)
  => the girl verb-phrase . (rule 4)
  => the girl noun-verb-phrase . (rule 5)
  => the girl sees noun-phrase . (rule 6)
  => the girl sees article noun . (rule 2)
  => the girl sees a noun . (rule 3)
  => the girl sees a dog . (rule 4)
```

**图 6.3** 使用图 6.2 语法的推导

相反，我们可以从句子“the girl sees a dog.”开始，通过图 6.3 的推导反向回溯直到得到 `sentence`，从而证明了该句子在语言中是合法的。

图 6.2 的简单语法实际上展示了编程语言语法的大部分属性。请注意，你不能假设一个句子是合法的，就意味着它在现实语境中是有意义的。例如，“the dog pets the girl”是一个毫无意义但合法的句子。这个例子还包含一个细微的错误：出现在句子开头的冠词应该大写。这种被称为位置属性（positional property）的属性很难用上下文无关文法来表示。此外，我们在句子 `girl sees a dog` 的标记之间之间留了空格。这个问题留给了扫描器（scanner）处理，如前一节所述，扫描器使用空白字符并识别单个标记或单词。（参见练习 6.9.）最后，该语法没有对输入格式规定额外的要求（例如换行符或文件结束标记）。有时我们需要在语法中显式地规定这种后一种条件，编写如下规则：

```
input $\rightarrow $
```

以表示句子后面应该跟着某种结束标记。该标记由美元符号 `$` 表示，可以显式生成，也可以不生成。

让我们花一点为目前为止讨论的标记制定定义。上下文无关文法由一系列规则组成。这些规则又由一个单一短语名称的左侧组成，后面跟着元符号“->”，然后右侧由一个可以替换的项目序列或其他短语名称组成。短语结构的名称（如 `sentence`）称为非终符（nonterminals），因为它们会被分解为进一步的结构。单词或标记符号也称为终符（terminals），因为它们不能被分解。规则也称为产生式（productions），因为它们通过推导“产生”语言的字符串。如果产生式只使用元符号“->"和“|”（有时也允许参数将内容分组在一起），则它们属于 Backus-Naur 形式（BNF）。

如上所述，上下文无关文法还有一个特殊的非终符，称为起始符号（start symbol）。这个非终符代表正在定义的整个顶层短语（如句子或程序），

## 6.2 上下文无关文法和 BNF

它是所有推导开始的符号。上下文无关文法定义了所谓的“文法语言”。这种语言是所有终符字符串的集合，存在从起始符号开始并以终符字符串结束的推导。

图 6.2 包含了七个终符（"girl","dog","sees","pets","the","a" 和 ""）、六个非终符和六个产生式。该语法定义的语言也是有限的，这意味着在 particular语言中可以推导出的句子数量是有限的（参见练习 6.8），但通常由语法定义的语言不是有限的。

通常，上下文无关文法中的产生式数量与非终符的数量相等，尽管可以通过单独编写每个选项来消除元符号符号，例如：

```
noun -> girl
noun -> dog
```

在这种情况下，每个非终符将对应于与选项数量相同的产生式。

为什么这种语法是上下文无关的？简单的原因是非终符单单出现在产生式的左侧。这意味着每个非终符都可以替换为任何右侧内容，无论该非终符出现在哪里。换句话说，不存在在特定上下文下才会发生特定的替换。例如，在讨论的语法中，只有当主语是“girl”时，使用动词“pets”才是合理的；这可以被看作是上下文性。我们可以通过允许上下文字符串出现在文法规则的左侧来写出上下文敏感文法。某些作者认为敏感性是纯粹的语法问题。然而，我们可能采取这种观点：任何无法用上下文无关文法表达的内容通常留给语义描述会更好（即使是一些可以作为上下文无关文法表达的内容，也涉及许多额外的产生式；参见练习 6.30.）。

作为上下文敏感性的一个例子，回想一下，在之前的语法中，句子开头的冠词应该大写。人们可以重写第一个规则为：

```
sentence -> beginning noun-phrase verb-phrase
```

然后添加上下文敏感规则：

```
beginning article -> The | A
```

现在推导过程看起来如下：

```
sentence -> beginning noun-phrase verb-phrase , (new rule 1)
=> beginning article verb-phrase , (rule 2)
=> noun verb-phrase , (new context-sensitive rule)
->
```
