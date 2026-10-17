
第 3 行声明了一个名为 `length` 的变量表示最小密码长度，第 6 行声明了一个名为 `password` 的字符串变量用于存储用户的密码。第 9 到 15 行在屏幕上显示信息，告知用户密码要求。第 18 和 19 行提示用户输入密码，密码从键盘读取并赋值给 `password` 变量。

从第 22 行开始的 `If-Then-Else` 语句评估了一个复合布尔表达式。用通俗语言来说，该语句应该解释为：

如果密码长度至少为 8 位且

密码中的大写字母至少有 1 个且

密码中的小写字母至少有 1 个，且

密码中的数字至少有 1 个，那么密码有效。

否则，密码不符合要求。

接下来显示了 `numberUpperCase` 函数：

## 程序 12-5 密码验证程序（续）：numberUpperCase 函数

```
32 // The numberUpperCase function accepts a string
33 // argument and returns the number of uppercase
34 // letters it contains.
35 Function Integer numberUpperCase(String str)
36 // 用于存储大写字母数量的变量
37 Declare Integer count = 0
38
39 // 用于遍历 str 的变量
40 Declare Integer index
41
42 // 遍历 str 并统计大写
43 // 字母的数量。
44 For index = 0 To length(str) - 1
45 If isUpper(str[index]) Then
46 Set count = count + 1
47
48 End If
49 End For
50
51 // 返回大写字母的数量。
52 Return count
53 End Function
```

该函数接受一个字符串作为参数，传递给参数变量 `str`。第 37 行声明了一个名为 `count` 的整数变量，并为 0。

## 12.2 逐字符处理

该变量将用累加器，存储参数变量 `str` 中找到的大写字母数量。第 40 行声明了整数变量 `index`。`index` 变量用于第 44 行开始的循环，以检查 `str` 参数变量中的字符。第 45 行开始的 `If-Then` 语句调用 `isUpper` 函数来确定 `str[index]` 处的字符是否为大写。如果是，则在第 46 行 `count` 变量加1。循环结束后，`count` 变量将包含 `str` 参数变量中找到的大写字母数量。`count` 变量的值在第 51 行从函数返回。

接下来显示了 `numberLowerCase` 函数：

## 程序 12-5 密码验证程序（续）：numberLowerCase 函数

```
// The LowerCase function accepts a string
// argument and returns the number of lowercase
// letters it contains.
Function Integer numberLowerCase(String str)
// 用于存储小写字母数量的变量
Declare Integer count = 0

// 用于遍历 str 的变量
Declare Integer index

// 遍历 str 并统计小写
// 字母的数量。
For index = 0 To length(str)-1 Then
  Set count = count + 1
End For

// 返回小写字母的数量。
Return count
End Function
```

该函数与 `numberUpperCase` 函数几乎完全相同，但第 67 行调用 `isLower` 库函数来确定 `str[index]` 处的字符是否为小写。当函数结束时，第 73 行的语句返回 `count` 变量的值，该值包含了 `str` 变量中找到的小写字母数量。

接下来显示了 `numberDigits` 函数：

## 程序 12-5 密码验证程序（续）：numberDigits 函数

```
// The numberDigits function accepts a string
// argument and returns the number of numeric
// digits it contains.
Function Integer numberDigits(String str)
// 用于存储数字数量的变量
Declare Integer count = 0

// 用于遍历 str 的变量
Declare Integer index

// 遍历 str 并统计数字
// 的的数量。
// For index = 0 To length(str) - 1
If isDigit(str[index]) Then
    Set count = count + 1
End If
End For

// 返回数字的数量。
Return count
End Function
```

该函数与 `numberUpperCase` 和 `numberLowerCase` 函数几乎完全相同，但第 89 行调用 `isDigit` 库函数来确定 `str[index]` 处的字符是否为数字。当函数结束时，第 95 行的语句返回 `count` 变量的值，该值包含了 `str` 变量中找到的数字。

## 程序输出（输入部分加粗显示）

```
此程序判断密码是否符合以下要求：
(1) 长度至少为 8 个字符。
(2) 必须包含至少一个大写字母。
(3) 必须包含至少一个小写字母。
(4) 必须包含至少一个数字。

Enter a password.
love [Enter]
The password does not meet the requirements.
```

## 程序输出（输入部分加粗显示）

```
此程序判断密码是否符合以下要求：
(1) 长度至少为 8 个字符。
(2) 必须包含至少一个大写字母。
(3) 必须包含至少一个小写字母。
(4) 必须包含至少一个数字。

Enter a password.
loVe679g [Enter]
The password is valid.
```

### 在字符串中插入和删除字符

大多数编程语言都提供了在字符串中插入和删除字符的库函数或模块。在我们的伪代码中，我们使用表 12-3 描述的模块来实现这些目的。

