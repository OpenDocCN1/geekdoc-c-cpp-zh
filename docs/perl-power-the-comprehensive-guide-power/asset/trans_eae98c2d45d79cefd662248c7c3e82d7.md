

## 第 3 章 标量和字符串

```
#a "not equals" statement tested
if($CityA ne $CityC)
{
    print "\nStatement true; cities not equal.";
}
```

### 选择、lt 和 gt

你可以使用小于（lt）和大于（gt）关系运算符来创建执行排序和排序等操作的复杂程序。这里，足以演示它们适用于字符串，如 Listing03_16 所示：

```
#Listing03_16
#Testing for greater than or less than relationships
$CityA = "Chicago";
$CityC = "Miami";

#selection test to discover one value alphabetically greater than the other
if($CityC gt $CityA)
{
    print "\nMiami comes later in an alphabetical list than Chicago.";
}

#selection test for one value alphabetically less than the other
if($CityA lt $CityC)
{
    print "\nChicago is earlier in an alphabetical list than Miami.";
}
```

Listing03_16 提供两个选择语句，两者都涉及按字母顺序排列 Chicago 和 Miami，以便在使用 `lt` 和 `gt` 的选择语句中进行比较时，结果证明为真。第一个选择语句测试 Chicago 是否在字母列表中位于 Miami 之前。第二个选择语句测试 Miami 是否在字母列表中位于 Chicago 之后。在两种情况下，选择语句都会产生真值求值，因此解释器会处理花括号之间的语句。图 3.15 说明了两个选择语句的输出。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_73_0.png)

**Figure 3.15**  
大于（`gt`）和小于（`lt`）运算符建立字母顺序。

### 字符串上的递增操作

*一元递增运算符*可以用于字符串。一元运算符是只涉及一个项的运算符。它不像二元运算符那样关联两个项。相反，它直接作用于一个项。在此情况下，一元运算符是一个*递增运算符*（`++`）。Perl 字符串的递增运算符会导致字符串中最后一个字符的值每当解释器处理涉及递增运算符的语句时增加一。当字符增加一时，它将变成字母表中下一个“更大”的字母。“a”变为“b”。在 Listing03_17 中，“x”提供了一种说明递增运算符仅影响字符串最后一个字符的方法。

```
#Listing03_17
#Testing the unary operator with strings
$SmallA = "a";
$LargeA = "xA";

#create an alphabet with a unary operator

print "\n 1. ", $SmallA , "\t"  , $LargeA;
print "\n 2. " . $SmallA++ . "\t" . $LargeA++;
print "\n 3. " . $SmallA++ . "\t" . $LargeA++;
print "\n 4. " . $SmallA++ . "\t" . $LargeA++;
print "\n 5. " . $SmallA++ . "\t" . $LargeA++;
print "\n 6. " . $SmallA++ . "\t" . $LargeA++;
```

图 3.16 说明了 Listing03_17 的输出。当你首次使用运算符时，你不会看到任何变化（1），因为打印字符串的行不包含递增运算符。在第一个递增行（2）中，你看不到任何变化，因为此示例中的递增运算符仅在其出现的语句执行后才递增值。你在行 2 中看到的值实际上显示的是递增前的值。对于行 3，你看到的是前一行更改后的值。

### q() 和 qq() 函数

虽然下一章广泛讨论了可以应用于字符串的函数，但有两个函数的工作方式与双引号和单引号非常相似。这些就是 q() 和 qq() 函数。函数名称分别缩写自单引号和双引号。事实上，通常你可以将这些函数视为执行双引号和单引号的工作。不过，你使用的是函数而不是引号。

当你使用函数时，你将想要转换为字符串的内容放在函数名称后面的开括号和闭括号之间。Listing03_18 提供了两个函数基本用法的示例：

```
#Listing03_18
#q() and qq()
#set up a scalar for testing in the functions
$TestValue = "Hello";

#q() gives you a character string, so you see what you type
$CharacterQ = q($TestValue, it is good to see you.);
print "\nq(): " . $CharacterQ;

#qa() gives you an interpolated string,
#so you have some options with embedded identifiers
$CharacterQQ = qq($TestValue, it is good to see you.);
print "\nqq(): " . $CharacterQQ;
```

当你将标量值（$TestValue）插入 q() 函数时，如图 3.17 所示，你只看到标识符的名称，而不是标识符存储的值。这表明 q() 函数创建一个字符串。另一方面，当你将标量标识符与一些文本一起插入 qq() 函数时，解释器会从标识符中提取字符串。这表明 qq() 函数创建一个插值字符串。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_74_0.png)

**Figure 3.16**  
递增运算符增加应用于的字符串中最后一个字母的值。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_75_0.png)

**Figure 3.17**  
q() 和 qq() 函数创建字符串和插值字符串。

### 块

块是使用开始和结束块标签创建的程序的一部分。每个块有一个标签。标签由你选择的一个词组成。你在要指定的块的开头输入开始标签。你在要指定的块的末尾输入结束标签。添加一些语法来使其正式化后，创建块所需的就是这些。

你可以将文本块分配给标量，并以这种方式使用 Perl 来管理相当大的信息量。当你使用块时，不能在块中包含变量。如果你想将变量与块关联使用，可以存储块，然后将其与变量关联。下一节提供了此类活动的示例。

### 块和 print

如前所述，你使用块标签来指定块。标签可以由你选择的任何词组成，只要它不是关键字。要指定块的开始，你在块标签的第一次使用前加上移位运算符（`<<`）。然后跟随你想要输入的任何文本。当你完成文本输入后，再次输入标签。第二次输入标签时，必须将其紧贴文本编辑区域的右边距。Listing03_19 展示了设置块的基本方法。在此示例中，当你创建块时，也会打印它。

```
#Listing03_19
#Creating blocks
#Print the block to show its creation
print <<NOTES;
    Thank you for contacting us.
    A service representative will
    contact you within 24 hours.
NOTES
```

图 3.18 说明了 Listing03_19 中的块作为输出显示的情况。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_76_0.png)

**Figure 3.18**  
块通过打印命令显示。

### 块和变量

打印块可以是立即处理大量文本的有用方法，但块的另一种同样有益的用途涉及将它们分配给标量标识符。你可以将块分配给标量变量，然后稍后使用标识符。赋值语句用括号括起来。Listing03_20 展示了将块存储在标量变量中，然后随后打印块的基本方法。

```
#Listing03_20

#Blocks assigned to and used with variables

#Variable to be combined with block
$TestValue = "Mr. Blue";

($BlockVariable = <<NOTES);
    Thank you for contacting us.
    A service representative will
    contact you within 24 hours.
NOTES

#Concatenating a value with the block
print "\n \n" . " $TestValue,\n" . $BlockVariable;
```

图 3.19 说明了作为输出显示的块。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_76_1.png)

**Figure 3.19**  
块使打印通知变得方便。

