

## 12.2 逐字符文本处理 489

```
15 Display "该号码格式不正确。"
16 End If
18 End Module
```

第 3 行声明了一个字符串变量 `phoneNumber`，用于存储用户将输入的电话号码。第 6 到第 8 行提示用户输入一个格式正确的电话号码，从键盘读取并将其存储在 `phoneNumber` 变量中。
从第 11 行开始的 If-Then-Else 语句将 `phoneNumber` 作为参数传递给 `isValid` 函数。如果参数格式正确，该函数返回 True，否则返回 False。如果函数返回 True，第 12 行将 `phoneNumber` 作为参数传递给 `unformat` 函数。`unformat` 函数通过引用接收其参数，并删除圆括号。随后，第 13 行显示未格式化的电话号码。
如果用户输入的号码格式不正确，`isValid` 函数在第 11 行返回 False，并执行第 15 行的 `Display` 语句。

`isValid` 函数如接下来所示：

| 程序 12-6 | 电话号码去格式化程序（续）： |
| --- | --- |
| | isValid 函数 |

```
19 // isValid 函数接受一个字符串参数
20 // 并按照以下方式确定其是否符合
21 // 美国电话号码的格式：
22 // ((XXX)XXX-XXX
23 // 如果参数格式正确，该函数
24 // 返回 True，否则返回 False。
25 Function Boolean isValid(str)
26 // 用于指示格式是否有效的局部变量
27 Declare Boolean valid
28
29 // 判断 str 格式是否正确
30 If length(str) == 13 AND str[0] == "("
31 str[4] == "-" AND str[8] == "-" Then
32 Set valid = True
33 Else
34 Set valid = False
35 End If
36
37 // 返回 valid 的值。
38 Return valid
39 End Function
```

该函数接受一个字符串作为参数，并传递给参数变量 `str`。第 27 行声明了一个名为 `valid` 的局部布尔变量，它将用作标志，指示 `str` 中的字符串是否符合美国电话号码的格式。

从第 30 行开始的 If-Else 语句评估一个复合布尔表达式。用通俗语言来说，该语句解释如下：

如果字符串长度为 13且位置 0 处的字符是 "("且位置 4 处的字符是 "-"且位置 8 处的字符是 "-" 则将值设置为 True。

否则

将值设置为 False。

在 If-Then-Else 语句执行后，变量 `valid` 将被设置为 True 或 False，指示 `str` 格式是否正确。第 38 行的语句返回 `valid` 变量的值。

格式模型如接下来所示：

## 程序 12-6 电话编号程序（续）：格式模型

```
41 // format 模块通过引用接受一个字符串，
42 // 假设包含如下格式的电话号码：
43 // (XXX) XXX-XXXX。
44 // 模块通过删除圆括号
45 // 和连字符对字符串进行格式化。
46 Module format(String ref str)
47 // 首先，删除位置 0 处的左括号
48 delete(str, 0, 0)
50 // 接下来，删除右括号。由于之前的
51 // 删除，它现在位于
52 // 位置 3。
53 delete(str, 3, 3)
55 // 接下来，删除连字符。由于之前的
56 // 删除，它现在位于
57 // 位置 6。
58 delete(str, 6, 6)
59 End Module
```

该模块通过引用接受一个字符串，并传递给参数变量 `str`。该模块假设字符串格式正确为 (XXX)XXX-XXXX。第 48 行删除了位置 0 处的字符，即 "(" 字符。所有剩余字符都会自动向左移动一个位置，以填充被删除字符留下的空间。接下来，第 53 行删除了位置 3 处的字符，即 ")" 字符。之前出现在位置 4 处的字符会自动移动以填充被删除字符留下的空间。接着，第 58 行删除了位置 6 处的字符，即连字符。之前出现在连字符右侧的字符将向左移动一个位置。在该语句执行后，`str` 中的字符串将变为未格式化，显示为一串数字。

## 程序输出（输入部分加粗显示）

输入电话号码。您的号码应该格式化为 (XXX)XXX-XXXX。
(919)555-1212 [Enter]
未格式化的号码是 9195551212

现在让我们来看一个算法，它获取一个未格式化的电话号码（一系列10位数字），并通过在正确的位置插入圆括号和连字符对其进行格式化。主模块所示：

## 12-7 电话号码格式化程序：主模块

