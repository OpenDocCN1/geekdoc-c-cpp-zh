

## 4.4.5 Conditional statements

ACD中有三种条件语句：一元、三元和案例型。

### 4.4.5.1 Unary conditional statements

一元条件的典型用途是开启或关闭提示。假设只有当序列被确定为蛋白质时才应提示输入窗口大小。实现此功能的ACD如下所示：

```
sequence: sequence
[
  parameter: "Y"
  type: gapany
]

integer: window
[
  standard: "$(sequence.protein)"
  etc
]
```

如果序列是蛋白质，则所需语句等效于：

```
standard: "Y"
```

并开启提示。如果序列是核酸，则语句等效于：

```
standard: "N"
```

这将有效地禁用提示。控制提示在其他地方有详细描述（第4.5节，“控制提示”）。

### 4.4.5.2 Ternary conditional statements

三元条件语句的一般形式为：

```
@(conditional ? value-if-true : value-if-false)
```

当为应用程序设置两种不同的使用模式时，它们很有用，例如在排列程序中为蛋白质和核酸设置不同的间隙罚分值。下面的示例将蛋白质的罚分设置为14，核酸的罚分设置为16：

```
integer: penalty
[
  standard: "N"
  default: "@($(sequence.protein) ? 14 : 16)"
  etc
]
```

### 4.4.5.3 Case conditional

在案例型操作中，测试值与一系列可能值进行比较。如果找到匹配项，则操作将解析为与该可能值关联的结果。测试值作为字符串解析，后跟等号（=），等号后跟一个或多个由冒号（:）分隔的可能值和关联值对。如果没有可能值匹配，则操作将解析为与关键字else关联的默认结果。

else : 默认值对不是强制性的，如果在没有默认值的操作中没有可能值匹配，则操作将解析为NULL。

其形式化如下：

```
@(testval = poss_valA : ass_valA
poss_valB : ass_valB
else : default_val)
```

例如：

```
string: matrix
[
    default: "@($(sequence.type) =
    protein : BLOSUM62
    dna : dnamat
    rna : rnat
    else : unknown)"
]
```

$(sequence.type)变量是一个字符串值，保存名为sequence的ACD数据项的序列类型。如果类型是protein，则操作解析为BLOSUM62；如果类型是dna，则解析为DNAMAT。如果类型不在此列表中，则操作解析为unknown。

如果测试值无法明确分配给单个关联值，则操作将解析为与其可能值匹配的最后一个关联值。

### 4.4.6 Use of variables

变量用于保存部分计算或值，很有用。其一般语法为：

```
VariableName : Variable value
```

请注意，由于变量只有一个值且没有属性，因此不使用方括号。

例如，以下是确定序列窗口最大大小的计算：

```
integer: start
[
    standard: "Y"
    maximum: "@(@($(sequence.length) - $(window)) + 1)"
]
```

可以通过将其中一个计算存储为部分结果来整理，如下所示：

```
variable: lminusw "@($(sequence.length) - $(window))"
integer: start
[
    standard: "Y"
    maximum: "@($(lminusw) + 1)"
]
```

在以下ACD代码中，内部ACD变量protlen用于存储中间结果。变量$(protlen)的值从输入序列（sequence数据类型）的长度计算得出，并用于定义窗口参数的最大大小：

```
variable: protlen "@( $(sequence.length) / 3 )"
integer: window
[
    maximum: "@($(protlen)-50)"
    default: 50
]
```

使用嵌套操作如下所示也可以实现相同的结果：

```
integer: window
[
    maximum: "@( @( $(sequence.length) / 3) - 50)"
    default: 50
]
```

窗口参数直接从sequence.length变量（计算属性）计算得出，方法是将除法算术操作嵌套在单独的减法操作中。

变量可用于简化ACD文件，使其更易于读取和解析。ACD文件可以使用变量定义仅定义一次结果，然后在所有后续ACD数据类型定义中按名称引用该变量。

### Caution

使用变量可能表明ACD定义中存在一定的复杂性。当使用变量，或当条件操作引用另一个ACD值时，应用程序在逻辑上可能被视为由解析的条件分叉的两个或多个独立应用程序。

### 4.4.6.1 Automatic variables

目前只有一个这样的变量（acdprotein），它根据读取的第一个序列的类型设置为true或false。

## 4.5 Controlling the prompt

### 4.5.1 Introduction

可靠地提示用户输入值是任何应用程序界面的关键部分。EMBOSS允许您精确控制应用程序参数的提示方式，从而为您节省大量开发时间。这是通过使用ACD数据属性实现的：

- parameter: "Y"表示该数据项是一个参数，即您不必在命令行上使用数据标签来为其指定值，例如myprog 10。
- standard: "Y"和additional : "Y"表示该数据项是一个限定符，即您必须在命令行上使用数据标签来为其指定值，例如myprog -somevalue 10。如果数据定义未定义为参数，或标准或附加限定符，则它将默认为高级限定符。

如果未在命令行上指定，参数和标准限定符的值始终会提示（带有其默认值）。除非在命令行上给出-options，否则不会提示附加限定符的值（将使用默认值）。ACD文件中应始终给出附加限定符的默认值。高级限定符的值永远不会提示。

### 4.5.2 Parameters

请考虑以下ACD文件，用于名为helloworld的应用程序，它定义了两个参数，即字符串输入（string数据类型）和输出文件（outfile数据类型）：

```
application: helloworld
[
    documentation: "Prints something arguably uninteresting"
]

string: message
[
    parameter: "Y"
]

outfile: outfile
[
    parameter: "Y"
]
```

参数的值必须在命令行上按照它们在ACD文件中出现的顺序指定。因此，要为helloworld指定两个参数，您需要输入类似：

```
helloworld "Hello World!" message.dat
```

这将导致Hello World!被打印到输出文件message.dat。或者，使用以下任一命令也是完全可以接受的：

```
helloworld -message "Hello World!" -outfile message.dat
helloworld -outfile message.dat -message "Hello World!"
helloworld -message "Hello World!" message.dat
```

对于参数，您不必使用名称标志，而对于限定符则必须使用。如果省略参数的标志，则它们的值*必须*在命令行上按照它们在ACD文件中出现的顺序出现。

但是，您可能不想强制用户指定消息，而是依赖ACD文件中定义的默认消息（“Hello World!”）在未给出其他内容时打印。因此，通过输入：

```
helloworld message.dat
```

您希望“Hello World!”（默认消息）被打印到文件message.dat。

上述ACD文件不会这样做。所有数据定义都是参数（parameter：），因此如果未在命令行上给出，则会提示输入。输入上述命令会导致message.dat被当作要打印的字符串，然后您将被提示输入输出文件名。简而言之，不是所需的行为。这时就需要限定符了。

### 4.5.3 Qualifiers

限定符（无论是“标准”、“附加”还是“高级”）的值可以出现在命令行上的任何位置，但您必须始终通过其标志引用它们。因此，如果您的消息定义为限定符而非参数，则对它的引用必须如下所示：

```
-message "Hello World!"
```

要将数据定义指定为限定符，您使用standard:或additional:，而不是当前指定的parameter:属性。或者，如果您未指定这些属性中的任何一个，它将默认为高级限定符。例如：

```
application: helloworld
[
    documentation: "Prints something arguably uninteresting"
]
string: message
[
    standard: "Y"
]
outfile: outfile
[
    parameter: "Y"
]
```

