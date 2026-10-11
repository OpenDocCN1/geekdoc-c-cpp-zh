
- 12.3 设计一个算法，判断 `str` 的第一个字符是否为数字，如果是，则删除该字符。

- 12.4 设计一个算法，判断 `str` 的第一个字符是否为大写字母，如果是，则将其改为 `"0"`。

- 12.5 假设有以下声明：

  `Declare String str = "World"`

  编写一条语句在 `str` 的开头插入 `"Hello "`。语句执行后，`str` 变量应包含 `"Hello World"`。

- 12.6 假设有以下声明：

  `Declare String city = "Boston"`

  编写一条删除第一个字符。

## 复习题

### 单选题

- 1. 哪条伪代码语句显示字符串变量 `str` 的第一个字符？

  a. Display `str[1]`

  b. Display `str[0]`

  c. Display `str[first]`

  d. Display `str`

- 2. 哪条伪代码语句显示字符串变量 `str` 的最后一个字符？

  a. Display `str[-1]`

  b. Display `str[length(str)]`

  c. Display `str[last]`

  d. Display `length(str) - 1`

- 3. 如果变量 `str` 包含 `"berry"`，哪条伪代码语句将其内容改为 `"blackberry"`？

  a. Set `str[0] = "black"`

  b. Set `str = str + "black"`

  c. Insert(`str`, 0, `"black"`)

  d. Insert(`str`, 1, `"black"`)

- 4. 如果变量 `str` 包含 `"Redmond"`，哪条伪代码语句将其内容改为 `"Red"`？

  a. delete(`str`, 3, length(`str`))

  b. delete(`str`, 3, 6)

  c. Set `str = "mond"`

  d. Set `str[0] = "Red"`

- 5. 下列伪代码会导致什么结果？

  `Declare name = "Sall"`

  Set `name[4] = "y"`

  a. 发生错误。

  b. 变量 `name` 将包含字符串 `"Sally"`。

  c. 变量 `name` 将包含字符串 `"Saly"`。

  d. 变量 `name` 将包含字符串 `"Sall y"`.

# 494 第 12 章 文本处理

## 判断对错

- 1. 当使用下标指定字符串中的字符位置时，第一个字符的下标为 0。

- 2. 当使用下标指定字符串中的字符位置时，最后一个字符的下标与字符串的长度相同。

- 3. 如果 String 变量 `str` 包含字符串 `"Might"`，那么语句 `str[5] = "y"` 将将其内容更改为 `"Mighty"`。

- 4. `insert` 库模块会自动扩展字符串的大小以容纳插入的字符。

- 5. `delete` 库模块不会真正从字符串中删除字符，而是将它们替换为空格。

- 6. `isUpper` 函数将字符转换为大写，而 `isLower` 库函数将字符转换为小写。

- 7. 在空 String 变量上使用下标将发生错误。

## 简答

- 1. 使用下标表示法指定字符串中的字符位置时，第一个和最后一个字符的下标是什么？

- 2. 如果以下伪代码是一个实际程序，它会显示什么？

  `Declare String greeting = "Happy"`

  `insert(greeting, 0, "Birthday")`

  `Display greeting`

- 3. 如果以下伪代码是一个实际程序，它会显示什么？

  `Declare String str = "Yada yada yada"`

  `delete(str, 4, 9)`

  `Display str`

- 4. 如果以下伪代码是一个实际程序，它会显示什么？

  `Declare String str = "AaBbCcDd"`

  `Declare Integer index`

  For `Index = 0 To length(str) - 1`

    If `isLower(str[index])` Then

      Set `str[index] = "-"`

    End If
  `Display str`

- 5. 如果以下伪代码是一个实际程序，它会显示什么？

  `Declare String str = "AaBbCcDd"`

  `delete(str, 0, 0)`

  `delete(str, 3, 3)`

  `delete(str, 3, 3)`

  `Display str`

## 算法工作台

- 1. 设计一个算法，统计 String 变量 `str` 中出现的数字个数。

- 2. 设计一个算法，统计 String 变量 `str` 中出现的小写字母个数。

- 3. 设计一个算法，统计 String 变量 `str` 中出现的大写字母个数。

- 4. 设计一个算法，删除 String 变量 `str` 中的第一个和最后一个字符。

- 5. 设计一个算法，将 String 变量 `str` 中每个字符 `"t"` 转换为大写。

- 6. 设计一个算法，将 String 变量 `str` 中每个字符 `"x"` 替换为空格。

- 7. 假设程序中存在以下声明：

  `Declare String str = "Mr. Bean"`

  设计一个算法，将变量中的 `"Mr."` 替换为 `"Mister"`。

## 调试练习

- 1. 以下伪代码哪里有错？

  // 此程序将一个字符赋值给字符串的

  // 元素。

  `Declare String letters`

  Set `letters[0] = "A"`

  Display `"The first letter of the alphabet is ", letters`

