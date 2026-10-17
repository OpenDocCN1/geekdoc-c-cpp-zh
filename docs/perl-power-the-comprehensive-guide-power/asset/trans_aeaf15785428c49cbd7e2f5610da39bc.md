

## 第 13 章 引用

- 使用 `&` 符号对其进行解引用：

```
&$addFoods();
```

- 在括号前使用指针运算符（`->`）：

```
$addFoods->();
```

清单 13_09 探讨了三个函数引用的创建。其中一个在调用时打印蔬菜列表。另外两个修改了该函数的基本版本，以便在追加食物名称时，在它们之间添加字符。为了探索函数引用的一种用法，你将两种形式的函数赋值给一个数组，然后使用数组名和对应函数引用在数组中的位置的索引号来调用这些函数。

```
#Listing13_09
#Function references
#1 Define an array
@Vegetables = ("Green beans", "Broccoli", "Brussels sprouts");
$NL = "\n";

#2 Definition of anonymous functions before their use
$addFoods = sub{
    return join(", ", @_);
};

#3 Definition and assignment to an array
$addMoreFoods[0] = sub{
    return join(" | ", @_);
};

$addMoreFoods[1] = sub{
    return join(" * ", @_);
};

#------------------------------------------------------------
printf(" %25s", "$NL $NL $NL Use of addFoods()");

#4 Using a dereferenced anonymous function
printf("$NL %15s $NL" . &$addFoods(@Vegetables));
```

## 函数引用

```
#5 Using pointer notation
printf("$NL %15s $NL" . $addFoods->(@Vegetables));
printf(" %25s", "$NL $NL $NL Use of addMoreFoods()");

#6 Accessing function references in an array
printf("$NL %15s $NL" . $addMoreFoods[0]->(@Vegetables));
printf("$NL %15s $NL" . $addMoreFoods[1]->(@Vegetables));
```

在清单 13_09 中标记为 #1 的行中，你定义了一个数组（@Vegetables）。
在标记为 #2 的注释处，你定义了三个匿名定义函数中的第一个。函数的定义涉及 `sub` 关键字，后跟用于形成函数作用域的左花括号和右花括号。右花括号后面跟一个分号。在函数的作用域中，你只放置一条语句。该语句返回一个字符串，该字符串将提交给函数的参数连接起来，然后返回它们。要连接参数，你使用 `join()` 函数。该函数的第一个参数由指定空格的引号组成，用于分隔函数返回的字符串中的项目。对于第二个参数，你提供参数数组字符（@_）。

注释 #3 之后的两个函数定义涉及与第一个类似的语句。在第一个中，你将管道符（|）作为 `join()` 函数形成字符串的项目的分隔符。在第二个中，你将星号（*）作为分隔符。

在标记为 #4 的注释处，你使用解引用运算符（&）调用 `addFoods()` 函数。你将 @Vegetables 数组作为参数提交给该函数。如图 13.10 所示，输出由数组中包含的项目组成，显示在一行中，并用空格分隔。

在与注释 #5 相关的行中，你使用指针运算符（->）来访问该函数。当你使用指针运算符时，类型是单个美元符号。再次，你将 @Vegetables 数组作为唯一参数提交。结果如图 13.10 所示，与第一次调用相同。

在对 @addMoreFoods 数组的调用中，结果根据索引值而有所不同。在注释 #6 之后的行中，你首先访问索引 0 处的函数引用。然后你访问索引 1 处的函数引用。如图 13.10 所示，你看到之前看到的来自 @Vegetables 数组的项目，但这一次，第一行中的项目由管道符分隔，第二行中的项目由星号分隔。

## 作为数据容器的匿名数组引用

如果你使用匿名数组引用，可以创建由数组内嵌数组组成的数据结构。程序员使用匿名引用的一个原因是，此类引用使他们能够避免为数组内嵌数组命名的需要。如果你使用匿名引用，可以专注于完善少数几组花括号的工作，而不是大量不同的标识符名称。如接下来的几个程序所示，如果没有匿名引用，你最终可能会得到几十个标识符名称，这将使你在程序中管理代码几乎不可能。

