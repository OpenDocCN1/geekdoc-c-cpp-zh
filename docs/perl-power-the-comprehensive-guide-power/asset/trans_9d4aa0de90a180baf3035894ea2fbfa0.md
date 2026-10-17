

## Figure 8.1 哈希是关联容器。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_200_0.png)

哈希构成关联容器，因为它不一定按照索引序列的逻辑来存储其包含的元素。相反，你根据元素内容建立的顺序来访问哈希中的元素。内容建立的顺序创造了一种情况：元素之间的关联，而非序列，表征了表征容器的逻辑。

哈希中的元素可以说是根据哈希键组织的。当你将键放入哈希时，如图 8.1 所示，你会看到一个可识别的单词。然而，当你将这个单词插入哈希时，哈希会对其进行转换（或哈希处理），使其本质上可以作为一种加密索引。这个索引可以放置在容器中的任意位置。容器背后编程中嵌入的算法决定这个位置。给定算法的有效设计，当你在哈希中搜索给定键时，哈希检索项目的速度比使用顺序搜索（通常用于数组的方法）要快。

每个键都作为值的哈希索引。Perl 哈希提供唯一键。当哈希提供唯一键时，如果发现你插入的键哈希中已包含，它会用新键替换旧键。在图 8.2 中，当你使用键 `Alkali` 插入第二个和第三个元素时，第三个键取代了前两个，之后检查哈希内容时，你只能找到第三个条目，在此示例中，它与 Potassium 相关联。两个 Metalloids 键也表征了同样的置换形式。最终，你只能找到与 Silicon 相关联的键。

| Category | Element |
|---|---|
| Noble Gasses | Helium |
| Alkali Metals | Lithium |
| Alkali Metals | Sodium |
| Alkali Metals | Potassium |
| Transition Metals | Titanium |
| Metalloids | Boron |
| Metalloids | Silicon |

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_201_0.png)

| Category | Element |
|---|---|
| Noble Gasses | Helium |
| Alkali Metals | Potassium |
| Transition Metals | Titanium |
| Metalloids | Silicon |

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_201_1.png)

然而，键所适用的情况不适用于值。如图 8.3 所示，只要你插入唯一键，哈希就存储多个相同的值。

| Key | Value |
|---|---|
| Helium | Noble Gasses |
| Lithium | Alkali Metals |
| Sodium | Alkali Metals |
| Potassium | Alkali Metals |
| Titanium | Transition Metals |
| Boron | Metalloids |
| Silicon | Metalloids |

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_201_2.png)

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_201_3.png)

哈希替换重复键的顺序是可预测的。最近输入的重复键会取代旧键。至于哈希中值的组织，情况取决于哈希背后的算法。当你显示哈希中的项目时，很难预测显示顺序。考虑图 8.3 中显示的元素。这可能是你从哈希中打印元素时看到的顺序。元素顺序不是字母顺序。也不是你向哈希添加值的顺序。

# 识别和初始化哈希

哈希有两种使用上下文。一种是隐式上下文。另一种是标量上下文。当哈希出现在隐式哈希上下文中时，你使用百分号（%）来标识它。

# 第 8 章 哈希

当你在标量上下文中使用哈希时，你使用美元符号（$）来标识它。Listing08_01 向你展示了在隐式和标量上下文中初始化的哈希。该程序不产生任何输出。

```
#Listing08_01

#1 Implicit initialization using the
# correspondence operator (=>)
#Parentheses
%Elements = (Hydrogen => H,
             Helium => He,
             Manganese => Mn);

#Implicit initialization using a list
%Elements = ("Oxygen" , "O",
             "Nitrogen" , "N",
             "Potassium" , "K");

#2 Scalar initialization using
#Curly braces
        # correspondence operator (=>)
$Elements{Carbon}=C;
$Elements{Calcium}=C;
$Elements{Aluminum}=Al;
```

