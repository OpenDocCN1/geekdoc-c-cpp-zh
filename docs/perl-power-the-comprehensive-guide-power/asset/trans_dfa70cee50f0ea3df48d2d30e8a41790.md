

## 第 14 章 文件 IO

在注释 #3 处，你已退出 `while` 循环，并为保险起见再次调用 `tell()` 函数。指针现已推进到文件末尾，因此 `tell()` 函数报告的位置标记了与 `Struthiomimus` 结尾对应的字符位置。要关闭文件流，你调用 `close()` 函数。你提供给该函数的单个参数由文件句柄组成。

在注释 #4 之后的行中，你调用 `print()` 函数并打印摘要数据。`$LengthOfFile` 标识符直接提供来自 `tell()` 函数的信息，而 `$TotalWordLength` 标识符代表你计算的结果。鉴于两个值相等，如图 14.9 所示，你可以得出结论：行（或恐龙名称）的总长度占据了文件的总长度。这就是 `tell()` 函数的工作原理。

### 图 14.9

随着指针推进，`tell()` 函数允许你了解单词长度。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_398_0.png)

## seek() 和 getc() 函数

你使用 `seek()` 函数在文件中定位指针。该函数采用以下形式：

```
Seek(file_handle, offset, [beginning | point_within | end])
```

该函数需要三个参数。第一个参数是文件句柄。第二个参数提供你希望定位指针的文件位置（偏移量）。第三个参数比前两个稍微复杂一些。它允许三个值。它指定你希望将寻找活动的初始位置设置为何。第三个参数的设置如下：

- 0 表示你希望从文件开头开始。
- 1 表示你希望从当前位置（文件中的某个点）开始。

```
#Assign values using an anonymous array reference
#use a hash to capture beginning and end positions
$WordPositions{$Line} = [$WordBeginning, $FileSoFar];

$WordBeginning = $FileSoFar;
}while($Line = <FILE>);

#4 Assign keys to an array and sort
@Dinosaurs = keys(%WordPositions);
@Dinosaurs = sort(@Dinosaurs);

foreach $Name (@Dinosaurs){
    print(" ");
    #5 Use seek() to put the pointer at the start of each word
    # Start the iterator at the pointer position
    # And advance to the end of the word

    # Use reference lookups to retrieve the values
    seek(FILE, $WordPositions{$Name}->[0], 0);

    #6 Use the getc() function to retrieve a character at a time
    for ($Itr = int($WordPositions{$Name}->[0]);
         $Itr < int($WordPositions{$Name}->[1] - 1);
         $Itr++)
    {
        print (getc(FILE));
    }
}

#7 Close out the session
close(FILE) || "Cannot close file: $!";
```

与注释 #1 关联的行允许你以只读（<）文件句柄打开 SourceData.txt。然后你继续（参见注释 #2）定义标识符 $WordBeginning，它在随后的 do...while 循环中充当计数器。要检索文件的第一行，你使用菱形运算符（<>）访问文件句柄并将文件的第一行检索到标识符 $Line 中。

## read() 函数

read() 函数使用三个或四个参数。第一个参数标识文件句柄。第二个参数建立一个字符串标识符，你可以在读取操作期间使用它从文件中提取字符（目标字符串）。第三个参数指定你想要提取的字符数。第四个参数与你想要存储字符的标识符相关（目标字符串）。它指示你在将字符传输到目标字符串时，希望用作起始点的目标字符串中的索引位置。

要使用 read() 函数，你首先调用 seek() 函数来指定起始点。read() 函数从起始点开始读取你指定的字符数。Listing14_07 尝试使用 read() 函数，利用 SourceData.txt 文件中命名恐龙的起始位置和长度。它一次移动一个单词，访问单词，然后将它们按字母顺序放入一个字符串中。

```
#Listing14_07

#1 Open source file
$NL = "\n ";
open(FILE, "<SourceData.txt")
                         or die ("File could not be opened: $!");

#2 Set the first value and advance through the file
$WordBeginning = 0;
$Line = <FILE>;
do{
#3 Obtain word beginnings and ends
    $FileSoFar = tell(FILE);
    #Assign values using an anonymous array reference
    #use a hash to capture beginning and end positions
    $WordPositions{$Line} = [$WordBeginning, $FileSoFar];
    $WordBeginning = $FileSoFar;
}while($Line = <FILE>);

#4 Assign keys to an array and sort
@Dinosaurs = keys(%WordPositions);
@Dinosaurs = sort(@Dinosaurs);

$Str = 0;
foreach $Name(@Dinosaurs){
```

