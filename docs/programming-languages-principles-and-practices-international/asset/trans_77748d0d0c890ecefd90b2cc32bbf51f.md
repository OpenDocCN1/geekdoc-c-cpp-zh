

通过在新语法中将字符串 NUMBER 大写，我们表示它不是一个按字面意义识别的记号，而是一个其结构由扫描器决定的记号。此类记号的结构必须作为语言词法约定的一部分来指定。如第 6.1 节所述，此类记号的结构可以用正则表达式来指定。然而，许多语言设计者选择将此类记号的结构作为语法的一部分，并认为实现者可以将这些结构放在扫描器而不是解析器中。因此，使用 BNF、EBNF 或语法图来描述一种语言时，不仅可能包括语法，还可能包括编程语言的大部分词法结构（或**词法**）。因此，句法结构和词法结构之间的界限并不总是清晰可辨，而是取决于设计者和实现者的观点。

语法和语义也是如此。我们一直采取这样的观点：语法是任何可以用上下文无关文法定义的东西，而语义是任何不能这样定义的东西。然而，有些作者将我们称之为语义的属性视为语言的句法属性。例如，变量先声明后使用以及过程内标识符不得重复声明等规则。这些规则是上下文相关的，不能写成上下文无关规则。因此，我们更倾向于将它们视为语义规则而非句法规则。

当语言要求某些字符串为**预定义标识符**而非**保留字**时，语法和语义之间就会出现另一种冲突。回顾第 6.1 节，保留字是固定的字符串，它们本身是记号，不能用作标识符。相比之下，预定义标识符是在语言中被赋予预定义含义的固定字符串，但可以通过在程序中重新定义来改变其含义。如前所述，*if*、*while* 和 *do* 在 C、Java 和 Ada 中都是保留字。然而，在 Ada 中，所有基本数据类型名称，如 *integer* 和 *boolean*，都是可以重新定义的预定义标识符。例如，下面这段 Ada 声明是完全合法的：

```text
integer: boolean;
```

经过此声明后，名称 *integer* 变成了一个 *boolean* 类型的变量。（如果你觉得这很令人费解，有这种感觉的不止你一个。）

另一方面，C、C++ 和 Java 将基本类型如 *int*、*double*、*bool*（在 C++ 中）或 *boolean*（在 Java 中）设为不可重新定义的保留字。这可能是更好的做法，因为这些名称在每个程序中都有固定的语义，即使我们可以改变，也几乎不会想要去改变。

最后，在语言中，当必须使用语义信息来区分歧义解析情况时，语法和语义可能变得相互依赖。一个简单的例子发生在 C 语言中，在解析过程中必须区分类型名和变量名。例如，考虑以下 C 表达式：

```text
(x)-y
```

如果 x 是类型名，则这是将值 −y 强制类型转换为 x。然而，如果 x 是变量名，则这是从 x 中减去 y。因此，解析器必须拥有关于标识符的上下文信息才能消除此类歧义。有人可能会认为这是 C 语法的一个设计缺陷。（Java 也有同样的问题，但 Ada 没有。）然而，在实践中这个问题相对容易解决，正如你将在后续章节中看到的那样。

## 6.8 案例研究：为 TinyAda 构建语法分析器

在本章的最后，我们为一种在某些方面类似于 Ada 编程语言的小型语言开发一个解析器。这种名为 TinyAda 的小型语言既足够大，可以说明许多高级语言的语法特征，又足够小，只需要一个中等规模编程项目来实现。在本节中，我们将通过讨论一个简单的语法分析器来启动该项目。接下来的几章将再次回到该项目，添加代码来分析一些语义。

图 6.27 展示了 TinyAda 的 EBNF 文法。请注意尖括号中的语义限定符，例如 `<type>`。你现在可以忽略它们，但我们将在接下来的几章中再讨论它们。

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

正如你从文法中看到的那样，TinyAda 包含几种声明（常量、变量、类型和过程）、语句（赋值、选择、循环和过程调用）以及表达式。这种小型语言中的顶级短语称为 subprogramBody，它是一个过程声明，对于 TinyAda 程序而言，其作用可能类似于 C 语言中的 main 函数在程序执行中的作用。还要注意，声明、语句和表达式的规则是间接递归的，允许嵌套的声明、语句和表达式。

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

