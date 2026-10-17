
值由符号`$$`表示，而右部第 n 个符号的值由`$n`给出。（这些值始终是整数，除非另有指定。）例如，在图 6.25 的第 7 行，`$1 + $3`表示产生式右部的第一个和第三个符号的和：

```
expr : expr '+' term
```

因此，右部`expr`和`term`的值被相加。请注意元符号、非终结符和标记的不同约定。

```
(1) %{ 
(2) #include <stdio.h> 
(3) %} 
 
(4) %% 
(5) command : expr '\n' { printf("The result is: %d\n",$1); } 
(6) ;
```

Figure 6.25 YACC/Bison specification of a calculator for simple integer arithmetic expressions (continues)

```c
(7)  expr     : expr '+' term { $$ = $1 + $3; }

(8)           | term { $$ = $1; }

(9)           ;

(10) term     : term '*' factor { $$ = $1 * $3; }

(11)          | factor { $$ = $1; }

(12)          ;

(13) factor   : number { $$ = $1; }

(14)          | '(' expr ')' { $$ = $2; }

(15)          ;

(16) number   : number digit { $$ = 10 * $1 + $2; }

(17)          | digit { $$ = $1; }

(18)          ;

(19) digit    : '0' { $$ = 0; }

(20)          | '1' { $$ = 1; }

(21)          | '2' { $$ = 2; }

(22)          | '3' { $$ = 3; }

(23)          | '4' { $$ = 4; }

(24)          | '5' { $$ = 5; }

(25)          | '6' { $$ = 6; }

(26)          | '7' { $$ = 7; }

(27)          | '8' { $$ = 8; }

(28)          | '9' { $$ = 9; }

(29)          ;

(30) %%

(31) main()

(32) { yyparse();

(33)   return 0;

(34) }

(35) int yylex(void)

(36) { static int done = 0; /* flag to end parse */

(37)   int c;

(38)   if (done) return 0; /* stop parse */

(39)   c = getchar();

(40)   if (c == '\n') done = 1; /* next call will end parse */

(41)   return c;

(42) }

(43) int yyerror(char *s)

(44) /* allows for printing error message */

(45) { printf("%s\n",s);

(46) }
```

**Figure 6.25** YACC/Bison specification of a calculator for simple integer arithmetic expressions

YACC/Bison 从文法生成一个过程`yyparse`，因此我们必须提供一个调用`yyparse`的`main`过程（第 31–34 行）。YACC/Bison 还假设（除单个字符外的）标记由一个名为`yylex`的扫描器过程识别，类似于图 6.24 的`getToken`过程。因此，我们提供一个用 C 编写的`yylex`，它读取并返回一个字符（第 35–42 行）。然而`yylex`与`getToken`的一个不同之处在于，YACC/Bison 只有在`yylex`返回 0 时才会结束分析（在递归下降版本中，我们可以编写特殊代码在换行符上结束分析）。因此，`yylex`包含记住何时到达换行符并在换行符后的下一次调用时返回 0 的代码（允许生成的分析器在完成前直接匹配换行符；参见练习 6.28）。也可以从 LEX/Flex 等扫描器生成器自动生成`yylex`，但我们这里不研究这一点。（有关更多信息，请参阅本章末尾的注释和参考文献。）最后，需要一个错误过程`yyerror`来打印错误消息。

YACC/Bison 不仅对翻译编写者有用，对语言设计者也有用。给定一个文法，它提供了可能的问题和歧义的描述。然而，要阅读这些信息，我们必须对自底向上分析技术有更具体的了解。有兴趣的读者可以参阅本章末尾的注释和参考文献。

## 6.7 词法 vs. 语法 vs. 语义

上下文无关文法通常通过在文法规则中包含构成标记的字符序列来描述语言的标记。例如，在第 6.2 节中引入的部分英语文法中，标记是英语单词`a`、`the`、`girl`、`dog`、`sees`和`pets`，以及`.`字符。在第 6.3 节的简单整数表达式文法中，标记是算术符号`1`和`*`，括号`(`和`)`，以及数字 0 到 9。格式的具体细节，例如第 6.1 节中提到的空白约定，留给扫描器处理，需要作为与文法分开的词法约定来说明。

