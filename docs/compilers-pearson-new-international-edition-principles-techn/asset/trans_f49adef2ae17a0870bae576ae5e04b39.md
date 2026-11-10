
## 2.5 简单表达式的翻译器

```java
import java.io.*;
class Parser {
    static int lookahead;

    public Parser() throws IOException {
        lookahead = System.in.read();
    }

    void expr() throws IOException {
        term();
        while(true) {
            if (lookahead == '+') {
                match('+'); term(); System.out.write('+');
            }
            else if (lookahead == '-') {
                match('-'); term(); System.out.write('-');
            }
            else return;
        }
    }

    void term() throws IOException {
        if (Character.isDigit((char)lookahead)) {
            System.out.write((char)lookahead); match(lookahead);
        }
        else throw new Error("syntax error");
    }

    void match(int t) throws IOException {
        if (lookahead == t) lookahead = System.in.read();
        else throw new Error("syntax error");
    }
}

public class Postfix {
    public static void main(String[] args) throws IOException {
        Parser parse = new Parser();
        parse.expr(); System.out.write('\n');
    }
}
```

图 2.27：将中缀表达式翻译成后缀形式的 Java 程序

### Java 的一些显著特性

那些不熟悉 Java 的读者可能会发现以下关于 Java 的注释有助于阅读图 2.27 中的代码：

- Java 中的类由一系列变量定义和函数定义组成。
- 即使没有参数，也需要用圆括号括住函数参数列表；因此我们写成 `expr()` 和 `term()`。这些函数实际上是过程，因为它们不返回值，这由函数名前的关键字 `void` 表示。
- 函数通过“按值”传递参数或访问共享数据进行通信。例如，函数 `expr()` 和 `term()` 使用类变量 `lookahead` 检查向前看符号，它们都能访问该变量，因为它们都属于同一个类 `Parser`。
- 与 C 一样，Java 使用 `=` 表示赋值，`==` 表示相等，`!=` 表示不等。
- `term()` 定义中的“throws IOException”子句声明可能发生名为 `IOException` 的异常。当函数 `match` 使用例程 `read` 时没有可读取的输入，就会发生这种异常。任何调用 `match` 的函数也必须声明在其自身执行期间可能发生 `IOException`。

## 2.6 词法分析

词法分析器从输入中读取字符，并将它们分组为“词法单元对象”。除了用于语法分析决策的终结符之外，词法单元对象还以属性值的形式携带附加信息。到目前为止，没有必要区分“词法单元”和“终结符”这两个术语，因为语法分析器会忽略词法单元所携带的属性值。在本节中，词法单元是带有附加信息的终结符。

构成单个词法单元的输入字符序列称为*词素*。因此，我们可以说词法分析器根据词法单元的词素表示来实例化词法单元。

本节的词法分析器允许数字、标识符和“空白”（空格、制表符和换行符）出现在表达式中。它可用于扩展上一节的表达式翻译器。由于必须扩展图 2.21 的表达式文法以允许数字和标识符，我们将借此机会也允许乘法和除法。扩展后的翻译方案见图 2.28。

```
expr   →   expr + term     { print('+') }
       |   expr - term     { print('-') }
       |   term

term   →   term * factor   { print('*') }
       |   term / factor   { print('/') }
       |   factor

factor →   ( expr )
       |   num             { print(num.value) }
       |   id              { print(id.lexeme) }
```

图 2.28：翻译为后缀表示法的动作

在图 2.28 中，假定终结符 **num** 具有属性 *num.value*，它给出与此处出现的 **num** 对应的整数值。终结符 **id** 具有一个字符串值属性，写作 *id.lexeme*；我们假定该字符串是构成此 **id** 词法单元实例的实际词素。

用于说明词法分析器工作方式的伪代码片段将在本节末尾汇编成 Java 代码。本节的方法适用于手写词法分析器。3.5 节介绍一个名为 Lex 的工具，它根据规范生成词法分析器。用于保存标识符相关信息的符号表或数据结构将在 2.7 节讨论。

### 2.6.1 去除空白和注释

2.5 节的表达式翻译器会看到输入中的每个字符，因此多余字符（如空格）会导致它失败。大多数语言允许词法单元之间出现任意数量的空白。注释在语法分析期间同样被忽略，因此也可以将它们视为空白。

如果词法分析器消除了空白，语法分析器就永远不必考虑它。另一种做法是修改文法，将空白纳入语法，但这要难实现得多。

图 2.29 中的伪代码通过只要看到空格、制表符或换行符就读取输入字符来跳过空白。变量 *peek* 保存下一个输入字符。行号和上下文在错误消息中有助于精确定位错误；代码使用变量 *line* 统计输入中的换行字符。

```
for ( ; peek = next input character ) {
    if ( peek is a blank or a tab ) do nothing;
    else if ( peek is a newline ) line = line+1;
    else break;
}
```

图 2.29：跳过空白

### 2.6.2 预读

词法分析器可能需要预读一些字符，才能决定要返回给语法分析器的词法单元。例如，C 或 Java 的词法分析器在看到字符 > 后必须预读。如果下一个字符是 =，那么 > 是字符序列 >= 的一部分，即“大于或等于”运算符的词法单元的词素。否则，> 本身构成“大于”运算符，而词法分析器已经多读了一个字符。

在输入上预读的一种通用方法是维护一个输入缓冲区，词法分析器可从中读取字符并回推字符。仅从效率角度就足以证明使用输入缓冲区是合理的，因为一次取一块字符通常比一次取一个字符更高效。指针跟踪已分析的那部分输入；回推一个字符通过向后移动指针来实现。输入缓冲技术将在 3.2 节讨论。

通常一个字符的预读就足够了，因此一个简单的解决方案是使用一个变量（比如 peek）来保存下一个输入字符。本节的词法分析器在收集数字的数字或标识符的字符时会预读一个字符；例如，它会读过 1 以区分 1 和 10，并读过 t 以区分 t 和 true。

词法分析器只在必须预读时才预读。像 `*` 这样的运算符无需预读即可识别。在这种情况下，peek 被设为空白，当调用词法分析器查找下一个词法单元时，该空白将被跳过。本节的不变式断言是：当词法分析器返回一个词法单元时，变量 peek 要么保存当前词法单元的词素之后的字符，要么保存一个空白。

### 2.6.3 常量

只要表达式的文法中出现单个数字，就似乎有理由允许在其位置使用任意整数常量。可以通过为这类常量创建终结符（比如 num）来允许整数常量，也可以将整数常量的语法纳入文法。将字符合集成整数并计算其整体数值的工作通常交给词法分析器，因此在语法分析和翻译期间，数字可以作为单个单元处理。

