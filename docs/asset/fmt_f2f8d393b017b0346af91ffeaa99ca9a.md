
`chomp($a1=<STDIN>)`

`print "Name another animal: ";`

`chomp($a2=<STDIN>)`

`print "A $a1 and $a2 go for a walk ...n"`

如果这段代码存储在名为 `animals2.pl` 的文件中，则可以如下执行：

```
ahoover@video animals2.pl

Name an animal: turtle

Name another animal: frog

A turtle and frog go for a walk ...

ahoover@video>
```

`chomp` 操作可以在单独的赋值语句中使用，但通常像上面示例那样结合使用。Shell 脚本中用于格式化字符串的特殊符号（`{}`）在 Perl 中的处理方式相似。分号用于分隔 Perl 代码行，通常放在每行的末尾。

为了对输出格式化提供更多控制，Perl 提供了 `printf` 操作。它是基于同名的 C 函数建模的。例如：

```
#!/usr/local/bin/perl

$t=4;

$s="turtles"

$f=1.3;

printf "The %d %s move at %f kph ...n", $t,$s,$f;
```

如果这段代码存储在名为 `animals3.pl` 的文件中，则可以如下执行：

```
ahoover@video animals3.pl

The 4 turtles move at 1.300000 kph ...

ahoover@video>
```

C 语言中用于格式化 `printf()` 语句的大多数符号在 Perl 版本的 `printf` 中可用，且遵循相同的约定。
Perl 提供了访问文件的 `open` 和 `close` 语句。例如：

```
#!/usr/local/bin/perl

$n=42;

open DATA ">data1.txt";

print DATA "History of the world\n"

printf DATA "Answer: %d\n", $n;

close DATA;
```

执行此程序会生成一个名为 `data1.txt` 的文件，内容如下：

History of the world
Answer: 42

`open` 和 `close` 语句的工作类似于 C 语言的 `open()` 和 `close()` 函数，但语法略有不同。I/O 的类型通过文件名前的管道符号来标识：`<` 用于读取，`>` 用于写入，`>>` 用于追加。C 语言文件指针的对等物是 Perl 中的文件句柄（filehandle），它可以在 `print` 和 `printf` 语句中使用，用于指示写入字节的流。可以使用钻石操作符 `<>` 包围文件句柄名称从文件中读取数据。例如：

```
#!/usr/local/bin/perl

open WORLD, "data.txt";

$=<WORLD>; #使用钻石操作符

print ("$s");

close WORLD;
```

如果此程序存储在名为 `redata.pl` 的文件中，那么执行它将产生以下输出：

```
- ahoover@video> redata.pl

(1) History of the world

ahoover@video>
```

每当使用钻石操作符读取一个流时，它都会读取一整行文本，包括换行符。

### 9.3.2 变量

Perl 中有两种主要的变量类型：标量（scalars）和数组（arrays）。标量名字前面有一个美元符号 (`$`)。变量中存储的数据类型并不重要。在内部，所有数据都存储为字符串，所有数值表达式都使用双精度浮点数进行求值，但大多数操作符会自动对变量中的数据进行类型强制转换。例如：

```
#!/usr/local/bin/perl

# 这是一个注释

$x=3;

$y=7.2;

$z="14frog";

$a=$x+$y;

$b=$x+$z;
```

> 5. 在 shell 脚本中，当变量位于赋值的左侧时会省略 `$` 符号，但在表达式或语句中使用变量时会包含它；在 Perl 编程中，无论上下文如何，都始终使用它。这在不同脚本语言之间来回切换可能会引起困惑。

```
$c=$y+$z;

print "$a $b $c\n";
```

如果这段代码存储在名为 `vars1.pl` 的文件中，那么执行它将产生以下输出：

```
ahoover@video> vars1.pl

10.2 17 21.2

ahoover@video>
```

