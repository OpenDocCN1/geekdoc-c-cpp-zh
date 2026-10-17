
## 第14章 文件 I/O

```perl
#runMenu() -- no arguments
sub runMenu(){
    print (<<MENU);
    Dinosaur Name Period of Existence
    ----------------------------------------
    1. Parasaurolophus        Cretaceous
    2. Tsintaosaurus          Cretaceous
    3. Edmontosaurus          Cretaceous
    4. Allosaurus             Jurassic
    5. Centosaurus            Jurassic
    6. Tyrannosaurus          Cretaceous
    ----------------------------------------
MENU
#4 Obtain Data
print(" Type one of the dinosaur names from the list. $NL >>");
$Input = <STDIN>;
chomp($Input);
$Record = join(" ", $Input);
print(" Type the period of existence. $NL >>");
$Input = <STDIN>;
chomp($Input);
$Record = join(" ", ($Record, $Input));
print " $Record $NL";
}
#9 --------- Definition of checkCycle() ------------
#checkCycle() -- returns y or n
sub checkCycle(){
    print("$NL File written...");
    print("Write another> ( y n )");
    $ControlChar = <STDIN>;
    chomp($ControlChar);
    return $ControlChar;
}
```

在注释 #1 引入的代码行中，你建立了一个 `while` 块，其中包含了程序执行的大部分动作。`checkCycle()` 函数在每次循环重复时都会测试 `while` 循环条件，询问你是否要继续使用该程序。

### 基本的打开、打印和关闭操作

在注释 #2 处，你调用 `runMenu()` 函数。该函数首先显示六种恐龙及其生活时期的列表，如图 14.2 所示。为了显示该列表，正如注释 #3 后面 `runMenu()` 函数的定义所示，你需要创建一个文本块。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_387_0.png)

**图 14.2**  
每次交互循环中，程序都会写入一个文件。

为了收集用户输入，在注释 #4 处（仍然在定义中），你使用一个句柄（`<STDIN>`）并将输入赋值给标识符 `$Record`。通过使用 `join()` 函数，你可以在提示用户输入恐龙名称的基础上，再提示其输入生活时期，并将两个条目连接成一个字符串。你返回这个字符串（`$Record`）。显式的 `return` 语句并非必需，但它有助于展示程序的流程。

回到 `while` 循环中，同样在注释 #2 处，你将 `runMenu()` 函数的返回值赋给标识符 `$LineToWrite`。这样你就可以打开一个文件句柄，将 `$LineToWrite` 的内容写入文件。

要打开文件进行写入，你调用 `open()` 函数。作为其第一个参数，你提供一个文件句柄（`FILE`）。文件句柄可以是任意你选择的名称，按照惯例，你将其大写。`open()` 函数的第二个参数是你要写入的文件（`DinoData.txt`）。在这种情况下，一个文件说明符（`>>`）位于文件之前。该说明符指示 `open()` 函数：如果文件尚不存在，则创建一个文件；如果文件已存在，则打开它，并向其中追加写入的内容。

> 表 14.1 提供的信息在你试验文件读取和写入时至关重要。`>>` 说明符会向你的文件追加数据，但其他说明符会导致文件中已有数据被覆盖。

```perl
#2 Iterate through the lines of the file to the EOF
# and print
while($Line = <FILE>) {
    print("$Line");
}
#3 Close the file
close(FILE) || "Cannot close file: $!";
```

在清单 14_02 的注释 #1 处，你打开文件进行读取。对于文件句柄，你提供一个大写名称；对于文件名，你提供一个常量字符串（`DinoData.txt`）。在注释 #2 处，你创建了一个 `while` 循环，使你能够重复访问句柄所引用的流。通过这种方式，你从流中检索行，并将它们赋给一个标量标识符（`$Line`）。一行是由换行符结尾的文本字符串。这样的行的数量决定了 `while` 循环重复的次数。当 `while` 循环到达 EOF 字符时，循环终止。然后你调用 `close()` 函数来关闭文件。`close()` 函数唯一的参数是文件句柄。图 14.4 提供了这种“原始”数据的视图。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_389_0.png)

