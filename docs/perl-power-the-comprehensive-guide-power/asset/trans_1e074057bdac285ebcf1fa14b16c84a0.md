

## 第 9 章 扩展哈希应用

```perl
#4 Assign the elements to an array
@NElementNames = keys(%NewlandsElements);
#5 Use an inner foreach loop and a selection statement
#to retrieve the names of elements
	$Itr = 1;
	foreach $NEName (@NElementNames) {
		if(!defined($MendeleevElements{$NEName})) {
			printf("\n %-15s %-15s %-15s",
				$NEName,
				$NewlandsElements{$NEName},
				"Newlands");
		}
	}
system("pause");
```

要格式化输出表，在注释 #1 中，你定义了几个与格式相关的标识符。在注释 #2 中，你设置了两个哈希。第一个哈希包含门捷列夫使用的数据。第二个哈希包含纽兰兹使用的数据。在注释 #3 中，你打印输出表的标题。

在与注释 #4 相关的行中，你将包含纽兰兹使用的数据的哈希的键赋值给一个数组，`@NElementNames`。有了这个数组后，你接着在注释 #5 之后的行中使用 `foreach` 控制语句来遍历 `@NElementNames` 数组中的项目。当你访问元素名称时，你将它们暂时赋值给 `$NEName` 标识符。

将元素名称赋值给 `$NEName` 标识符后，你可以在哈希查找操作中使用该标识符，并使用 `defined()` 函数的否定形式（`!defined()`）来对其进行求值。此操作的目的是测试包含门捷列夫使用的数据的哈希（`%MendeleevElements`）中未定义的键。

你测试纽兰兹使用的每个元素。每次找到一个不存在于门捷列夫数据中的元素时，你就打印它。除了元素名称外，你还打印与其关联的状态。在每种情况下，状态都是“D”。你还打印“Newlands”以确认该数据仅由纽兰兹使用。图 9.2 显示了 Listing09_02 的输出。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_231_0.png)

**Figure 9.2**  
使用 `defined()` 函数来确定两个哈希中的元素是否相同。

### 确定键值对的数量

要确定哈希中键值对的数量，可以使用涉及 `keys()` 函数和 `scalar()` 函数的方法。该过程首先是将哈希中的键赋值给一个数组。然后，你使用 `scalar()` 函数来提取数组中的元素数量。Listing09_03 提供了一个涉及纽兰兹和门捷列夫使用的数据的示例。有关程序的背景讨论，请参阅标题为“Checking for Existence”的部分。

```perl
#Listing09_03

# 1 Formatting elements for the table
$NL = "\n ";
$DC = "=";              #character for top and bottom lines of table
$TW = 55;                #Table width
$DL = sprintf( "%55s", $NL . $DC x $TW); #top and bottom lines
$COLAHEAD = "Mendeleev";
$COLBHEAD = "Newlands";

#2 Set up the data using an implicit hash
%MendeleevElements = (H, D, Li, D, Be, D, B, D, C, D, N, D, O, D,
                      F, D, Na, D, Mg, D, Al, D, Si, D, P, D, S, D,
                      Cl, D, K, D, Ca, D, Ti, D, V, D, Cr, D, Mn, D,
                      Fe, D, Co, D, Ni, D, Cu, D, As, D,
                      Se, D, Br, D, Ru, D, Rh, D, Pd, D, Ag, D, Cd, D,
                      In, D, Sn, D, Sb, D, Te, D, I, D, Cs, D, Ba, D);

%NewlandsElements = (H, D, Li, D, B, D, C, D, N, D, O, D, F, D, Na, D,
Mg, D, Al, D, Si, D, P, D, S, D, Cl, D, K, D,
Ca, D, Cr, D, Ti, D, Mn, D, Fe, D, Co, D, Ni, D,
Cu, D, Zn, D, Y, D, In, D, As, D, Se, D, Br, D,
Rb, D, Sr, D, La, D, Ce, D, Zr, D, Nb, D, Mo, D, Ru, D,
Rh, D, Pd, D, Ag, D, Cd, D, U, D, Sn, D, Sb, D,
Te, D, I, D, Cs, D, Ba, D, V, D);

#3 use keys to extract the unique keys
$MLenK = scalar(keys(%MendeleevElements));
$MLenV = scalar(values(%MendeleevElements));
$NLenK = scalar(keys(%NewlandsElements));
$NLenV = scalar(values(%NewlandsElements));

#Display the result
printf("$DL");
printf("\n %-30s %-30s" , $COLAHEAD , $COLBHEAD);
printf("$DL");
printf("\n %-15s %-15s%-15s %-15s", "Keys" , "Values",
"Keys", "Values");
printf("$DL");
printf("\n %-15s %-15s%-15s %-15s", $MLenK, $MLenV ,
$NLenK, $NLenV);
system("pause");
```