任何以井号 (`#`) 开头的行或行的一部分都被视为注释。当持有字符串数据的变量被用于算术运算时，操作符会尝试将数据转换为数值。在例例中，前两个字符被用于形成数值 14，随后该值被用于运算。其他方便的快捷方式还包括复制和拼接字符串的能力。

```
#!/usr/local/bin/perl

$x="turtle";

$y=$x . $y;

$z=$x . $y;

print "$y $z\n";
```

如果这段代码存储在名为 `vars2.pl` 的文件中，那么执行它将产生以下输出：

```
ahoover@video> vars2.pl

frofrogfrog turtlefrogfrog

ahoover@video>
```

交叉符号 (`x`) 按指定的次数复制前面的文本。点 (`.`) 运算符拼接字符串。

数组变量名字前面有一个 at 符号 (`@`)。数组变量的工作方式与 C 语言数组类似，包含一组连续的、整数索引的值。例如：

```
#!/usr/local/bin/perl

@a=("green frog", "orange tiger", "turtle");

print "@a[0] @a[1] @a[2]\n";

$f=$a[2];

print "$f\n";
```

如果这段代码存储在名为 `vars3.pl` 的文件中，那么执行它将产生以下输出：

```
ahoover@video> vars3.pl

green orange tiger turtle

turtle

ahoover@video>
```

标量变量可以取数组变量中任何单个元素的值。`qw` 运算符提供了一个使用单单词列表初始化数组的方便快捷方式。例如：

```
#!/usr/local/bin/perl

@a=qw /frog tiger turtle /

print "%a[0] @a[1] @a[2]\n"

print "%a\n"
```

如果这段代码存储在名为 `vars4.pl` 的文件中，执行它将产生以下输出：

```
ahoover@video> vars4.pl

frog tiger turtle

frog tiger turtle

ahoover@video>
```

有几种语法可以实现相同的功能，如本例中的两个 `print` 语句所示。范式是，程序员应该在编写代码时使用任何最节省时间的语法；例如，在本例中，第二种语法优于第一种。然而，Perl 中有很多快捷方式。初级程序员不太可能写出最短的代码；随着经验的增加，程序规模和编写时间通常会减少，直到达到某种程度的熟悉。

与大多数脚本语言一样，Perl 中的变量在使用之前不需要声明。然而，Perl 提供了一种种强制执行变量声明的方法。例如：

```
#!/usr/local/bin/perl

use strict;

my $x=3;

my $y=7.2;
```

`use strict` 语句会强制要求在使用变量前声明它。如果不这样做，Perl 将会报错。这有助于避免由于拼写错误导致的 Bug。此外，`my` 关键字用于声明局部标量变量。

### 9.3.3 循环与条件判断

Perl 语言拥有熟悉的 `for` 和 `while` 语句。例如：

```
#!/usr/local/bin/perl

for ($i=0; $i<5; $i++) {

  $t=$i;

}

print "$t\n";

$j=0;

while ($j < 5) {

  $t=$j;

  $j++;

}

print "$t\n";
```

如果这段代码存储在名为 `loops1.pl` 的文件中，那么执行它将产生以下输出：

```
ahoover@video> loops1.pl

10

20

ahoover@video>
```

`foreach` 语句的语法是将参数（在本例中为 `$i`）赋予第二个参数（在此情况下为 1, 2, 3, 4）中的每一个值，并执行循环体。第二个参数可以通过多种方式形成。例如，如果想要一个值范围，使用以下语法通常更短：

```
foreach $i (1..4)
```

这与之前的示例效果相同。列表不需要是连续的值；事实上，它不需要是数值值。例如：

```
#!/usr/local/bin/perl

foreach $i (1,2,"frog","turtle")

{

  print "tiger\n";

}
```

循环代码块的大括号是要求的，即使块只有一行。`next` 语句可以跳转到循环的下一次迭代，而 `last` 语句可以退出循环。这些与 C 语言中的 `continue` 和 `break` 语句工作方式相似。