```
Module main()
  // 声明一个存储电话号码的变量。
  // 声明 String phoneNumber
  // 提示用户输入电话号码。
  Display "输入一个未格式化的10位电话号码。"
  Input phoneNumber
  // 如果输入长度为10个字符，则进行格式化：
  If length(phoneNumber) == 10 Then
    format(phoneNumber)
    Display "格式化后的号码是 ", phoneNumber
Else
    Display "该号码不是10位数字。"
  End If
End Module
```

第 3 行声明了一个字符串变量 `phoneNumber`，用于存储用户将输入的电话号码。第 6 行提示用户输入一个未格式化的10位电话号码，第 7 行将输入存储在 `phoneNumber` 变量中。从第 10 行开始的 If-Then 语句调用库函数 `length` 来判断用户的输入是否为10个字符。如果是，`format` 函数通过引用接受 `phoneNumber` 作为参数，并在适当的位置插入圆括号和连字符，使其以 (XXX)XXX-XXXX 的形式出现。格式化后的电话号码在第 12 行显示。如果用户输入的长度不是10个字符，则在第 14 行显示错误消息。

`format` 模块如接下来所示：

## 12-7 电话号码格式化程序（续）：format模块

```
// format 模块通过引用接受一个字符串，
// 假设包含一个未格式化的10位电话
// 号码。模块按以下方式对字符串格式化
```

## 第12章 文本处理

```
21 // 方式：(XXX)XXX-XXXX。
22 Module format(String Ref str)
23 // 首先，在位置 0 处插入左括号
24
25 insert(str, 0, "(")
26
27 // 接下来，在位置 4 处插入右括号
28 insert(str, 4, ")")
29
30 // 接下来，在位置 8 处插入连字符
31 insert(str, 8, "-")
32 End Module
```

该模块通过引用接受一个字符串参数，并传递给参数变量 `str`。第 24 行调用 `insert` 在位置 0 处插入 "("。由于插入操作，所有后续字符都会向右移动一个位置以腾出空间。第 27 行在位置 4 处插入 ")"。之前位于位置 4 处的字符会自动向右移动。接者，第 30 行在位置 8 处插入连字符 "-"。

程序输出（输入部分加粗显示）
输入电话号码。您的号码应该格式化为 (XXX)XXX-XXXX。
(919)555-1212 [Enter]
未格式化的号码是 9195551212

##  own点 (Checkpoint)

- 12.1 假设有以下声明：
  name = "Joy"
  以下语句将显示什么？
  Display name[2]

- 12.2 假设有以下声明：
  Declare String str = "Tiger"
编写一条语句将第一个字符改为 "L"。

- 12.3 设计一个算法，判断 `str` 的第一个字符是否为数字，如果是，则删除该字符。

- 12.4 设计一个算法，判断 `str` 的第一个字符是否为大写字母，如果是，则将其改为 "0"。

- 12.5 假设有以下声明：
  Declare String str = "World"
编写一条语句在 `str` 的开头插入 "Hello "。语句执行后，`str` 变量应包含 "Hello World"。

- 12.6 假设有以下声明：
  Declare String city = "Boston"
编写一条删除第一个字符。

## 复习题

### 单选题

- 1. 哪条伪代码语句显示字符串变量 `str` 的第一个字符？
  a. Display str[1]
  b. Display str[0]
  c. Display str[first]
  d. Display str

- 2. 哪条伪代码语句显示字符串变量 `str` 的最后一个字符？
  a. Display str[-1]
  b. Display str[length(str)]
  c. Display str[last]
  d. Display length(str) - 1

- 3. 如果变量 `str` 包含 "berry"，哪条伪代码语句将其内容改为 "blackberry"？
  a. Set str[0] = "black"
  b. Set str = str + "black"
  c. Insert(str, 0, "black")
  d. Insert(str, 1, "black")

- 4. 如果变量 `str` 包含 "Redmond"，哪条伪代码语句将其内容改为 "Red"？
  a. delete(str, 3, length(str))
  b. delete(str, 3, 6)
  c. Set str = "mond"
  d. Set str[0] = "Red"

- 5. 下列伪代码会导致什么结果？
  Declare name = "Sall"
  Set name[4] = "y"
  a. 发生错误。
  b. 变量 name 将包含字符串 "Sally"。
  c. 变量 name 将包含字符串 "Saly"。
  d. 变量 name 将包含字符串 "Sall y".