一些典型的标记类别，如字面量或常量和标识符，并不是本身固定的字符序列，而是由一组固定的字符，如数字 0..9 构建而成。这些标记类别的结构可以用文法定义，例如表达式文法中`number`和`digit`的文法规则。然而，使用扫描器来识别这些结构是可能且甚至是可取的，因为不需要分析器的完整递归能力，扫描器可以通过简单的重复操作来识别它们。使用扫描器可以使数字和标识符的识别更快更简单，并且可以减小分析器的大小并减少文法规则的数量。

为了表达表达式文法中的一个数字应为标记而不是由非终结符表示，我们可以将图 6.18 的文法重写为图 6.26 所示。

```
expr → term { + term }
term → factor { * factor }
factor → ( expr ) | NUMBER
```

Figure 6.26 Numbers as tokens in simple integer arithmetic

通过在新语法中将字符串`NUMBER`大写，我们表示它不是一个按字面意义识别的记号，而是一个其结构由扫描器决定的记号。此类记号的结构必须作为语言词法约定的一部分来指定。如第 6.1 节所述，此类记号的结构可以用正则表达式来指定。然而，许多语言设计者选择将此类记号的结构作为语法的一部分，并认为实现者可以将这些结构放在扫描器而不是解析器中。因此，使用 BNF、EBNF 或语法图来描述一种语言时，不仅可能包括语法，还可能包括编程语言的大部分词法结构（或**词法**）。因此，句法结构和词法结构之间的界限并不总是清晰可辨，而是取决于设计者和实现者的观点。

语法和语义也是如此。我们一直采取这样的观点：语法是任何可以用上下文无关文法定义的东西，而语义是任何不能这样定义的东西。然而，有些作者将我们称之为语义的属性视为语言的句法属性。例如，变量先声明后使用以及过程内标识符不得重复声明等规则。这些规则是上下文相关的，不能写成上下文无关规则。因此，我们更倾向于将它们视为语义规则而非句法规则。

当语言要求某些字符串为**预定义标识符**而非**保留字**时，语法和语义之间就会出现另一种冲突。回顾第 6.1 节，保留字是固定的字符串，它们本身是记号，不能用作标识符。相比之下，预定义标识符是在语言中被赋予预定义含义的固定字符串，但可以通过在程序中重新定义来改变其含义。如前所述，`*if*`、`*while*`和`*do*`在 C、Java 和 Ada 中都是保留字。然而，在 Ada 中，所有基本数据类型名称，如`*integer*`和`*boolean*`，都是可以重新定义的预定义标识符。例如，下面这段 Ada 声明是完全合法的：

```text
integer: boolean;
```

经过此声明后，名称`*integer*`变成了一个`*boolean*`类型的变量。（如果你觉得这很令人费解，有这种感觉的不止你一个。）

另一方面，C、C++ 和 Java 将基本类型如`*int*`、`*double*`、`*bool*`（在 C++ 中）或`*boolean*`（在 Java 中）设为不可重新定义的保留字。这可能是更好的做法，因为这些名称在每个程序中都有固定的语义，即使我们可以改变，也几乎不会想要去改变。

最后，在语言中，当必须使用语义信息来区分歧义解析情况时，语法和语义可能变得相互依赖。一个简单的例子发生在 C 语言中，在解析过程中必须区分类型名和变量名。例如，考虑以下 C 表达式：

```text
(x)-y
```

如果 x 是类型名，则这是将值 −y 强制类型转换为 x。然而，如果 x 是变量名，则这是从 x 中减去 y。因此，解析器必须拥有关于标识符的上下文信息才能消除此类歧义。有人可能会认为这是 C 语法的一个设计缺陷。（Java 也有同样的问题，但 Ada 没有。）然而，在实践中这个问题相对容易解决，正如你将在后续章节中看到的那样。

## 6.8 案例研究：为 TinyAda 构建语法分析器

在本章的最后，我们为一种在某些方面类似于 Ada 编程语言的小型语言开发一个解析器。这种名为 TinyAda 的小型语言既足够大，可以说明许多高级语言的语法特征，又足够小，只需要一个中等规模编程项目来实现。在本节中，我们将通过讨论一个简单的语法分析器来启动该项目。接下来的几章将再次回到该项目，添加代码来分析一些语义。