- 2. 以下伪代码哪里有错？

  // 此程序判断用户的输入是否为单个

  // 数字。

  `Declare Integer digit`

  ```
  // 从用户处获取输入。
  Display "Enter a single digit."
  digit

  // 判断输入是否为单个数字。
  If isDigit(digit[0]) AND length(digit) == 1 Then
    Display digit, " is a single digit.
  Else
    Display digit, " is NOT a single digit.
  End If
  ```

- 3. 为什么以下伪代码的运行结果没有如注释所示？

  ```
  // 此程序统计字符串中的字符。
  Declare String word
  Declare Integer index
  Declare Integer letters = 0
  ```

  ```
  // 从用户处获取输入。
  Display "Enter a word."
  Input word
  ```

  ```
  // 统计字符串中的字符。
  For index = 0 To length(word)
    Set count = count + 1
  End For
  Display "That word contains ", count, " characters."
  ```

## 编程练习

- 1. 反转字符串

  设计一个程序，提示用户输入一个字符串，然后反向显示字符串内容。例如，如果用户输入 `"gravity"`，程序应显示 `"ytivarg"`。

- 2. 句首大写

  设计一个程序，提示用户输入包含多个句子的字符串，然后显示每个句子首字母字母大写的字符串。例如，如果用户输入 `"hello. my name is Joe. What is your name?"`（提示：程序应显示 `"Hello. My name is Joe..."` ...可以使用 `Upper` 函数将单个字符转换为大写。）

- 3. 元音与辅音

  设计一个程序，提示用户输入一个字符串。程序随后应显示字符串中元音和辅音的个数。

- 4. 字符串中数字之和

  设计一个程序，要求用户输入一个包含一系列不分离数字的字符串。程序应显示字符串中所有数字的和。例如，如果用户输入 `2514`，该方法应返回 `12`，即 `2`、`5`、`1` 和 `4` 之和。（提示：可以使用 `string` 函数。）

- 5. 出现频率最高的字符

  设计一个程序，提示用户输入一个字符串，并显示字符串中出现频率最高的字符。

- 6. 字母数字转换

  许多公司使用像 `555-GET-FOOD` 这样的数字以便客户记忆。在标准电话中，字母映射到数字的方式如下：

  | Letter | Number |
  | :--- | :--- |
  | A, B, and C | 2 |
  | D, E, and F | 3 |
  | G, H, and I | 4 |
  | J, K, and L | 5 |
  | M, N, and O | 6 |
  | P, Q, and R | 7 |
  | T, U, and V | 8 |
  | W, X, Y, and Z | 9 |

  设计一个程序，提示用户输入一个字符，并显示其原始格式对应的数字。例如，如果用户输入 `555-GET-FOOD`，程序应显示 `555-438-3663`。

- 7. 单词分隔符

  设计一个程序，接受一个每个单词首字母都大写的句子。（提示：可以使用 `toLower` 转换为小写）。

- 8. 拉丁语

  设计一个程序，读取一个句子并将每个单词转换为“拉丁语”。在拉丁语版本中，你通过移除单词的首字母并将其放在末尾来转换单词。例如：

  English: SLEPT OF NIGHT

  Pig Latin: IAY OSTMAY FOHTNA

- 9. 摩斯密码转换

  设计一个程序，提示用户输入一个字符串，然后将其转换为摩斯密码。摩斯密码是一种将字母表、数字和各种标点符号用点和横线表示的代码。表 12-4 显示了部分代码。

- 10. 文件加密

  文件加密是用加密代码编写文件的科学。在作业中，你将设计一个程序打开文件并加密其内容。假设你要加密的文件包含字符串列表。程序应打开文件并读取内容，每次读取一个字符串。将字符串中的每个字符替换为另一种字符。将加密后的字符串写入第二个文件。程序完成后，第二个文件将是第一个文件的版本，但使用了加密。

- 11. 文件解密过滤

  设计一个程序解密练习 10 中生成的文件。解密程序应读取加密文件的内容，将数据恢复到原始状态并写入另一个文件。

| Character | Code | Character | Code | Character | Code | Character | Code |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| space | space | 6 | . . . . | G | -- -- | Q | -- - |
| comma | --, -- | 7 | . -- . | H | .. | R | - . |
| period | .-- .. | 8 | --- | I | -- | S | ... |
| ? | . . . . | 9 | .... | J | . . . | T | . - |
| 0 | ---- | A | - - | K | -- - | U | -- - |
| 1 | ---- | B | .-- . | L | .-- . | V | ... |
| 2 | .. --- | C | . - . | M | -- | W | --- |
| 3 | . . -- | D | -- . | N | - | X | --, - |
| 4 | . . . - | E | . | O | --- | Y | --, -- |
| 5 | .... | F | .-- . | P | --- . | Z | --, -- |

# 递归

- 13.1 递归简介

- 13.2 使用递归解决问题

- 13.3 递归算法示例

## 13.1 递归简介

