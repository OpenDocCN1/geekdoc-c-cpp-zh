

# 关键术语

- assign function（赋值函数）—用于在字符串中按指定次数复制某个字符

- Concatenation operator（连接运算符）—用于连接（串联）字符串；在 C++ 中的 `+` 符号

- Consuming the character（消耗字符）—丢弃该字符的另一种术语

- erase function（删除函数）—用于从字符串中移除（擦除）字符

- find function（查找函数）—返回一个整数，表示字符串在字符串变量中的起始位置

- getline function（读取行函数）—从键盘读取输入的字符，直到遇到分隔符字符为止，该分隔符会被消耗（忽略）

- ignore function（忽略函数）—告诉计算机先读取后消耗（丢弃）一个或多个字符

- insert function（插入函数）—用于在字符串中插入字符

- length function（长度函数）—返回字符串变量中包含的字符数

- replace function（替换函数）—用于替换字符串中的字符

- String concatenation（字符串连接）—将字符串连接（或链接）在一起的过程；通过连接运算符实现

- substr function（子字符串函数）—返回你想要从字符串变量中访问的字符

# 复习题

1. 下列哪个语句显示了名为 `address` 的字符串变量中包含的字符数？
    a. `cout << address.length() << endl;`
    b. `cout << numChars(address) << endl;`
    c. `cout << length(address) << endl;`
    d. `cout << size.address << endl;`

2. 下列哪个语句应该提示程序获取任何城市的名称并将其存储名为 `cityName` 的字符串变量中？
    a. `cin >> cityName;`
    b. `cin(cityName);`
    c. `getline(cityName, cin);`
    d. `getline(cin, cityName);`

3. 如果 `amount` 变量包含字符串 "$56.55"，下列哪个语句将移除变量内容中的美元符号？
    a. `amount.erase("$");`
    b. `amount.erase(0, 1);`
    c. `amount = amount.substr(1);`
    d. 都 b 和 c

4. 如果 `state` 变量包含字符串 "MI "（字母 MI 后面跟着三个空格），下列哪个语句将移除变量内容中的三个空格？
    a. `state.erase(" ");`
    b. `state.erase(3, " ");`
    c. `state.remove(2, 3);`
    d. 以上均不是

5. 字符串变量中包含的字符的下标是 ________。
    a. 0（零）
    b. 1（一）

6. 下列哪个子句决定了存储在 `part` 变量中的字符串是否以字母 A 开头？
    a. `if (part.begins("A"))`
    b. `if (part.begswith("A"))`
    c. `if (part.substr(0, 1) == "A")`
    d. `if (part.substr(1) == "A")`

7. 下列哪个子句决定了存储在 `part` 变量中的字符串是否以字母 B 结尾？
    a. `if (part.ends("B"))`
    b. `if (part.endswith("B"))`
    c. `if (part.substr(part.length() - 1, 1) == "B")`
    d. 以上均不是

8. 下列哪个语句将 `part` 变量中的前三个字符赋值给 `code` 变量？
    a. `code = part.assign(0, 3);`
    b. `code = part.substr(0, 3);`
    c. `code = part.substr(1, 3);`
    d. `code = part.substring(0, 3);`

# 第 13 章 字符串

9. 如果 `word` 变量包含字符串 "Bells"，下列哪个语句将变量的内容更改为 "Bell"？
    a. `word.erase(word.length() - 1, 1);`
    b. `word.replace(word.length() - 1, 1, "");`
    c. `word = word.substr(0, word.length() - 1);`
    d. 以上所有

10. 下列哪个语句将 `word` 变量的内容从 "men" 更改为 "mean"，
    a. `word.addTo(2, "a");`
    b. `word.insert(2, "a");`
    c. `word.insert(3, "a");`
    d. 以上均不是

11. 如果 `msg` 变量包含字符串 "Happy holidays"，语句 `cout << msg.find("day", 0);` 将在屏幕上显示什么？
    a. -1
    b. 0
    c. 10
    d. 11

12. 如果 `msg` 变量包含字符串 "Happy holidays"，语句 `location = msg.find("Day", 0);` 将什么值赋值给 `location` 变量？
    a. -1
    b. 0
    c. 10
    d. 11