在注释 #1 中，你首先使用通信运算符初始化一个哈希。要进行此类初始化，你在哈希标识符前加上百分号（%Elements）。这指定了一个隐式哈希。然后，你使用列表操作（括起来的键和值）来指定要分配给哈希的键值对。如果不使用括号，初始化仍然有效，但仅适用于第一个元素（Hydrogen）。使用列表的第二种隐式初始化形式涉及使用逗号而不是通信运算符。这种方法与第一种一样有效。

与注释 #2 相关的行允许你继续使用标量或查找形式的初始化来初始化 %Elements 哈希。在此情况下，你在哈希标识符前加上美元符号（$Elements），并使用花括号（{ }）来括起来要指定的键。然后，你跟随一个赋值运算符和要与键关联的值。

# 初始化顺序

当你使用隐式和查找形式初始化哈希时，你先遵循隐式形式，再遵循查找形式。考虑以下初始化顺序：

```
#1 Lookup following implicit form works
%Elements = (Hydrogen =>  H);  #implicit
$Elements{Aluminum} = Al;       #lookup
```

当查找跟随隐式形式时，如果你使用格式打印 @Elements 的内容，你会看到以下输出：

```
Aluminum Al
Hydrogen H
```

Perl 解释器允许你隐式初始化哈希，然后使用标量或查找语句向哈希添加更多元素。你在 Hydrogen 之后添加 Aluminum，当你打印内容时，你会看到这两个元素。

当你反转顺序时，情况会发生变化。如果你先使用查找形式的初始化，然后再使用隐式形式的初始化，Perl 解释器不会向哈希添加元素。相反，它允许隐式初始化取消先前分配的内容。考虑以下行中的初始化：

```
#2 Implicit following lookup does not work
$Elements{"Calcium"}=       "Ca";       #lookup
$Elements{Aluminum}=        "Al";       #lookup
%Elements = ("Oxygen", "O");           #implicit – cancels previous
```

当你在两个标量表达式之后跟随隐式初始化时，如果你使用格式打印 @Elements 的内容，你只能看到一个元素：

```
Oxygen O
```

使用隐式初始化，你会丢失先前定义的哈希内容。

> 当你考虑在隐式（%）和（标量）显式（$）形式之间来回切换的方式时，Perl 的行为可能看起来是任意的。反驳这一观念的一种方法是记住，当你使用显式（$）形式时，你正在处理哈希中的一个单个标量项目。当你使用隐式形式（%）时，你正在将项目视为整个哈希结构的一部分。这就像你拨动了一个开关。

# 初始化的变体

当你为哈希使用隐式初始化形式或标量（查找）初始化形式时，你可以用多种方式表示你正在处理的数据。Listing08_02 提供了几种数据表示的示例，这些方法有些随机。该程序不产生任何输出。

```
#Listing08_02

#1 Implicit initialization -- variations

# Scalar
$TableElement = "Hydrogen";

# A scalar and interpolated and literal strings
%Elements = ($TableElement => "H",
             "Helium" => 'He',
             'Manganese' => "Mn");

#2 Initialization using the scalar
$Elements{"Carbon"} = "C";
$Elements{"Calcium"} = "Ca";
$Elements{Aluminum} = "Al";

#3 Keys and values consisting of more than one word
#requires quotes
$CompoundName = "Carbon Monoxide";
%Compounds = ($CompoundName       => "CO",
              q(Plumbous Oxide)   => 'PbO',
              qq(Copper Hydroxide) => "CuOH");
$Compounds{"Calcium Oxide"}      =     "CaO";
```

在 Listing08_02 的注释 #1 中，你首先将插值字符串分配给标量（$TableElement）。然后，在随后的隐式初始化形式中，你将标量插入列表中指定第一个元素键的位置。对于第一个元素的值，你在通信运算符（=>）之后跟随一个包含单个字符 H 的插值字符串，它指定了元素周期表中 Hydrogen 的缩写。

在插入 Hydrogen 元素后，当你初始化紧随其后的元素时，你首先使用插值字符串（"Helium"）作为键和一个字符串