> 概念：递归模块是调用自身的模块。

你已经见过模块调用其他模块的实例。在程序中，主模块可能会调用模块 A，然后 A 可能会调用模块 B。模块也可能调用自己。调用自身的模块被称为递归模块。例如，查看程序 13-1 所示的 `message` 模块。

# 程序 13-1

```
Module main()
  Call message()
  End Module

Module message()
  Display "This is a recursive module."
  Call message()
  End Module
```

## 程序输出

```
This is a recursive module.
This is a recursive module.
This is a recursive module.
This is a recursive module.
...此输出会无限重复！
```

`message` 模块显示字符串 `"This is a recursive module."` 然后调用自己。每当调用自己时，循环就会重复。你能看出这个模块有什么问题吗？没有方法可以停止递归调用。这个模块就像一个无限循环，因为没有代码可以停止它的重复。

就像循环一样，递归模块必须有一种方式控制重复的次数。程序 13-2 中的伪代码显示了 `message` 模块的修改版本。在这个程序中，`message` 模块接收一个 `Integer`，指定模块显示消息的次数。

# 程序 13-2

```
Module main()
  // 通过向 message 模块传递参数 5，
  // 我们告诉它显示五
  // 次消息。
  Call message(5)
End Module

Module message(Integer times)
  If times > 0
    Display "This is a recursive module."
    Call message(times - 1)
  End If
End Module
```

## 程序输出

This is a recursive module.

This is a recursive module.

This is a recursive module.

This is a recursive module.

This is a recursive module.

此程序中的 `message` 模块包含一个 `If-Then` 语句（第 9 到 12 行），用于控制递归。只要 `times` 参数大于 0，就会显示消息 `"This is a recursive module."`，然后模块再次调用自己。每当它调用自己时，都会将 `times - 1` 作为参数传递。

主模块传递参数 5 调用 `message` 模块。当模块第一次被调用时，`If-Then` 语句显示消息，然后以 4 作为参数调用自己。图 13-1 说明了这一点。

# 图 13-1 模块的前两次调用

![](img/c939132f78787c7f339c6977b3fc8c85_524_0.png)

## 13.1 递归简介

图 13-1 所示的图说明了模块的两次独立调用。每当调用模块时，内存中都会创建一个 `times` 参数的新实例。第一次调用模块时，`times` 参数被设置为 5。当模块调用自己时，会创建一个 `times` 参数实例，并将值 4 传递其中。这个循环一直重复，直到最后将 0 作为参数传递给模块。如图 13-2 所示。

# 图 13-2 对 message 模块的六次调用

![](img/c939132f78787c7f339c6977b3fc8c85_525_0.png)

如图中所示，模块被调用了六次。第一次是从主模块调用的，其余五次是它调用自己。模块调用自己的次数被称为递归深度。当模块达到六次调用时，`times` 参数被设置为 0。此时，`If-Then` 语句的条件表达式为假，模块返回。程序从模块的第六次实例返回，这在图 13-3 中所示：

- 如果问题可以通过非递归解决，则模块解决它并返回

- 如果问题无法非递归解决，则模块将其还原为更小的问题并调用自己

## 13.2 使用递归解决问题

为了应用这种方法，首先要识别一个不需要递归即可解决的情况。这被称为**基准情况**（base case）。其次，确定在所有其他情况下如何使用递归解决问题。这被称为**递归情况**（recursive case）。在递归情况中，我们必须将问题还原为原始问题的较版本。通过每次递归调用缩小问题，最终到达基准情况，递归停止。

# 使用递归计算阶乘

之前的示例演示了递归模块。大多数编程语言也允许你创建递归函数。让我们从数学角度分析递归函数。在数学中，符号 $n!$ 表示 $n$ 的阶乘。非负整数的阶可以通过可以通过规则定义：

- 如果 $n=0$ 则 $n! = 1$

- 如果 $n>0$ 则 $n! = 1 \times 2 \times 3 \dots \times n$

我们将符号 $n!$ 替换为 `factorial(n)` 看起来像计算机代码，并重写这些规则：

- 如果 $n=0$ 则 `factorial(n) = 1`

- 如果 $n>0$ 则 `factorial(n) = 1 \times 2 \times 3 \dots \times n`

这些规则规定当 $n=0$ 时，其阶乘为 1。当 $n > 0$ 时，其阶乘为 1 到 $n$ 的所有正整数的积。例如，`factorial(6)` 计算为 $1 \times 2 \times 3 \times 4 \times 5 \times 6$。

在设计计算任何数字阶乘的递归算法时，我们首先识别基准情况，即不需要递归即可解决的部分。即 $n$ 等于 0 的情况：

- 如果 $n=0$ 则 `factorial(n) = 1`

这告诉我们当 $n$ 等于 0 时如何解决问题，但当 $n$ 大于 0 时该怎么办？那就是递归情况，即我们使用递归解决的部分。我们表示为：