注意上一个例子，$t 的值在使用之前未被定义。这是 Perl 提供的一种快捷方式。如果未定义的变量被用于数值运算，则其值被假设为 0；如果未定义的变量被用于字符串运算，则其值被假设为空字符串。这种快捷方式允许程序员在跳过变量声明的同时，也跳过变量初始化。

## 第 9 章 • 脚本语言

这段代码简单地打印了四次 "tiger"。最后，第一个参数可以完全省略，使用默认变量名。例如：

这段代码输出 "10"， 与上面的示例相同。它没有定义一个变量名来在每次迭代中存储列表值，而是使用了 `$_`，这是默认的变量名。这种简便方法在 Perl 编程中被频繁使用。

$ 默认变量也可以用于从流中读取数据的 `while` 循环。例如：

```
#!/usr/local/bin/perl

while <STDIN> {

    print "$_";

}
```

为了进行演示，此示例使用了之前创建的 `data.txt` 数据文件。如果此代码存储在名为 `default1.pl` 的文件中，执行它将产生以下输出：

```
ahoover@video> default1.pl < data1.txt

History of the world

Answer: 42

ahoover@video>
```

使用这种语法，`while` 语句从给定的流（在本例中为 STDIN）读取，直到没有更多数据可用。默认变量 `$_` 在每次迭代中被赋予输入行的内容。这为经常执行的任务提供了一种简洁的语法。

Perl 语言拥有熟悉的 `if` 条件语句。例如：

```
#!/usr/local/bin/perl

foreach (1,2,"turtle","frog") {

    if ($_ >= 2) {

        print "number\n";

    }
```

```perl

if ($_ eq "frog") {

    print "animal\n";

}
```

如果此代码存储在名为 `if1.pl` 的文件中，执行它将产生以下输出：

```
ahoover@video> if1.pl

number

animalahoover@video>
```

`if` 语句的语法与 C 语言的 `if` 语句相似，不同之处代码块周围的大括号是强制要求的。如果测试的条件是数值，则使用数学符号（`< <= != >=`）作为运算符。如果测试的条件是文本，则使用字符串（`lt eq ne gt ge`）作为运算符。Perl 语言还有 `else` 和 `elsif` 语句，可以与语句配合使用。

### 9.3.4 模式替换

Perl 语言中最受欢迎的功能之一是模式匹配和替换。在最基础的形式下，它的工作原理类似于文字处理程序中的查找和替换函数。例如：

```
#!/usr/local/bin/perl

$a="Hello Mr. Frog, how are you?";

$a =~ s/Frog/Turtle/;

print "$a\n";
```

如果此代码存储在名为 `pattern1.pl` 的文件中，执行它将产生以下输出：

```
ahoover@video> pattern1.pl

Hello Mr. Turtle, how are you?

ahover@video>
```

操作 `s/Frog/Turtle/` 搜索字符串 `Frog` 并将其替换为字符串 `Turtle`。`=~` 符号对被称为绑定运算符，它要求 Perl 使用左侧的变量对右侧执行操作。

查找和替换操作通常在从 STDIN 流接收的文本上执行。这允许 Perl 程序员使用涉及默认变量名的简便方法。以下数据将用于演示：

Hello Mr. Frog, how are you?
Fine! Thank you Mr. Frog.
How are you Mr. Turtle?
I've seen a lot of frogs today...
Is it a holifrog day?

假设这些数据存储在名为 `data2.txt` 的文件中。以下代码从 STDIN 流获取输入并执行与上一个示例相同的替换：

```
#!/usr/local/bin/perl

while (<STDIN>)

{

s/Frog/Turtle/

  print;

}
```

`while` 语句、查找替换语句或 `print` 语句都没有指示变量名，因为 Perl 使用默认变量名 `$_` 执行所有这些操作。这种简洁的表示法可能会令人困惑，但编写 Perl 程序的目标之一是尽可能缩短程序代码。如果此代码存储在名为 `pattern2.pl` 的文件中，那么在 `data2.txt` 文件上执行它将产生以下输出：

```
ahoover<video> pattern2.pl < data2.txt
```