匿名数组引用由方括号内的方括号组成。外层花括号构成一个“容器”，用于容纳你想要添加到其中的任意数量的数组。你可以将外层花括号内的数组视为“记录”。你可以将这些记录数组中的元素视为“字段”。图 13.11 说明了由此产生的数组排列，以及当你访问记录中的任何给定字段时涉及的两组索引括号。

# 图 13.10

你可以将函数引用存储在数组中。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_372_0.png)

# 图 13.11

外层容器数组涉及两组索引。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_372_1.png)

如图 13.11 所示，标识第一个数组中第一个元素（Cereal）的索引是数组的 0 和元素的 0（[0] [0]）。对于第二个数组中的第三个元素（1 cup），你使用数组的 1 和元素的 2（[1] [2]）。当你在引用中创建引用时，这种容器-被包含数组结构就成为可能。清单 13_10 尝试了这种结构。你将包含不同食物信息的数组存储在名为 @FoodGroupData 的数组中。每个数据项都是记录中的一个字段，你解引用数组以访问字段包含的信息。

```
#Listing13_10
#1 Create an array using anonymous references (square brackets).
# Food Group Food Serving KCalories
Grams of Fiber
$FoodGroupData =
[ #Container array
[Cereal, 'All Bran', '1 Cup', '25', '2.5'], #Arrays contained
[Cereal, 'Oatmeal', '1 Cup', '155', '4.0'],
[Vegetables, 'Green Beans', '0.5 Cup', '15', '1.0'],
[Vegetables, 'Broccoli', '0.5 Cup', '20', '3.0']
];
#2 Insert a record
$FoodGroupData->[4] = [Fruits, 'Apple', '1 Medium', '80', '3.0'];
#3 Insert items into a record and insert record in larger array
$FoodGroup = 'Fruits';
$FoodName= "Apricot";
$Serving = "3 medium";
$kCalories = "50";
$DietaryFiber = "1.8";
$insertRecord = [$FoodGroup, $FoodName,
$Serving, $kCalories, $DietaryFiber];
$FoodGroupData->[5] = $insertRecord;
#4 Obtain the number of records; dereference the
#container array
@Ref = @$FoodGroupData;
```

# # 第 13 章 引用

```
#Obtain the number of items in the container array
$Length = scalar(@Ref);
print "\n Number of Records: " . $Length . "\n";;
#Traverse both 'dimensions' of the array
for($Itr = 0; $Itr < $Length; $Itr++){
    print("\n");
    $Record = $FoodGroupData->[$Itr];
    $NumOfFields = scalar(@$Record);
    for(my $Itr = 0; $Itr < $NumOfFields ; $Itr++){
        printf(" %-12s", $Record->[$Itr]);
    }
}
```

```
#5 Retrieve a reference for a given array
$Ref = @$FoodGroupData->[0];
#Obtain the number of items (fields or columns) in the array
$Length = scalar(@$Ref);
print "\n\n Number of Columns: " . scalar(@$Ref) . "\n";
print("\n");
for($Itr = 0; $Itr < $Length ; $Itr++){
    printf(" %-12s", $FoodGroupData->[0][$Itr]);
}
```

注释 #1 相关的行涉及两层方括号。第一组方括号创建容器数组（请参阅图 13.11）。第一组方括号包含的四组方括号创建被包含的数组。每个被包含的数组提供五个字段。字段描述位于数组定义之前。注释 #2 之后的行提供了显式插入第五个匿名数组的示例。你使用索引 4 插入第五个数组，因为数组索引从零开始。

在注释 #3 引入的行中，你间接地处理字段，首先创建一系列标量标识符，并向其分配字符串常量。然后你将标识符放置在匿名数组结构中，并将其分配给另一个标量标识符。然后你将此标量标识符分配给索引 5 处的容器数组。

注释 #4 之后的赋值操作涉及解引用容器数组，并将解引用的数组分配给数组标识符（@Ref）。然后你使用 `scalar()` 函数获取容器数组包含的记录数量。你将此值分配给

