

# 第13章 字符串

# 如何使用 replace 函数

语法
string.replace(substring, count, replacementString);

示例 1
string phone = "1-800-111-0000";
phone.replace(2, 3, "877");
将 phone 变量中从下标为 2 的字符开始的三个字符替换为 "877"；将 phone 变量的内容更改为 "1-877-111-0000"

示例 2
string item = "ABC34";
item.replace(3, 1, "D");
将 item 变量中从下标为 3 的字符开始的一个字符替换为 "D"；将 item 变量的内容更改为
"ABCD34"

示例 3
string name = "Karen Wilson";
name.replace(7, 6, "Farley");
将 name 变量中从下标为 7 的字符开始的六个字符替换为 "Farley"；将变量的内容更改为 "Karen Farley"

```
示例 4
int subscript = 0;
string salary = "";
cout << "Salary:";
getline(cin, salary);
while (subscript < salary.length()) {
    if (salary.substr(subscript, 1) == " ")
        salary.replace(subscript, 1, "");
    else
        subscript += 1;
    //end if
} // while
```

将变量中的任何逗号和空格替换为空字符串

图 13-28 如何使用 replace 函数

图 13-29 显示了如何在年收入程序中使用 replace 函数代替 erase 函数。对其原始代码进行的修改（之前在图 13-26 中显示）在图 13-29 中用阴影标记。

# 社会安全号程序

```cpp
//移除任何逗号或空格
while (subscript < income.length()) {
    if (income.substr(subscript, 1) == ",") {
        // income.substr(subscript, 1) == ")"
        income.replace(subscript, 1, "");
    } else {
        subscript += 1;
        // 你可以使用 subscript
        subscript++;
    }
}
```

图 13-29 显示使用 replace 函数的部分年收入程序

# 微型测验 13-3

- 1. 下列哪项用于在名为 cityState 的字符串变量中搜索逗号，并将结果赋值给名为 location 的 int 变量
  a. location = cityState.find("

> 微型测验题的答案位于附录 A。

# 社会安全号程序

图 13-30 显示了社会安全号程序的描述和 IPO 图（输入-处理-输出图表）。该程序应允许用户输入不带连字符的社会安全号。如果用户输入包含九个字符，程序应在社会安全号适当的位置插入连字符并将结果显示在屏幕上。如果用户没有输入九个字符，程序应显示适当的消息。你将在下一节学习如何在字符串变量内部插入字符。

# 第13章 字符串

# 问题规范

创建一个程序，允许用户输入不带两个连字符的社会安全号。用户的输入应包含九个字符。如果用户没有输入所需的字符数，程序应显示消息“The number must contain 9 characters”（数字必须包含9个字符）。否则，程序应插入两个连字符并将结果显示在屏幕上。

| 输入 | 处理 | 输出 |
| --- | --- | --- |
| SSN（不带连字符） | 处理项目：无 | SSN（带连字符） |

算法。

- 1. 输入 SSN
- 2. 如果 (SSN 包含9个字符)
  在 SSN 的第四个字符处插入连字符
  在 SSN 的第七个字符处插入连字符
  显示 SSN
  否则
  显示消息 "The number must contain 9 characters" 

图 13-30 社会安全问题的问题规范和 IPO 图

# 在字符串变量内部插入字符

除了删除和替换字符串变量中的字符外，你还可以在字符串变量内部插入字符。例如，你可以在员工的名字和姓氏之间插入中间首字母。或者，你可以在电话号码的区号周围插入括号。你还可以在社会安全号中插入连字符。在字符串变量内部插入字符的字符串 insert 函数语法如图 13-31 所示。在语法中，字符串变量名和下标指定了你在字符串的哪个位置进行插入。要在字符串开头插入，使用数字 0 作为下标。要从字符串的第二个字符开始插入，使用数字 1 作为下标，依此类推。图 13-31 还显示了使用 insert 函数的示例：name.insert(7, "G ") 告诉计算机在 name 变量中插入—G.（字母 G、句点和一个空格）。字母 G 被插入。句点和空格被插入在下标 8 和 9 处，使它们成为变量中的第九和第十个字符。执行该语句后，name 变量包含字符串 "Karen Guthers"。在示例 2 中，phone.insert(0, "(") 将 phone 变量的内容从 "312 050-1111" 更改为 "(312)050-1111"。