| 函数 | 说明 |
| --- | --- |
| `insert(string1, position, string2)` | `string1` 是字符串，`position` 是整数，`string2` 是字符串。该函数从 `position` 开始将 `string2` 插入 `string1`。 |
| `delete(string, start, end)` | `string` 是字符串，`start` 是整数，`end` 是整数。该函数删除从 `start` 指定位置开始、到 `end` 指定位置结束的所有字符。结束位置的字符包含在删除范围内。 |

下面是如何使用 `insert` 模块的示例：

```
Declare String str = "New City"
insert(str, 4, "York")
Display str
```

第二条语句将 `"York"` 插入到 `str` 变量中，从位置 4 开始。原本在位置 4 的字符向后移动。在内存中，`str` 变量被扩展以容纳插入的字符。如果这些语句是一个完整程序并运行，我们将看到 `"New City"`。

下面是如何使用 `delete` 模块的示例：

```
Declare String str = "I ate blueberries!"
delete(str, 8, 9)
Display str
```

第二条语句删除了 `str` 中 8 到 9 的字符。原本在 10 的字符占据了留下的空间。如果这些语句是一个完整程序并运行，我们将看到 `"I ate blueberries!"`。

### 焦点：电话号码的格式化与去格式化

美国的电话号码通常格式化如下：

```
(XXX) XXX-XXXX
```

在格式中，X 代表数字。括号内的三个数字是区码。区码后的三个数字是前缀，连字符后的四个数字是用户号码。这里有一个示例：

```
(919)555-1212
```

虽然括号和连字符让人们更容易阅读，但对于计算机处理来说是不必要的。在计算机系统中，电话号码通常存储为无格式的数字序列，如下：

```
919551212
```

处理电话号码的程序通常需要对用户输入的号码进行去格式化。这意味着在将号码存储到文件或进行其他处理之前，必须移除括号和连字符。此外，某些程序需要在屏幕上显示或在纸上处理之前将号码格式化为包含括号和连字符。程序 12-6 显示的伪代码演示了去格式化电话号码的算法。主模块提示用户输入一个格式化的电话号码。然后它调用 `isValidFormat` 判断电话号码是否格式正确。如果是，则调用 `unformat` 模块移除括号和连字符。最后显示无格式的电话号码。与其在纸上展示整个程序，让我们来看主模块：

| 程序 12-6 | 电话号码去格式化程序： |
| main module |

```
Module main()
  // 声明一个存储电话号码的变量
  Declare String phoneNumber

  // 提示用户输入电话号码。
  Display "Enter a telephone number. The number you"
  Display "enter should be formatted as (XXX)XXX-XXXX."
  Input phoneNumber

  // 如果格式正确，对其进行去格式化。
  If isValidFormat(phoneNumber) Then
    unformat(phoneNumber)
    Display "The unformatted number is " , phoneNumber
  Else
```

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

如果字符串长度为 13且位置 0 处的字符是 `"("`且位置 4 处的字符是 `"-"`且位置 8 处的字符是 `"-"` 则将值设置为 True。

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

该模块通过引用接受一个字符串，并传递给参数变量 `str`。该模块假设字符串格式正确为 `(XXX)XXX-XXXX`。第 48 行删除了位置 0 处的字符，即 `"("` 字符。所有剩余字符都会自动向左移动一个位置，以填充被删除字符留下的空间。接下来，第 53 行删除了位置 3 处的字符，即 `")"` 字符。之前出现在位置 4 处的字符会自动移动以填充被删除字符留下的空间。接着，第 58 行删除了位置 6 处的字符，即连字符。之前出现在连字符右侧的字符将向左移动一个位置。在该语句执行后，`str` 中的字符串将变为未格式化，显示为一串数字。

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

第 3 行声明了一个字符串变量 `phoneNumber`，用于存储用户将输入的电话号码。第 6 行提示用户输入一个未格式化的10位电话号码，第 7 行将输入存储在 `phoneNumber` 变量中。从第 10 行开始的 If-Then 语句调用库函数 `length` 来判断用户的输入是否为10个字符。如果是，`format` 函数通过引用接受 `phoneNumber` 作为参数，并在适当的位置插入圆括号和连字符，使其以 `(XXX)XXX-XXXX` 的形式出现。格式化后的电话号码在第 12 行显示。如果用户输入的长度不是10个字符，则在第 14 行显示错误消息。

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

该模块通过引用接受一个字符串参数，并传递给参数变量 `str`。第 24 行调用 `insert` 在位置 0 处插入 `"("`。由于插入操作，所有后续字符都会向右移动一个位置以腾出空间。第 27 行在位置 4 处插入 `")"`。之前位于位置 4 处的字符会自动向右移动。接者，第 30 行在位置 8 处插入连字符 `"-"`。

程序输出（输入部分加粗显示）

输入电话号码。您的号码应该格式化为 (XXX)XXX-XXXX。

(919)555-1212 [Enter]

未格式化的号码是 9195551212

## own点 (Checkpoint)

- 12.1 假设有以下声明：

  `name = "Joy"`

  以下语句将显示什么？

  `Display name[2]`

- 12.2 假设有以下声明：

  `Declare String str = "Tiger"`

编写一条语句将第一个字符改为 `"L"`。
