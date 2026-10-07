

## 第 12 章：使用字符函数

这里是一个合并两个数据集的程序：

### 程序 12.2：将值转换为大写

```sas
data Mixed;
  set Learn.Mixed;
  Name = upcase(Name);
run;

data Both;
  merge Mixed.Learn;
  by Name;
run;
```

正如你所预期的，UPCASE 函数将所有字母转换为大写。

有两个函数，LOWCASE 和 PROPCASE，它们分别将字母转换为小写和格式大小写（proper case）。**格式大小写**会将每个“单词”的首字母大为大写字母，并将其余字母转换为小写。我们所说的“单词”是指任何被分隔符隔的序列。默认分隔符是空格、正斜杠、连字符、括号和制表符。如果你需要，可以将分隔符作为 PROPCASE 函数的可选第二个参数来指定分隔符。程序 12.3 展示了 PROPCASE 函数以及下一节中描述的 COMPBL 函数的使用。

## 12.4 从字符串中删除字符

这一类别的函数包括 COMPBL 和 COMPRESS。前者将两个或多个空格转换为单个空格；后者从字符值中删除空格（默认操作）或你指定的字符。

我们在一个程序中演示了 COMPBL 函数（不要尝试读出 COMPBL；你可能会伤到自己——只需压缩空格即可），以帮助标准化某些地址。在下面的列表中，注意有几行包含多个空格，且大小写不一致。

### 图 12.2：数据集地址列表

| Name | Street | City | State | Zip |
|---|---|---|---|---|
| ron coDY | 1178 HIGH 480 | camp verde | tx | 78010 |
| jason Tran | 123 lake view drive | East Rockaway | ny | 11518 |

注意：这是一个等宽列表，以便你可以看到多个空格。

以下是一个程序，将多个空格转换为单个空格；将 Name 和 City 的大小写转换为格式大小写；并将州缩写转换为大写：

### 程序 12.3：将多个空格转换为单个空格并演示 PROPCASE 函数

```sas
data Standard;
  set Learn.Address;
  Name = compbl(propcase(Name));
  Street = compbl(propcase(Street));
  City = compbl(propcase(City));
  State = upcase(State);
run;
```

在此处你可以将一个函数嵌套在另一个函数内部。COMPBL 函数的参数是 PROPCASE 函数返回的值（在本例中，顺序并不重要）。下面的列表显示了结果：

### 图 12.3：数据集标准列表

| Name | Street | City | State | Zip |
|---|---|---|---|---|
| Ron Cody | 1178 Highway 480 | Camp Verde | TX | 78010 |
| Jason Tran | 123 Lake View Drive | East Rockaway | NY | 11518 |

## 12.5 拼接两个或多个字符串

将字符串组合在一起被称为连接（concatenation）。例如，如果你有代表名和姓的独立变量，你可以将它们连接起来（中间留一个空格）以创建一个包含全名的变量。

连接运算符 `||`（或 `|||`）对 SAS 程序员一直可用。例如，如果 One = ABC 且 Two = DEF，那么 One 等于 ABCDEF。

当你使用 `||` 运算符时，如果你没有预定义结果字符串的长度，则该字符串的长度是你正在连接的各个字符串长度之和。

三个实用的函数 CAT、CATS 和 CATX 让这个过程变得简单得多。CAT 函数接受两个或多个参数并将它们连接。它与使用 `||` 运算符几乎相同，区别在于结果字符串的长度默认为参数长度之和。CATS 函数会删除前导和尾的空格（记住 S 代表 strip）。CATX 函数与 CAT 函数类似，但你将分隔符作为第一个参数提供。当你使用此函数连接字符串时，前导和尾的空格会被删除，并且分隔符值被放在每个字符串之间。

### 程序 12.4：演示连接函数

```sas
title "Concatenation Functions";
data _;
  length Name4 $15;
  First = 'Ron';
  Last = 'Cody';
  Join = ':' || First;
  Name1 = First || Last;
  Name2 = cat(First,Last);
  Name3 = catx(',',First,Last);
  put Join=/nName1=/nName2=/nName3=/nName4=;
run;
```

第一个输出，然后是解释：

### 图 12.4：程序 12.4 的输出

![](img/9e15d853955818e4c3b0ae55b096.png)

再次，使用了等宽输出以便你可以看到多个空格。变量 Join 是通过将分隔符连接到变量的前后部创建的。注意 Ron 和 Cody 之间有三个空格。CAT 函数给出的结果与 `||` 运算符相同。CATS 函数在连接字符串之前删除了前导和尾部的空格。最后，Name4 在名和姓之间有一个单个空格，因为输入了一个空格作为分隔符值。

## 12.6 删除前导或尾部空格

三个函数 TRIMN（记住 N 代表 null 空）、LEFT 和 STRIP 允许你从字符值中删除尾部空格、前导空格或两者都有。我们将通过示例程序来演示这些函数：

### 程序 12.5：演示 TRIMN、LEFT 和 STRIP 函数

```sas
data Blanks;
  String = ' ABC ';
  JoinLeft = ':' || left(String);
  JoinTrim = ':' || trimn(String);
  JoinStrip = ':' || strip(String);
run;
```

以下是输出：

### 列表 12.5：数据集 Blanks 的输出

| String | JoinLeft | JoinTrim | JoinStrip |
|---|---|---|---|
| ABC | :ABC | :ABC | :ABC |

变量 String 具有三个前导空格和两个尾部空格。判断一个值是否具有前导或尾部空格的一个好方法是在字符值的开头和结尾连接一个字符（例如，冒号）。注意：在输出中很难看出尾部空格——只有有经验的 SAS 程序员才能做到这一点！在三个 Join 变量中，JoinLeft 后面跟着五个空格，JoinTrim 后面跟着三个空格，而 JoinStrip 没有尾部空格。当你将这些函数中任何一个的结果赋值给变量时，该变量的长度不会改变。因此，如果你在以下示例中创建了三个变量，那么 Left、Trim、Strip 这三个变量的存储长度都等于 8（String 的长度）：

```sas
Left = left(String);
Trim = trimn(String);
Strip = strip(String);
```

## 12.7 使用 COMPRESS 函数从字符串中删除字符

这是一个有趣且相当常见的问题：你有一个包含电话号码的 SAS 数据集（或原始文件）。这些号码来自各种来源并以各种格式存在，如下：

### 图 12.6：数据集 Learn 的列表

| Phone |
|---|
| (908)232-4856 |
| 210.343-4757 |
| (516) 343-9293 |
| 93423425 |

你想在这些电话号码中仅保留数字，并从每个值中保留连字符。为了这一点，你需要删除空格、左括号、右括号、点和连字符。COMPRESS 函数允许你选择想要从字符值删除删除字符。以下是完成此任务的一种方法：

### 程序 12.6：使用 COMPRESS 函数从字符串中删除字符

```sas
data Phone;
  length PhoneNumber $10;
  set Learn.Phone;
  PhoneNumber = compress(Phone, ' -.');
```

COMPRESS 函数的第一个参数是你想要从中删除字符的字符值。如果你省略第二个参数，COMPRESS 将删除字符串中的所有空格。数据集 Phone 的列表所示：

### 图 12.7：数据集 Phone 的列表

| PhoneNumber | Phone |
|---|---|
| 9082324856 | (908)232-4856 |
| 2103434757 | 210.343-4757 |
| 5163439293 | (516) 343-9293 |
| 93423425 | 93423425 |

注意字符变量 PhoneNumber 仅包含数字。