图 6.27 展示了 TinyAda 的 EBNF 文法。请注意尖括号中的语义限定符，例如`<type>`。你现在可以忽略它们，但我们将在接下来的几章中再讨论它们。

```text
In the following grammar

=     means "is defined as"
" "   enclose literal items
[ ]   enclose items which may be omitted
{ }   enclose items which may appear zero or more times
|     indicates a choice
( )   are used for grouping required choices
< >   enclose semantic qualifications

subprogramBody =
        subprogramSpecification "is"
        declarativePart
        "begin" sequenceOfStatements
        "end" [ <procedure>identifier ] ";"

declarativePart = { basicDeclaration }

basicDeclaration = objectDeclaration | numberDeclaration
                  | typeDeclaration | subprogramBody

objectDeclaration =
        identifierList ":" typeDefinition ";"

numberDeclaration =
        identifierList ":" "constant" ":=" <static>expression ";"

identifierList = identifier { "," identifier }

typeDeclaration = "type" identifier "is" typeDefinition ";"

typeDefinition = enumerationTypeDefinition | arrayTypeDefinition
                | range | <type>name

range = "range" simpleExpression ".." simpleExpression

index = range | <type>name

enumerationTypeDefinition = "(" identifierList ")"

arrayTypeDefinition = "array" "(" index { "," index } ")" "of" <type>name

subprogramSpecification = "procedure" identifier [ formalPart ]

formalPart = "(" parameterSpecification { "," parameterSpecification } ")"

parameterSpecification = identifierList ":" mode <type>name

mode = [ "in" ] | "in" "out" | "out"

sequenceOfStatements = statement { statement }

statement = simpleStatement | compoundStatement

simpleStatement = nullStatement | assignmentStatement
                 | procedureCallStatement | exitStatement

compoundStatement = ifStatement | loopStatement

nullStatement = "null" ";"

assignmentStatement = <variable>name ":=" expression ";"

ifStatement =
        "if" condition "then" sequenceOfStatements
        { "elsif" condition "then" sequenceOfStatements }
        [ "else" sequenceOfStatements ]
        "end" "if" ";"

loopStatement =
        [ iterationScheme ] "loop" sequenceOfStatements "end" "loop" ";"

iterationScheme = "while" condition

exitStatement = "exit" [ "when" condition ] ";"

procedureCallStatement = <procedure>name [ actualParameterPart ] ";"

actualParameterPart = "(" expression { "," expression } ")"

condition = <boolean>expression

expression = relation { "and" relation } | relation { "or" relation }

relation = simpleExpression [ relationalOperator simpleExpression ]

simpleExpression =
    [ unaryAddingOperator ] term { binaryAddingOperator term }

term = factor { multiplyingOperator factor }

factor = primary [ "**" primary ] | "not" primary

primary = numericLiteral | stringLiteral | name | "(" expression ")"

name = identifier [ indexedComponent ]

indexedComponent = "(" expression { "," expression } ")"

relationalOperator = "=" | "/=" | "<" | "<=" | ">" | ">="

binaryAddingOperator = "+" | "-"

unaryAddingOperator = "+" | "-"

multiplyingOperator = "*" | "/" | "mod"
```

**图 6.27** TinyAda 的 EBNF 文法

正如你从文法中看到的那样，TinyAda 包含几种声明（常量、变量、类型和过程）、语句（赋值、选择、循环和过程调用）以及表达式。这种小型语言中的顶级短语称为`subprogramBody`，它是一个过程声明，对于 TinyAda 程序而言，其作用可能类似于 C 语言中的`main`函数在程序执行中的作用。还要注意，声明、语句和表达式的规则是间接递归的，允许嵌套的声明、语句和表达式。

图 6.28 展示了一个简短的 TinyAda 程序，其中包含两个过程声明以及若干常量声明、类型声明、变量声明、语句和表达式。

```text
procedure TEST is

    COLUMN_MAX : constant := 10;
    ROW_MAX : constant := COLUMN_MAX;
    type COLUMN_INDEX is range 1..COLUMN_MAX;
    type ROW_INDEX is range 1..ROW_MAX;
    type MATRIX is array(COLUMN_INDEX, ROW_INDEX) of INTEGER;
```

**图 6.28** 一个 TinyAda 程序（续）
