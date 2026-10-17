

DeepEx

不支持低于1366*768分辨率的设备访问。
当前基于web登录的设备相关功能将保留至2024年12月31日。

DeepEx

大数据智能分析平台

快速开始

首页

登录

用户名:

用户名

密码:

密码

记住登录

登录

任何忘记/未保存的更改将丢失。请勿在登录前手动关闭浏览器或刷新浏览器。

Copyright© 2020-2023 中国电子科技集团公司第二十八研究所 版权所有

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_217_0.png)

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_218_0.png)

**Figure 8.8**
`reverse()` 函数应用于哈希时，会反转哈希中项目的键值指定关系。

# 使用 `shift()` 函数

`shift()` 函数适用于数组。你可以像使用 `pop()` 函数来访问与查找函数共同使用的数组键，以便检索用于显示的值一样使用它。`pop()` 和 `shift()` 函数之间的唯一区别在于，`pop()` 函数从数组末尾提取项目，而 `shift()` 函数从数组开头提取元素。如前所述，关于 `pop()` 函数，鉴于 `shift()` 函数实际上会从数组中删除项目，你可以通过使用它来提升程序的性能。Listing08_08 说明了 `shift()` 函数的用法。

```perl
#Listing08_08

# 1 Formatting elements for the table
$NL = "\n ";
$DC = "=";                 #character for top and bottom lines of table
$TW = 45;                   #Table width
$DL = sprintf( "%45s", $NL . $DC x $TW); #top and bottom lines
$TableTitleText = ' Melting Points of Elements';
$COLAHEAD = "Element";
$COLBHEAD = "Celsius";

#2 Set up the data using an implicit hash
%ElementsMeltingPts = ( Aluminum, 659, Carbon, 3600,
                       Chromium, 1615, Copper, 1083,
                       Gold, 1946, Hydrogen, -259,
```

to a scalar, $ElementName. Given the default order of element names the sort() function creates, the first element out is Aluminum.

To print the element name and the corresponding melting point, you submit two values to the print() function. The first is $ElementName; the second is the returned temperature you retrieve when you use the hash lookup operation using, again, $ElementName. Figure 8.9 illustrates the output of Listing08_08.

**Figure 8.9**
`shift()` 函数可与查找操作配合使用，以访问哈希中的元素。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_220_0.png)

# 使用 each() 检索键和值

在所有专门用于哈希的函数中，当你希望从数组中检索键和值时，each() 函数被证明是最有用的。each() 函数将数组的隐式形式（%）作为其参数。每次调用时，它返回一个键值对。Listing08_09 说明了使用 each() 函数创建一个表格，以显示著名化学家的姓名及其成就。

#Listing08_09
# 1 Formatting elements for the table
$NL = "\n ";
$DC = "="; #character for top and bottom lines of table
$TW = 55; #Table width
$DL = sprintf( "%45s", $NL . $DC x $TW); #top and bottom lines
$TableTitleText = 'Leading Chemists of History';
$COLAHEAD = "Chemist";
$COLBHEAD = "Achievement";
$TableTitle = sprintf("%45s", $DC x int(( $TW - length($TableTitleText))/2) .
$TableTitleText .
$DC x int(( $TW - length($TableTitleText))/2));

```
# 2 Define the keys and values for a table
%Chemists = ("Trevisan", "Ancient alchemist",
            "Paracelsus", "Physician who cured diseases",
            "Priestley", "Discovered oxygen",
            "Lavoisier", "Father of modern chemistry",
            "Dalton", "Invented the atomic theory",
            "Woehler", "Father of organic chemistry",
            "Mendeleev", "Created the first table of elements",
            "Curies", "Isolated radium",
            "Thomson", "Discovered the electron"
           );

#3 Print the table
printf("$DL");
printf("%s", $NL . $TableTitle);
printf("$DL");
printf("\n %-15s %-20s", $COLAHEAD, $COLBHEAD);
printf("$DL");

# 4 Use each to retrieve key - value pairs
    while(($Name, $Achievement) = each(%Chemists)){
        printf("\n %-15s %-20s", $Name , $Achievement);
    }
```

注释 #1 的行标识了可用于格式化表格的元素。要创建 $TableTitle 标识符所包含的字符串，你需要构建一个由三部分组成的字符串。第一部分和第三部分是填充内容。第二部分是你想要用作标题的字符串。要创建填充部分，你需要用表格的宽度减去用于表格标题的字符串的长度。然后将余数除以二，以便在标题的两侧进行填充。然后使用 sprintf() 将各部分连接起来，并将其赋值给 $TableTitle。

紧跟在注释 #2 之后的行定义了一个哈希 %Chemists，其中包含标识著名化学家的键以及命名其最伟大成就的值。在注释 #3 处，你打印表格标题。为此，你打印已分配给 $TableTitle 的标题行，随后跟上列标题。

在注释 #4 处，你使用 while 控制语句遍历哈希。要访问哈希中的键值对，你使用 each() 函数。你将 each() 函数的返回值赋给一个包含两个标量的列表，$Name 和 $Achievement。请注意，你使用逗号分隔这些标量。你将 each() 函数的返回值赋给

这个列表。对于 each() 函数本身，将数组名称括在括号中是可选的，但使用括号可以使操作顺序更清晰。当 each() 函数遍历完所有键值对后，它会到达一个未定义的元素，从而终止 while 控制语句的操作。

在访问键值对时，你将它们传递给 printf() 函数。printf() 函数的格式化功能允许你设置宽度为 15 和 20 个字符的列。Figure 8.10 说明了 Listing08_09 的输出。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_222_0.png)

# ## 结论

本章探讨了哈希作为关联容器的基础知识。关联容器采用一种算法，该算法不涉及以严格顺序的方式存储数据，例如，当你检查数组的索引时，你会看到这一点。容器中的一个项目不一定按照你放置它们的顺序依次出现。相反，该算法的构建旨在根据数据自身的特征来组织数据。这些特征在算法中保持隐藏，但算法使你能够快速访问哈希存储的信息。

初始化哈希时，你可以同时使用哈希的标量形式和隐式形式。结果在很大程度上取决于你所处的上下文。尽管如此，基础知识保持不变。你可以通过哈希中的商业“at”符号（@）来识别哈希的隐式形式。标量形式，即查找形式的哈希，与美元符号相关联。

访问哈希中的项目时，你有多种选择。两种简单的方法涉及使用 keys() 或 values() 函数来访问给定哈希中的键或值，并将它们分配给一个数组。然后，你可以使用 while 或 foreach 等重复控制语句来遍历数组。与哈希的查找形式配合使用，遍历键或值的数组可以让你轻松访问哈希中的所有元素。

# 结论

本章还探讨了在处理数组时熟悉的函数在处理哈希时也能证明有用。其中包括 `shift()`、`pop()` 和 `reverse()` 函数。当你将哈希作为参数使用 `reverse()` 函数时，你会反转哈希中项目的键值关系。本质上，你是倒序读取列表，但就哈希而言，这意味着你也在倒序读取键值对。反转键值对允许你以多种方式轻松组织数据，例如，当你按照熔点建立的顺序显示化学元素时。

