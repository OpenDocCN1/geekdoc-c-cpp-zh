

## 第12章 函数

```text
#4 --------------- Definition of sortRows() -------------
#sortRows(string for table note)
sub sortRows() {
    %LocalHash = @_; #array passed to a hash

    #Access keys (names of media) and values (percents)
    @DissipationKeys = keys(%LocalHash);
    @DissipationValues = values(%LocalHash);

    #Sort the numbers
    @DissipationValues = sort{$a <=> $b}(@DissipationValues);

    #Use the sorted numbers to reorganize the keys
    foreach $Value (@DissipationValues){
        foreach $Key (@DissipationKeys){
            if($Value == $LocalHash{$Key}){
                #    printf("\n %-30s %-10s", $Key, $Value);
                @OrderedArray = (@OrderedArray , $Key, $Value);
            }#end if
        }#end inner
    }#end outer
    #Return an array in which items are ordered numerically
    return @OrderedArray;
}

#6 --------------- Definition of printTable() -------------
#printTable(@array to print)
sub printTable{
    @SortedMedia = @_;
    for($Itr = 0; $Itr < scalar(@SortedMedia); $Itr += 2){
        printf("$NL %-30s %-10.2f $NL ", $SortedMedia[$Itr],
                                      $SortedMedia[$Itr+1]);
    }
}

# ------------- Definition of printTableNote() -------------
# printTableNote(string for table note)
```

### 上下文环境与返回数组和哈希

```text
sub printTableNote{
    $NL = "\n";
    $CH = "-" x 52;
    #Join elements into a string
    $TableNote = join("$NL ", $NL, $CH, @_);
    #or
    #return($TableNote);
}
```

通过注释#1和#2标识的行，你首先设置了一个存储不同生态介质过滤太阳辐射信息的哈希（%MediaOfDissipation）。你还定义了一个数组，其中包含标识此信息来源的信息。此外，你设置了在图12.14中看到的列标题：介质与%太阳辐射。你必须使用转义序列来显示百分号。

在注释#3处，你调用sortRows()函数，并将%MediaOfDissipation哈希作为其唯一参数传递。sortRows()函数的目的是将哈希转换为数组，并对数组中的项目进行排序，使得代表太阳辐射百分比的数据按升序排列。

为了说明sortRows()执行结果的上下文环境，你将sortRows()的返回值赋给一个数组（@SortedMedia）。上下文环境之间转换的具体细节在注释#4处展开，该注释标识了sortRows()的定义。要重新创建传递给函数的哈希，你将参数数组的内容赋值给哈希标识符%LocalHash。然后调用keys()和values()函数来访问局部哈希中的介质（键）和辐射百分比（值）。

为了对表格的显示结果进行排序，你首先对百分比值进行排序。为此，你调用sort()函数的数值形式，并对@DissipationValues数组中的项目进行排序。该数组随后成为两个foreach语句中外部循环的控制数组。内部foreach语句访问介质的名称。在内部循环中，你使用哈希查找操作，利用百分比从局部哈希中检索介质名称。每次检索时，你都使用if选择语句来确定检索到的百分比是否与百分比数组所建立的升序一致。如果一致，则将百分比及其关联介质名称一同赋给一个新数组（@OrderedArray）。然后显式返回@OrderedArray。

由于包含介质的返回数组现在按照百分比值的升序排列，在注释#3处，你将返回数组赋给@SortedMedia，然后将@SortedMedia作为printTable()的参数使用（见注释#5）。

在与注释#6相关的行中，你定义了`printTable()`。在这种情况下，你将参数数组赋给一个局部数组，只是为了让阅读代码的人更清楚一些。你通过一个重复语句遍历数组中的项目，并使用计数器以2为增量推进。当计数器以2为增量推进时，你可以一次访问两个项目。第一个项目对应于计数器的值。第二个项目是对应于计数器值加1的项目。以这种方式从数组中检索项目，你可以将它们同时作为两个参数传给`printf()`函数。这样，你便按升序显示介质和百分比，如图12.14所示。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_348_0.png)

**图12.14**  
数组和哈希的上下文环境用法使你可以组织项目以便显示。

### 结论

在本章中，你探索了函数的使用。函数提供了一种将构成程序的语句组织成可管理单元的方式。在设置Perl程序时，借鉴结构化编程的一些经验是有益的。因此，你在程序中指定一个空间来放置函数定义。你在程序的另一个区域调用这些已定义的函数。你留出的用于调用函数的区域提供了程序的工作区。通过这种方式设置，你可以在工作区中进行开发活动，同时将已定义的区域保留给那些你认为稳定的代码。

函数的定义范围很广，从没有返回值且不接受参数的函数，到使用许多参数和返回值甚至包含数组和哈希的函数。当你向函数传递值时，是通过Perl参数数组传递的。参数数组将你传递给函数的所有参数转换为一个数组。要访问你作为参数提供给函数的值，必须通过函数定义块中实现的数组操作来检索它们。

要从参数数组中检索值，你可以将数组赋给局部数组或哈希。完成此赋值后，便可以使用标准的数组和哈希函数来执行操作。你在本章中实现的操作包括排序、打印、格式化和执行简单计算。无论执行什么操作，都可以返回结果。返回操作结果时，可以显式使用`return`关键字，也可以让最后执行的操作隐式返回其结果。

此页有意留白

TEAM LinG

## 第13章 引用

本章探讨引用，除其他用途外，引用允许你向函数传递复杂参数，并创建涉及在数组中存储数组或在散列中存储数组的数据结构。引用以直接和间接的方式工作。在直接方式中，你创建一个引用并直接将值赋给它。在间接方式中，你将值赋给一个标识符，然后将该标识符赋给引用。除了为标量、数组和哈希值构造引用外，你还可以创建对函数的引用。除了函数引用，你还可以使用typeglob，这是一种更基本的引用形式。typeglob的一个良好用途是创建常量值。以下是本章涵盖的几个主题：

- 如何创建引用
- 解引用
- 在哈希中存储数组
- 在数组中存储哈希
- 创建和使用函数引用
- typeglob与`ref()`函数

### 引用概述

在之前的章节中，你看到当你创建一个具有多个参数的函数时，这些参数会合并到参数数组中。定义函数时，如果要从参数数组中检索各个元素，必须对参数数组进行解包。如果将一系列标量值传递给数组，你可以通过使用参数数组的索引轻松检索这些值。当你向函数传递几种不同的数据类型时，解包参数数组就变得更加困难。思考一下清单13_01。

