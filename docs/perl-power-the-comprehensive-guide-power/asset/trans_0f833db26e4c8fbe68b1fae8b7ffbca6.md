

## pack() 函数

`pack()` 函数允许你通过指定要处理的数据类型以及容纳数据所需的字节数来创建固定长度的记录。要创建固定长度的记录，你首先需要确定要创建的记录的长度。假设你想要编写由以下字段组成的记录：

| 字段 | 最大长度 |
| --- | --- |
| 恐龙名称 | 20 个字符 |
| 恐龙科 | 20 个字符 |
| 存在时期 | 20 个字符 |

在调查基本数据后，你决定，如果对构成记录的三个字段使用以下最大长度，则是安全的。

要创建一个容纳这些字段的记录，你采用以下方法：

```perl
$Record = "A20 A20 A20";
my $RecordLength = length(pack($Record));
```

`pack()` 函数检索 `$Record` 标识符提供的信息，并将其“打包”为一个单一值。所提供规范的结果记录长度为 60。现在你可以使用此记录定义将记录写入文件。清单 14.8 在允许你创建包含固定长度记录的文件的上下文中探讨了此活动。该程序每次执行时都会创建文件，并使用记事本打开文件，以便你查看它。

```perl
# Listing 14.8
#1 创建匿名嵌入数组
$DinoRecords = [
    #容器数组
    ['Parasaurolophus', 'Hadrosaurids', 'Late Cretaceous'],
    ['Tsintaosaurus', 'Hadrosaurids', 'Late Cretaceous'],
    ['Allosaurus', 'Carnosaurs', 'Late Jurassic'],
    ['Centrosaurus', 'Carnosaurs', 'Late Jurassic']
];

#2 打印记录以预览它们
#取消引用
@Ref = @$DinoRecords;
#获取容器数组中的项目数
$Length = scalar(@Ref);
#遍历数组并打印其内容
for ($Itr = 0; $Itr < $Length; $Itr++) {
    print("\n");
    $Record = $DinoRecords->[$Itr];
    $NumOfFields = scalar(@$Record);
    for (my $Itr = 0; $Itr < $NumOfFields; $Itr++) {
        printf(" %-20s", $Record->[$Itr]);
    }
}

#3 使用格式。将字段设置为字母长度 20
$Record = "A3 A20 A20 A20";
$RecordLength = length(pack($Record));

print "\n\n Record length:" . $RecordLength . "\n";

#4 打开文件以进行写入 -- 覆盖旧数据
open(FILE, "+>RecordData.txt") || die "\n\tCannot access file.";

#5 将记录写入文件
#遍历数组的两个维度
for ($Itr = 0; $Itr < $Length; $Itr++) {
    print("\n");
    $Record = $DinoRecords->[$Itr];
    #访问每个字段 ...
    $Field = 0;
    $DinoName = $Record->[$Field++];
    $FamilyName = $Record->[$Field++];
    $Period = $Record->[$Field++];
    print(FILE pack("A3 A20 A20 A20", "\n",
        $DinoName,
        $FamilyName,
        $Period));
}

close(FILE);

#6 关闭并查看记录
print "\n File created...";
system('notepad RecordData.txt');
```

在清单 14.8 的注释 #1 处，你定义了一个匿名数组容器。你可以将其识别为数组容器，因为它由包含另一个集合的一组方括号组成。两组索引括号标识了容器 (`$DinoRecords[]->[]`) 。正如清单 14.8 中后面的行所揭示的，你使用指针运算符之前的索引来访问记录，而使用指针运算符所指向的索引来访问记录中的字段。`$DinoRecords` 标识符存储对包含四条记录的容器的引用，每条记录包含四个字段。

注释 #2 之后的行遍历记录及其字段，并在遍历过程中取消引用，并打印图 14.12 显示的表格。每行构成一条记录。行中的每个项代表一个字段。此时你看到的间距不代表字段的指定（固定）长度。在内部 `for` 循环中，你调用 `printf()` 函数并将 20 个字符指定为所有字段的宽度。

创建固定长度记录的工作尚未完成。工作从注释 #3 开始，在那里你设置一个包含四个字段（而不是三个字段）的记录。第一个字段提供一个保留给换行符的三个字符字段。你仅出于美观目的使用换行符字段，这样你在首次查看文件时就可以看到对齐的列（参见图 14.13）。