本程序对数据和数据的呈现采用了与前两个程序相同的方法。在注释 #1 标识的行中，你设置了呈现表的格式化元素。在注释 #2 中，你创建了两个哈希。一个哈希 `%MendeleevElements` 保存门捷列夫使用的数据的键和值。第二个哈希 `%NewlandsElements` 保存纽兰兹使用的数据的键和值。“D”表示“已定义”。

在注释 #3 中，你使用 `scalar()` 函数来确定每个哈希中键和值的数量。`keys()` 函数的唯一参数是你想要访问其键的哈希。`keys()` 函数的返回值是包含所有键的数组。当你将 `keys()` 函数级联到 `scalar()` 函数时，结果是一个表示键数量的值。

使用 `values()` 函数的过程类似。`values()` 函数访问哈希中的所有值，如果你将 `values()` 函数级联到 `scalar()` 函数，你将得到哈希中所有值的计数。

对于表示门捷列夫和纽兰兹使用的数据的两个哈希，你使用 `scalar()` 函数以及级联的 `keys()` 和 `values()` 函数来定义四个标量标识符（`$MLenV`、`$MLenK`、`$NLenK`、`$NLenV`）。获得这些值后，你可以继续打印它们。图 9.3 显示了 Listing09_03 产生的表。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_233_0.png)

**Figure 9.3**  
使用 `scalar()` 函数来检索元素的数量。

### 哈希切片

当你使用切片操作时，可以将一个或多个其他哈希的内容插入到一个哈希中。你可以即兴发挥出无数种哈希切片方法。该过程通常涉及使用目标哈希的查找形式。随后是涉及要切片到目标哈希的项目列表的赋值操作。在其他情况下，你可以避免使用查找操作，而是使用单独的列表赋值。Listing09_04 展示了三种可能性：

- 使用由逗号分隔的一系列键的哈希查找操作。将值列表赋值给这些键。请参见注释 #4。
- 使用哈希查找操作。作为查找的参数，使用 `keys()` 和你想要从中派生切片键的哈希。随后是赋值运算符和包含 `values()` 函数的列表。作为 `values()` 函数的参数，你使用与 `keys()` 函数中相同的哈希。请参见注释 #5。
- 使用赋值运算符将哈希列表赋值给目标哈希。作为列表中的第一个项目，命名目标列表。请参见注释 #6。

```perl
#Listing09_04
# 1 Formatting elements for the table
$NL = "\n ";
$DC = "=";            #character for top and bottom lines of table

%Elements = (%Elements,
    %InertGases,
    %AlkaliMetals,
    %RareEarthElements);

# 7 Print the table
printf("$DL");
printf("\n %-17s %3s", $COLAHEAD , $COLBHEAD);
printf("$DL");
foreach $ElementName (keys(%Elements))
{
    printf("\n %-17s %3.0f", $ElementName,
        $Elements{$ElementName});
}
```

在与注释 #1 相关的行中，你设置了一些用于显示切片数据的表格的格式化元素。在注释 #2 中，你创建了一个基本哈希 `%RareEarthElements`。该哈希包含六种稀土元素的名称及其对应的原子序数。在注释 #3 中，你创建了第二个哈希 `%AlkaliMetals`，它提供六种碱金属及其原子序数。这两个哈希暂时保留在后台。

在与注释 #4 相关的行中，你使用切片技术定义了第三个哈希。这种切片技术表面上采用哈希的查找形式。你在哈希名称前加上隐式哈希标识符（`@`）。（通常，你在查找操作中使用美元符号。）在花括号内，你提供要切片到哈希中的键列表。然后，你赋值一个你想要作为值切片到哈希中的项目列表。键列表对应值列表。

在注释 #4.1 之后的行中，你向程序添加了另一个哈希定义（`%Gasses`）。该定义包括四种元素及其对应的摄氏熔点。

注释 #5 标识第二种切片形式。在这种情况下，你使用 `keys()` 和 `values()` 函数将 `%Gasses` 哈希的键和值切片到 `%Elements` 哈希中。`keys()` 函数访问 `%Elements` 哈希中的所有元素。你在查找操作的花括号内调用 `keys()` 函数。

对于相应的值，你使用赋值运算符将 `values()` 函数返回的项目赋值给列表括号内。作为 `values()` 函数的参数，你再次使用 `%Gasses` 哈希。该操作基本上与你有一组逗号分隔的项目相同。

