
## 扩展哈希应用

最终的分片操作与注释 #6 相关联。在那里，你单独使用列表函数。为了实现分片，你将一个哈希列表赋值给目标哈希。唯一的规定是，所赋值列表中的第一个哈希必须是目标哈希。在这种情况下，目标哈希是 `%Elements`。图 9.4 说明，当你打印 `%Elements` 的内容时，你会获得 Listing09_04 中所有哈希的所有元素。

**图 9.4**  
分片操作允许你合并哈希。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_236_0.png)

### 将字符串转换为哈希

你可以使用 `split()` 函数将字符串转换为哈希。当你处理以字符串形式到达的互联网传输结果时，这个过程非常有用。`split()` 函数接受两个参数。第一个参数指定用于分隔字符串中各项的表达式。第二个参数是你想要操作的字符串。Listing09_05 提供了一个如何将字符串转换为哈希的示例。在此示例中，字符串由用冒号连接的键值对组成，逗号分隔这些键值对。

**Listing09_05**

```perl
#1 Set up the data using an implicit hash
#It is important not to introduce extra line returns and the like ...
$ElementsString = "Aluminum:659, Carbon:3600, Chromium:1615, Copper:1083, ".
"Gold:1946, Hydrogen:-259, Iron:1530, Lead:327, " .
"Magnesium:670, Manganese:1260, Nickel:1452, " .
"Phosphorous:44, Silicon:1420, Silver:961, " .
"Tin:232, Titanium:1795, Tungsten:3000, Zinc:419";

#2 Use the split() function and a regular expression to split
#the string. The expression calls for a comma followed by a space
@ElementList = split(", ", $ElementsString);

$ListLength = scalar(@ElementList); #read length of array
print "\nNumber of items : $ListLength\n";

# 3 At the colons, separate the elements and melting points
# The expression calls for a colon with no spaces
foreach $Item (@ElementList){
    ($Element, $MeltingPt) = split(":",$Item );
        # Two steps that could be one: create a hash with the two parts
        $NewElementList{$Element} = $MeltingPt;
}#end foreach

# 4 Print the hash as a string; use each to retrieve keys and values
print "\nThe element list follows:\n";

$Itr = 1;
while (($Element, $MeltingPt) = each(%NewElementList)){
    printf "\n %-4s %-25s %-10.0f", $Itr++, $Element, $MeltingPt;
}#end while
```

Listing09_05 中注释 #1 对应的行创建了一个字符串，其中包含多种化学元素及其熔点。逗号分隔构成该字符串的元素-温度对。为了在本书中显示此程序，有必要将字符串拆分为一组串联的元素。你可以从中得到一个教训：不要向要拆分的字符串中引入换行符，这一点仍然至关重要。`split()` 函数通常会处理你的字符串，但除非你另行指定，否则它会假定你希望保留转义序列不变。这可能会带来问题。

在注释 #2 指定的行中，你使用 `split()` 函数将字符串划分为由元素-值集合组成的项。为了拆分字符串，你向 `split()` 函数提供的第一个参数是逗号后跟一个空格。你用双引号将它们括起来。（你也可以使用正斜杠（`//`）、`q()` 函数、`qq()` 函数或单引号。）`split()` 函数返回按约定拆分字符串后得到的项，并将这些项赋值给数组 `@ElementList`。你使用 `scalar()` 函数确定数组中的项数，正如图 8.14 所示，你打印这个数量，以便对照它检查显示的元素。

在注释 #3 处，你使用 `foreach` 控制语句遍历 `@ElementList` 数组中的项。`foreach` 语句允许你访问数组中的每个项，并将其赋值给标量 `$Item`。在 `foreach` 块内，你再次使用 `split()` 函数来分离 `$Item` 标识符临时存储的元素和温度组成部分。为此，你提供给 `split()` 函数的第一个参数是由双引号括起来的冒号。

你将 `split()` 函数的返回值赋值给由两个标量标识符（`$Element`、`$MeltingPt`）组成的列表。然后，你将这两个元素提供给以 `%NewElementList` 哈希为特征的查找哈希操作。在花括号之间，`$Element` 标识符为每个哈希项提供键，`$MeltingPt` 标识符提供所赋的值。

在注释 #4 处，你将 `each()` 函数的返回值作为 `while` 控制语句中的参数，以遍历 `%NewElementList` 哈希。你将访问到的值赋给之前使用的相同标量标识符（`$Element`、`$MeltingPt`）。然后，你可以使用 `printf()` 函数以格式化、编号的形式显示哈希内容。为了对显示的项进行编号，你在 `while` 块内包含一个递增的标识符（`$Itr`）。图 9.5 展示了生成的表格。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_238_0.png)

### 删除元素

要从哈希中删除项，Perl 为你提供了 `delete()` 函数。`delete()` 函数需要一个参数：你所操作的哈希的查找形式，并带有你要删除的键值对的键。Listing09_06 提供了一个交互式程序，你必须在 DOS 命令行中执行。你可以打开命令提示符窗口，也可以直接在 Windows 资源管理器中单击该程序。程序会提示你输入要从化学元素列表中删除的化学元素名称（Aluminum）。图 9.6 展示了与该程序的一次完整交互。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_240_0.png)

**图 9.6**  
使用 `delete()` 函数从哈希中移除键值对。

在注释 #3 处，你提示程序用户输入要从列表中删除的化学元素名称。你使用 `<STDIN>` 句柄获取用户的输入。你将输入赋值给标量标识符 `$KeyToDelete`。然后，你调用 `chomp()` 函数。你将 `$KeyToDelete` 作为参数提供。`chomp()` 函数会移除按 Enter 键时附加到输入中的换行符。

然后，你使用 `if` 控制语句检查在提示符处输入的数据是否存在于哈希中。为此，你调用 `defined()` 函数。在本例中，你在 `defined()` 函数前加上 NOT 运算符（`!`），这样只有当元素未正确输入或以其他方式不在哈希中时，选择语句才为真。你提供给 `defined()` 函数的参数是一个查找哈希操作。你将 `$KeyToDelete` 标识符提交给此操作。

与注释 #4 相关的行使用了 `delete()` 函数。该过程涉及将查找哈希操作作为参数。查找操作本身的参数是指定要删除的哈希项的键（`$KeyToDelete`）。

删除完成后，你使用 `while` 控制语句和 `each()` 函数遍历哈希并确认删除。图 9.6 显示了删除后的哈希项。

### 将哈希转换为字符串

当你想要在网页中显示数据库或互联网交互的内容时，将哈希转换为字符串通常非常有用。将哈希转换为字符串涉及将 `join()` 函数与 `sprintf()` 函数结合使用。在许多情况下，你可以不使用 `sprintf()` 函数，但如果你想要格式化从哈希中提取的项，它仍然是一个方便的辅助函数。Listing09_07 展示了一个你可能