你指定四列。第一列设置为三个字母字符，其余三列每列设置为 20 个字母字符。你将包含这些规范的插值字符串分配给 `$Record` 标识符。在下一行，你调用 `pack()` 函数来生成记录长度以供显示。你使用 `length()` 函数来检索 `pack()` 函数定义的记录的整数长度。如图 14.12 所示，在将此值分配给 `$RecordLength` 后，你调用 `print()` 函数将其立即打印到屏幕上，紧跟在数据表之后。

在注释 #4 处，你调用 `open()` 函数来打开文件流。你使用流说明符 (`+>`)，如果不存在名为 `RecordData.txt` 的新文件，则打开它；如果已存在同名文件，则覆盖现有数据。打开文件流后，你启动一个 `for` 循环将记录写入文件。

你在此处用于检索记录的方法涉及访问容器数组中每条记录存储的引用。要完成此操作，你使用指针运算符来访问第一个索引的引用 (`$DinoRecords->[$Itr]`) 。你将引用分配给标量标识符 (`$Record`) 。此标识符现在持有一个引用，允许你访问数据字段。

要访问字段，你设置一个计数器 (`$Field`) 。在 `for` 块的每次重复中，你将 `$Field` 标识符设置为零。之后，通过连续三次使用指针运算符和 `$Record` 标识符，你访问字段包含的信息，并将其分配给三个代表性标识符 (`$DinoName`、`$FamilyName` 和 `$Period`) 。然后你将这三个标识符作为参数传递给 `print()` 函数。作为 `print()` 函数的第一个参数，你提供一个换行符。如前所述，这用作装饰元素。

`print()` 函数采用的形式涉及文件句柄标识符 (`FILE`) 作为其第一个参数。你随后跟随由 `pack()` 函数给出的记录字段规范。（在此情况下，你不使用 `length()` 函数，因为你不是要输出整数，而只是要创建记录规范。）你使用之前用于创建数据表后显示值的相同字段值。`for` 循环遍历四条记录后终止。然后你调用 `close()` 函数来关闭文件流。然后，为了查看工作结果，你使用 `system()` 函数调用记事本并显示你创建的文件的内容。图 14.13 显示了结果。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_409_0.png)

**图 14.12**  
在写入数据之前显示数据，并指示你打算创建的记录长度。

清单 14.8 自动调用 `system()` 函数来打开记事本，以便你查看创建的文件，如图 14.13 所示。要退出记事本，请选择“文件” > “退出”。这会保持清单 14.8 的命令窗口打开。按 Return 键退出。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_409_1.png)

**图 14.13**  
程序以固定字段长度将记录写入数据文件。

## 访问固定长度记录

要访问固定长度记录中的数据，你再次使用 `pack()` 函数来确定要读取的记录的长度。然后你使用 `seek()` 函数以等于记录长度的增量导航文件。要了解在哪里找到给定记录，你确定文件中记录的编号，然后将记录长度乘以该编号。你将乘积分配给 `seek()` 函数，并使用记录长度作为 `read()` 函数的参数，检索记录以供查看。清单 14.9 探讨了如何检索特定的固定长度记录。它不引入任何新函数，而是为你提供了机会来尝试已经介绍过的函数的常见用法。

```perl
# Listing 14.9
#从文件读取固定长度记录
#1 验证记录长度
$NL = "\n";
$DC = sprintf("%c", 236);     #特殊字符
$TW = 63;                       #行宽
$DL = sprintf("%63s", $NL . $DC x $TW); #顶部和底部行
open(FILE, "<SourceData.txt") or die ("File could not be opened: $!");
print($DL);

$Record = "A3 A20 A20 A20";
$RecordLength = length(pack($Record));
print "$NL Record length: $RecordLength";

#2 打开数据文件--只读
open(FILE, "RecordData.txt") || die "\n Cannot access file.";

#3 将文件设置在末尾（选项 2）
    seek(FILE, 0, 2);
# 获取长度
    $FileLength = tell(FILE);
    print "$NL The length of the file is $FileLength";
    $NumOfRecords = int($FileLength/$RecordLength);
    print "$NL $NumOfRecords records are in the file.";
    print($DL);
    print "$NL>>Press <Enter>";

#4 使用 seek 和 read 通过乘以长度来获取记录
```