```
#5 Reset the pointer to the start of the word
seek(FILE, $WordPositions{$Name}->[0], 0);
read(FILE,
    $DinosaurName,
    ($WordPositions{$Name}->[1]-1) - ($WordPositions{$Name}->[0]),
    0);
$Itr++;
$FinalString = join( " ", $FinalString, $DinosaurName);
}
#7 Close out the session
close(FILE) || "Cannot close file: $!";
# Print the alphabetical string
print "$FinalString";
```

有关你在 Listing14_07 中执行的任务的具体讨论，请参见前一节“seek() 和 get() 函数”中由注释 #1 到 #5 指定的行。

在 Listing14_07 的注释 #5 处，你已进入一个 foreach 重复块，用于检索 @Dinosaurs 数组中每个恐龙的名称。@Dinosaurs 数组包含 %WordPositions 哈希中所有恐龙的字母顺序名称。foreach 选择语句从 @Dinosaur 数组中检索每个恐龙名称，并将其分配给 $Name 标识符。

当你调用 seek() 函数时，你会重新定位文件指针，使其指向当前分配给 $Name 的恐龙名称的第一个字符。要获取 seek() 函数所需的第一个字符的位置，你将 $Name 用作哈希查找操作中的键，并将其用作 seek() 函数的第二个参数。seek() 函数将指针移动到该位置，然后你就可以调用 read() 函数，该函数将检索构成恐龙名称的所有字符。

seek() 函数将文件指针定位在恐龙名称的开头。read() 函数（与 getc() 函数类似，请参见前一节的讨论）从调用它时有效的指针位置开始读取文件。

鉴于 read() 函数仅在调用时知道其位置，你必须向其提供有关你希望它读取多少字符以及读取后要对字符做什么的信息。因此，你向 read() 函数提供四个参数。

正如注释 #5 之后的行所揭示的，第一个参数由文件句柄标识符（`FILE`）组成。第二个参数提供一个标量标识符（`$DinosaurName`），你可以将 `read()` 函数从文件中检索到的字符串分配给它。最后（第四个）参数涉及此标识符。设置为零时，此参数告诉 `read()` 函数使用目标标识符（`$DinosaurName`）的零索引作为它复制到该标识符的字符串的起始位置。通常，此参数指定你希望将从文件中复制的字符串传输到的目标字符串中的位置。

对于 `read()` 函数的第三个参数，你提供你希望 `read()` 函数从文件中检索的字符数。要实现这一点，你使用一个涉及将一个解引用值减去另一个解引用值的表达式。以下是该表达式：

```
`$WordPositions{$Name}->[1]-1) - ($WordPositions{$Name}->[0])`
```

你使用 `$Name` 标识符来识别 `%WordPositions` 哈希中的给定键（恐龙名称）。使用该键，你检索与该键关联的数组。该数组包含两个元素。第一个元素（索引 0 处）提供恐龙名称第一个字符的位置。第二个元素（索引 1 处）告诉你文件中恐龙名称末尾字符之后一个字符的位置。要获取恐龙名称的长度，你从末尾减去 1，然后从末尾减去开头。差值告知 `read()` 函数要从文件传输到 `$DinosaurName` 标识符的字符数。

鉴于你已将恐龙名称分配给 `$DinosaurName` 标识符，你随后调用 `join()` 函数将恐龙名称与其他恐龙名称连接成一个字符串（`$FinalString`）。在连接名称时，你在恐龙名称之间插入一个短横线作为装饰功能。

在 `foreach` 语句遍历数组中的所有名称后，其块终止，你关闭文件流。要关闭文件流，你使用 `close()` 函数（参见注释 #6）。之后，你调用 `print()` 函数并将 `$FinalString` 作为其唯一参数提供。图 14.11 显示了结果。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_405_0.png)

**图 14.11**  
使用 `read()` 函数检索数据并创建一个你打印到显示器的字符串。

