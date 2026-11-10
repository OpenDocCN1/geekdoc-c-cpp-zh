
## 2.5. 简单表达式的翻译器

然后，消除左递归的变换产生了图2.23中的翻译方案。图2.21中的 *expr* 产生式已被变换为 *expr* 的一个产生式，而一个新的非终结符 *rest* 扮演 *R* 的角色。*term* 的产生式重复自图2.21。图2.24展示了如何使用图2.23中的文法翻译 9-5+2。□

```text
expr → term rest
rest → + term { print('+') } rest
     | - term { print('-') } rest
     | ε
term → 0 { print('0') }
     | 1 { print('1') }
     | ...
     | 9 { print('9') }
```

图2.23：消除左递归后的翻译方案

![](img/a29d16e454785bb105e96ef448ac07f6_75_0.png)

图2.24：将 9-5+2 翻译为 95-2+

消除左递归必须小心进行，以确保我们保留语义动作的顺序。例如，图2.23中的变换后方案在产生式体的中间有动作 { print('+') } 和 { print('-') }，在每种情况下都位于非终结符 *term* 和 *rest* 之间。如果将这些动作移到末尾，即移到 *rest* 之后，那么翻译就会变得不正确。我们留给读者证明：那时 9-5+2 会被错误地翻译为 952+-，即 9-(5+2) 的后缀表示，而不是期望的 95-2+，即 (9-5)+2 的后缀表示。

### 2.5.3  非终结符的过程

图2.25中的函数 *expr*、*rest* 和 *term* 实现了图2.23中的语法制导翻译方案。这些函数模仿相应非终结符的产生式体。函数 *expr* 通过调用 *term*() 然后调用 *rest*() 来实现产生式 *expr* → *term rest*。

```text
void expr() {
    term();  rest();
}

void rest() {
    if ( lookahead == '+' ) {
        match('+');  term();  print('+');  rest();
    }
    else if ( lookahead == '-' ) {
        match('-');  term();  print('-');  rest();
    }
    else { } /* do nothing with the input */ ;
}

void term() {
    if ( lookahead is a digit ) {
        t = lookahead;  match(lookahead);  print(t);
    }
    else report("syntax error");
}
```

图2.25：非终结符 *expr*、*rest* 和 *term* 的伪代码。

函数 *rest* 实现图2.23中非终结符 *rest* 的三个产生式。如果向前看符号是加号，则应用第一个产生式；如果向前看符号是减号，则应用第二个产生式；在所有其他情况下应用产生式 *rest* → ε。*rest* 的前两个产生式由过程 *rest* 中 if 语句的前两个分支实现。如果向前看符号是 +，则通过调用 *match*('+') 匹配加号。在调用 *term*() 之后，通过写出一个加号字符来实现语义动作。第二个产生式类似，只是用 − 代替 +。由于 *rest* 的第三个产生式以 ε 为右部，函数 *rest* 中最后的 else 子句什么也不做。

*term* 的十个产生式生成十个数字。由于这些产生式中的每一个都生成一个数字并将其打印出来，图2.25中的同一段代码实现了它们全部。如果测试成功，变量 *t* 保存由 *lookahead* 表示的数字，以便在调用 *match* 之后将其写出。注意，*match* 会改变

### 2.5.5  完整程序

我们的翻译器的完整 Java 程序出现在图2.27中。图2.27的第一行以 `import` 开头，提供了对包 `java.io` 的访问，用于系统输入和输出。其余代码由两个类 `Parser` 和 `Postfix` 组成。类 `Parser` 包含变量 `lookahead` 以及函数 `Parser`、`expr`、`term` 和 `match`。

执行从函数 `main` 开始，它定义在类 `Postfix` 中。函数 `main` 创建类 `Parser` 的一个实例 `parse`，并调用其函数 `expr` 来解析一个表达式。

函数 `Parser` 与其类同名，是一个*构造器*；当创建该类的对象时，它会自动被调用。从类 `Parser` 开头处的定义可以注意到，构造器 `Parser` 通过读取一个记号来初始化变量 `lookahead`。记号由单个字符组成，由系统输入例程 `read` 提供，该例程从输入文件中读取下一个字符。注意，`lookahead` 被声明为整数，而不是字符，以预见到后续小节中将引入除单个字符之外的其他记号。