**图 14.4**  
调用 `open()` 函数并使用 `while` 循环和句柄就足以检索数据。

### 基本读取与格式化

当你从文件读取数据时，通常需要将其格式化以供显示。为了实现这一点，你可以使用多种方法。除其他方式外，你可以将数据读取到哈希或数组中。清单 14_03 探讨了使用 `split()` 函数将行划分为易于管理的单元。鉴于 `DinosaurData.txt` 中的每一行都由空格和冒号分隔的单词组成，你可以使用 `split()` 函数将每种恐龙的名称、生活时期和科分配给不同的标识符。然后你可以使用 `printf()` 函数来格式化恐龙信息的显示。

```perl
#Listing14_03
#1
$NL = "\n";
$FileName = "DinosaurSourceData.txt";
#make the table heading
makeHeading();

#2 Open the file and designate a file handle
open(FILE, "$FileName") || die "\n Cannot access file. $!";

#3 Iterate through the lines of the file to the EOF
$Count = 1;
while($Line = <FILE>){
    ($Dino, $Period, $Family) = split(":", $Line);
    printf("%2.0f.%-14s %-14s %-14s $NL", $Count++,
        $Dino,
        $Period,
        $Family);
}

#4 Close the file
close(FILE) || "Cannot close file: $!";

print($NL . "-"x$TW . $NL);
############################################################

#----------------------------------makeHeading()--------------------------------------
#3 Formatting elements for the table
sub makeHeading(){
    $NL = "\n ";
    $DC = sprintf("%c",236); #special character
    $TW = 64;    #Table width
    $DL = sprintf( "%55s", $NL . $DC x $TW); #top and bottom lines
    $COLAHEAD = "Dinosaur";
    $COLBHEAD = "Period";
    $COLCHEAD = "Family";
    #Print the header
    print "$NL Dinosaur Information $NL";
    printf("$DL $NL" );
    printf( " %-20s %-16s %16s", $COLAHEAD ,
        $COLBHEAD,
        $COLCHEAD );
    printf("$DL $NL $NL " );
}
```

### 从文件读取数据

清单 14_03 中注释 #1 后面的代码行会打印一个表标题和一条分隔线。在打印标题之前，你定义了一个标识符（`$FileName`），其中包含要访问的文件名。然后调用 `makeHeading()` 函数来设置表标题。它设置了三个列标题。（见图 14.6。）

在注释 #2 处，你调用 `open()` 函数。其参数包括一个文件句柄（`FILE`）和你用文件名定义的标识符（`$Filehandle`）。为了确保在程序无法找到文件时能够生成有用的错误消息，你使用 `die()` 函数。（下一节将讨论 `die()` 函数的使用。）

打开文件后，你就可以从中读取数据。为了完成此任务，如注释 #3 后面的代码行所示，你创建了一个计数器（`$Count`），以便在打印项目时对它们进行编号。你将 `$Count` 初始化为 1。然后启动一个 `while` 块。`while` 语句的控制表达式将从文件中检索到的连续行赋给一个标量标识符（`$Line`）。当控制到达 EOF 字符时，它终止。每重复一次该块，你就调用一次 `split()` 函数。

`split()` 函数的第一个参数是你希望用来划分每一行的表达式。在这种情况下，你使用引号将冒号括起来。在此示例中，冒号用于分隔源文件 `DinosaurData.txt` 中的各项。这种分隔数据的方法使你可以读取包含空格的字符串。图 14.5 显示了源文件中的数据外观。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_391_0.png)

**图 14.5**  
数据可以带有特殊字符存储，以便于格式化。

要将这些项赋给标识符，你使用 `list()` 函数。你使用了三个标识符：`$Dino`、`$Period` 和 `$Family`。随着循环的重复，这三个标识符成为 `printf()` 函数的参数，该函数以左对齐的列打印它们。你还创建了第四列，位于其他列的左侧，用于存放 `$Count` 的值。如图 14.6 所示，通过这种方式，你可以轻松看到已经输入的恐龙名称的数量，以及它们的生活时期和科。