13. 下列哪个将 `amount` 变量中逗号的位置赋值给名为 `loc` 的 `int` 变量？
    a. `loc = amount.contains(",");`
    b. `loc = amount.substr(",");`
    c. `loc = amount.find(",", 0);`
    d. 以上均不是

14. 下列哪个语句在名为 `state` 的字符串变量中搜索字符串 "CA"，并将结果赋值给名为 `result` 的 `int` 变量？搜索应从 `state` 变量中下标为 5 的字符开始。`state` 变量的内容是大大写的。
    a. `result = find(state, 5, "CA");`
    b. `result = state.find(5, "CA");`
    c. `result = state.find("CA", 5);`
    d. `result = state.find("CA", 5);`

15. 如果 `state` 变量包含字符串 "San Francisco,"，语句 `state.find("CA", 5)` 将返回什么？
    a. -1
    b. 0
    c. 10
    d. 11

16. 下列哪个语句从 `state` 变量中下标为 5 的字符搜索 "CA"？
    a. `result = find(state, 5, "CA");`
    b. `result = state.find(5, "CA");`
    c. `result = state.find("CA", 5);`
    d. `result = state.find("CA", 5);` (注：此处原文逻辑似乎重复，已按字面翻译)

15. 如果 `state` 变量包含字符串 "San Francisco,"，语句 `state.find("CA", 5)` 将返回什么？
    a. -1
    b. 0
    c. 10
    d. 11

16. 下列哪个语句在 `state` 变量中替换下标为 5 的字符为 "CA"？
    a. `state.replace(5, 2, "CA");`
    b. `state.replace(5, "CA");`
    c. `state.replace(5, 2, "CA");`
    d. `state.replace(5, 2, "CA");`

17. 下列哪个语句将 `divider` 变量赋值五个星号 `*****`？
    a. `divider.assign(5, "*");`
    b. `divider.assign("*****");`
    c. `divider.assign(5, "*");`
    d. `divider.assign(5, "*");`

18. 下列哪个语句将 `city` 变量的内容、逗号以及 `state` 变量的内容连接起来，并将结果赋值给 `cityState` 变量？
    a. `cityState = city + "," + state;`
    b. `cityState = city + "," + state;`
    c. `cityState = city + "," + state;`
    d. 以上均不是

# 第 13 章 字符串

19. 下列哪个语句将 `word` 变量中的第五个字符赋值给 `letter` 变量？
    a. `letter = word.substr(4, 1);`
    b. `letter = word[4];`
    c. `letter = word.substr(4);`
    d. 以上 a 和 b

20. 下列哪个语句告诉计算机忽略后续 100 个字符？
    a. `cin.ignore(100);`
    b. `cin.ignore('100');`
    c. `cin.ignore(100);`
    d. 以上均不是

21. 处理时，________ 可以消耗换行符。
    a. `>>` 运算符
    b. `<<` 运算符
    c. `getline` 函数
    d. a 和 c

# 练习题

![](img/d4a28a6f49d11bf2f31740ad594.png)

# 纸笔练习

1. 写一个 C++ 语句，将 `message` 变量中包含的字符数赋值给名为 `numChars` 的 `int` 变量。答案在章节末尾。

2. 写一个 C++ 语句使用 `erase` 函数从 `message` 中移除两个字符。答案在章节末尾。

3. 使用 `replace` 函数重写纸笔练习 2。

4. 写一个 C++ 语句将 `code` 变量的首字符替换为 "B"。

5. 写一个 C++ 语句将名为 `address` 的字符串变量中的前四个字符赋值给字符串变量 `num`。

6. `part` 变量包含字符串 "ABCD34G"。写一个 C++ 语句将 `part` 变量中的 34 赋值给字符串变量 `code`。

7. 写一个 C++ 语句将 `word` 变量的内容从 "mend" 更改为 "amend"。

8. 写一个 C++ 语句将 `word` 变量的内容从 "mouse" 更改为 "mouth"。

9. `amount` 变量包含 "3,123,560"。编写 C++ 代码移除变量内容中的逗号。