函数 `expr` 是2.5.4节所讨论的简化结果；它实现图2.23中的非终结符 `expr` 和 `rest`。图2.27中 `expr` 的代码调用 `term`，然后有一个 while 循环，永远测试 `lookahead` 是否匹配 `'+'` 或 `'-'`。当控制到达 return 语句时，就退出这个 while 循环。在循环内，使用 `System` 类的输入/输出设施写出一个字符。

函数 `term` 使用 Java 类 `Character` 中的例程 `isDigit` 来测试向前看符号是否为数字。例程 `isDigit` 期望作用于一个字符；然而，`lookahead` 被声明为整数，以预见到未来的扩展。构造 `(char)lookahead` 将 `lookahead` 强制转换或强制为字符。与图2.25相比有一处小改动：写出向前看字符的语义动作发生在调用 `match` 之前。

函数 `match` 检查终结符；如果向前看符号匹配，则读取下一个输入终结符，否则通过执行以下代码发出错误信号

```text
throw new Error("syntax error");
```

这段代码创建类 `Error` 的一个新异常，并为其提供字符串 `syntax error` 作为错误消息。Java 不要求在 `throws` 子句中声明 `Error` 异常，因为它们只用于本不应发生的异常事件。⁶

⁶可以使用 Java 的异常处理设施来简化错误处理。一种方法是定义一个新异常，比如 `SyntaxError`，它扩展系统类 `Exception`。然后，当在 `term` 或 `match` 中检测到错误时，抛出 `SyntaxError` 而不是 `Error`。此外，在 `main` 中处理该异常，方法是将调用 `parse.expr()` 包在一个 try 语句中，该语句捕获异常 `SyntaxError`，写出一条消息并终止。我们需要向图2.27中的程序添加一个类 `SyntaxError`。为完成该扩展，除 `IOException` 外，函数 `match` 和 `term` 现在还必须声明它们可以抛出 `SyntaxError`。调用它们的函数 `expr` 也必须声明它可以抛出 `SyntaxError`。

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
            if( lookahead == '+' ) {
                match('+'); term(); System.out.write('+');
            }
            else if( lookahead == '-' ) {
                match('-'); term(); System.out.write('-');
            }
            else return;
        }
    }

    void term() throws IOException {
        if( Character.isDigit((char)lookahead) ) {
            System.out.write((char)lookahead); match(lookahead);
        }
        else throw new Error("syntax error");
    }

    void match(int t) throws IOException {
        if( lookahead == t ) lookahead = System.in.read();
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

图2.27：将中缀表达式翻译为后缀形式的 Java 程序

### Java 的一些显著特性

- Java 中的类由一系列变量和函数定义组成。
- 即使没有参数，也需要用括号括住函数参数列表；因此我们写 `expr()` 和 `term()`。这些函数实际上是过程，因为它们不返回值，这由函数名前的关键字 `void` 表示。
- 函数通过“按值”传递参数或访问共享数据进行通信。例如，函数 `expr()` 和 `term()` 使用类变量 `lookahead` 检查向前看符号，它们都可以访问该变量，因为它们都属于同一个类 Parser。
- 与 C 一样，Java 使用 `=` 表示赋值，`==` 表示相等，`!=` 表示不等。
- `term()` 定义中的“throws IOException”子句声明可能发生名为 IOException 的异常。当函数 `match` 使用例程 `read` 时，如果没有要读取的输入，就会发生这种异常。任何调用 `match` 的函数也必须声明在其自身执行期间可能发生 IOException。

## 2.6  词法分析

词法分析器从输入中读取字符，并将它们分组为“记号对象”。除了用于解析决策的终结符之外，记号对象还以属性值的形式携带附加信息。到目前为止，还没有必要区分“记号”和“终结符”这两个术语，因为解析器忽略记号所携带的属性值。在本节中，记号是终结符加上附加信息。

构成单个记号的输入字符序列称为*词素*。因此，我们可以说词法分析器从记号的词素表示实例化一个解析器。

本节的词法分析器允许数字、标识符和“空白”（空格、制表符和换行符）出现在表达式中。它可用于扩展上一节的表达式翻译器。由于图2.21的表达式文法必须扩展以允许数字和标识符，我们
