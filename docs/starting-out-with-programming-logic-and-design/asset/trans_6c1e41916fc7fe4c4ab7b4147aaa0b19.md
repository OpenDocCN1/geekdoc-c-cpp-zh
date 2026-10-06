

# 494 第 12 章 文本处理

## 判断对错

- 1. 当使用下标指定字符串中的字符位置时，第一个字符的下标为 0。
- 2. 当使用下标指定字符串中的字符位置时，最后一个字符的下标与字符串的长度相同。
- 3. 如果 String 变量 `str` 包含字符串 "Might"，那么语句 `str[5] = "y"` 将将其内容更改为 "Mighty"。
- 4. `insert` 库模块会自动扩展字符串的大小以容纳插入的字符。
- 5. `delete` 库模块不会真正从字符串中删除字符，而是将它们替换为空格。
- 6. `isUpper` 函数将字符转换为大写，而 `isLower` 库函数将字符转换为小写。
- 7. 在空 String 变量上使用下标将发生错误。

## 简答

- 1. 使用下标表示法指定字符串中的字符位置时，第一个和最后一个字符的下标是什么？
- 2. 如果以下伪代码是一个实际程序，它会显示什么？
  Declare String greeting = "Happy"
  insert(greeting, 0, "Birthday")
  Display greeting
- 3. 如果以下伪代码是一个实际程序，它会显示什么？
  Declare String str = "Yada yada yada"
  delete(str, 4, 9)
  Display str
- 4. 如果以下伪代码是一个实际程序，它会显示什么？
  Declare String str = "AaBbCcDd"
  Declare Integer index
  For Index = 0 To length(str) - 1
    If isLower(str[index]) Then
      Set str[index] = "-"
    End If
  Display str
- 5. 如果以下伪代码是一个实际程序，它会显示什么？
  Declare String str = "AaBbCcDd"
  delete(str, 0, 0)
  delete(str, 3, 3)
  delete(str, 3, 3)
  Display str

## 算法工作台

- 1. 设计一个算法，统计 String 变量 `str` 中出现的数字个数。
- 2. 设计一个算法，统计 String 变量 `str` 中出现的小写字母个数。
- 3. 设计一个算法，统计 String 变量 `str` 中出现的大写字母个数。
- 4. 设计一个算法，删除 String 变量 `str` 中的第一个和最后一个字符。
- 5. 设计一个算法，将 String 变量 `str` 中每个字符 "t" 转换为大写。
- 6. 设计一个算法，将 String 变量 `str` 中每个字符 "x" 替换为空格。
- 7. 假设程序中存在以下声明：
  Declare String str = "Mr. Bean"
  设计一个算法，将变量中的 "Mr." 替换为 "Mister"。

## 调试练习

- 1. 以下伪代码哪里有错？
  // 此程序将一个字符赋值给字符串的
  // 元素。
  Declare String letters
  Set letters[0] = "A"
  Display "The first letter of the alphabet is ", letters
- 2. 以下伪代码哪里有错？
  // 此程序判断用户的输入是否为单个
  // 数字。
  Declare Integer digit

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
  设计一个程序，提示用户输入一个字符串，然后反向显示字符串内容。例如，如果用户输入 "gravity"，程序应显示 "ytivarg"。
- 2. 句首大写
  设计一个程序，提示用户输入包含多个句子的字符串，然后显示每个句子首字母字母大写的字符串。例如，如果用户输入 "hello. my name is Joe. What is your name?"（提示：程序应显示 "Hello. My name is Joe..." ...可以使用 Upper 函数将单个字符转换为大写。）
- 3. 元音与辅音
  设计一个程序，提示用户输入一个字符串。程序随后应显示字符串中元音和辅音的个数。
- 4. 字符串中数字之和
  设计一个程序，要求用户输入一个包含一系列不分离数字的字符串。程序应显示字符串中所有数字的和。例如，如果用户输入 2514，该方法应返回 12，即 2、5、1 和 4 之和。（提示：可以使用 string 函数。）
- 5. 出现频率最高的字符
  设计一个程序，提示用户输入一个字符串，并显示字符串中出现频率最高的字符。
- 6. 字母数字转换
  许多公司使用像 555-GET-FOOD 这样的数字以便客户记忆。在标准电话中，字母映射到数字的方式如下：
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
  设计一个程序，提示用户输入一个字符，并显示其原始格式对应的数字。例如，如果用户输入 555-GET-FOOD，程序应显示 555-438-3663。
- 7. 单词分隔符
  设计一个程序，接受一个每个单词首字母都大写的句子。（提示：可以使用 toLower 转换为小写）。
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

