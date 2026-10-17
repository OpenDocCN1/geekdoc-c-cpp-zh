
## 检查字符串是否为数值

`is_numeric (string)`

该函数检查*字符串*是否为数值，并相应地返回 true 或 false。数字字符串由可选的符号、任意数量的数字、可选的小数部分和可选的指数部分组成。

# 示例

```php
<?php

$a = "753";
echo is_numeric($a), "\n";      //Value 1 (true) is displayed

$a = "753.6";
echo is_numeric($a), "\n";      //Value 1 (true) is displayed

$a = "-10E-3";
echo is_numeric($a), "\n";      //Value 1 (true) is displayed

$a = "Hello";
echo is_numeric($a), "\n";      //This displays nothing (false)
?>
```

# 练习 14.4-1 — *交换姓名的顺序*

编写一个 PHP 脚本，提示用户在一个字符串中输入名字和姓氏。最后，脚本应调换这两个名字的顺序。

# 解答

本练习不同于你在第 8 章中学过的交换两个变量数值的练习。在本练习中，你必须拆分字符串，并将每个名字赋给不同的变量。如果做到了这一点，就可以按不同的顺序重新连接它们。

让我们通过一个例子来理解这个练习。下图显示了需要拆分的字符串及其每个字符的位置。

![](img/4d9a992abc5da7946ac44f9e6bf1d032_169_0.png)

在视觉上分隔名字和姓氏的字符是它们之间的空格字符。问题在于这个字符并不总是在位置 3。有些人的名字很短，比如“Tom”，而另一些人的名字较长，比如“Robert”。因此，你需要一种方法，无论字符串内容如何，都能找到空格字符的位置。

要生成随机整数，可以使用 `rand()` 函数。由于需要三位随机整数，范围必须在 100 到 999 之间。

该算法的 PHP 脚本如下所示。

```php
<?php
echo "Enter last name: ";
$last_name = trim(fgets(STDIN));

$random_int = rand(100, 999);

$login_ID = strtolower( substr($last_name, 0, 4) ) . $random_int;
echo $login_ID;
?>
```

> **注意：** 请注意，`substr()` 函数是如何嵌套在 `strtolower()` 函数中的。内层（嵌套）函数的结果被用作外层函数的参数。这是大多数程序员喜欢采用的一种编写风格，因为它有助于节省大量代码行。当然，如果嵌套了太多函数，没有人能理解你的代码。最多嵌套四层是完全可以接受的。

# 练习 14.4-3   *创建随机单词*

编写一个 PHP 脚本，创建一个由五个字母组成的随机单词。

# 解答

要创建随机单词，你需要一个包含英文字母全部 26 个字母的字符串。然后可以使用 `rand()` 函数在位置 0 到 25 之间随机选择一个字母。

该算法的 PHP 脚本如下所示。

```php
<?php
$alphabet = "abcdefghijklmnopqrstuvwxyz";

$random_word = $alphabet[rand(0, 25)] .
               $alphabet[rand(0, 25)] .
               $alphabet[rand(0, 25)] .
               $alphabet[rand(0, 25)] .
               $alphabet[rand(0, 25)];

echo $random_word;
?>
```

# 14.5 复习题：判断对错

请判断以下每个陈述是 true 还是 false。

+   1. 字符串是你可以使用键盘输入的任何内容。
+   2. 字符串必须用圆括号括起来。
+   3. 短语 "Hi there!" 包含 8 个字符。
+   4. 在短语 "Hi there!" 中，字母 "t" 位于位置 3。
+   5. 语句 $y = $a[1] 将变量 $a 所含字符串的第二个字母赋给变量 $y。
+   6. 语句 $y = $a[-1]; 是有效语句。
+   7. 修剪（trimming）是从字符串开头或末尾移除空白字符的过程。
+   8. 语句 $y = trim("Hello Aphrodite") 将值 "HelloAphrodite" 赋给变量 $y。
+   9. 语句 echo str_replace("Hi", "Hello", "Hi there! ") 显示消息 "Hello there!"。
+   10. 语句 $index = strpos("Hi there", "the") 将值 4 赋给变量 $index。
+   11. 语句 echo strtoupper("hello there!") 显示消息 "Hello There"。
+   12. 语句 echo substr("Hello there!", 0) 显示消息 "Hello there!"。
+   13. 语句 echo substr($a, 0, strlen($a)) 显示变量 $a 的部分字母。
+   14. 语句 echo substr($a, strlen($a) - 1, 1) 等价于语句 echo $a[strlen($a) - 1]。
+   15. 语句 echo strtoupper(substr("hello there!", 0, 5)) 显示单词 "HELLO"。
+   16. 语句 is_numeric("Exercise 1") 返回 true。
+   17. 语句 is_numeric("10E-2") 返回 true。

# 14.6 复习题：选择题

请为下列每个陈述选择正确答案。

+   1. 以下哪项不是字符串？
+      a. "Hello there!"
+      b. "13"
+      c. "13.5"
+      d. 以上都是字符串。
+   2. 字符串 "Hello Zeus!" 中的空格字符位于哪个位置？
+      b. 5
+      c. 空格不是字符。
+      d. 以上都不是
+   3. 语句 `echo substr($a, strlen($a) - 1, 1)` 显示
+      a. 变量 `$a` 的最后一个字符。
+      b. 变量 `$a` 的倒数第二个字符。
+      c. 该语句无效。
+   4. 语句 `ltrim(rtrim($a))` 等价于语句
+      a. `rtrim(ltrim($a))`.
+      b. `trim($a)`.
+      c. `trim(rtrim(ltrim($a)))`.
+      d. 以上都是
+   5. 语句 `str_replace($a, " ", "")`
+      a. 在变量 `$a` 的每个字母之间添加一个空格。
+      b. 从变量 `$a` 中移除所有空格字符。
+      c. 清空变量 `$a`。
+   6. 语句 `str_replace("  Hello  ", " ", "")` 等价于语句
+      a. `str_replace("  Hello  ", "", "")`.
+      b. `trim("  Hello  ")`.
+      c. `rtrim("  Hello  ")`.
+      d. 以上都是
+      e. 以上都不是
+   7. 语句 `echo strlen("")` 显示
+      a. 什么都不显示。
+      b. 1.
+      c. 0.
+      d. 该语句无效。
+      e. 以上都不是
+   8. 语句 `$Shakespeare = strpos("2b || !2b", "b")` 将哪个值赋给变量 `$Shakespeare`？
+      a. 1
+      b. 2
+      c. 6
+      d. 以上都不是

# 第 14 章
字符串操作

# 9. 下面的代码片段会做什么？

```
$a = "Hi there";
$b = substr($a, strpos($a, " ") + 1);
```

+   a. 它将单词 “Hi” 赋给变量 $b。
+   b. 它将一个空格字符赋给变量 $b。
+   c. 它将单词 “there” 赋给变量 $b。
+   d. 以上都不是

# 10. 在哪些情况下，函数 `is_numeric()` 会返回 true？

+   a. `is_numeric("1E21")`
+   b. `is_numeric("21")`
+   c. `is_numeric("1E-21")`
+   d. 以上都是

# 14.7 复习练习

完成以下练习。

+   1. 编写一个 PHP 脚本，提示用户输入其名字、中间名、姓氏以及偏好的称谓（Mr.、Mrs.、Ms.、Dr. 等），并按以下所有格式显示它们。
+   
+      *称谓 名字 中间名 姓氏*
+   
+      *名字 中间名 姓氏*
+   
+      *姓氏, 名字*
+   
+      *姓氏, 名字 中间名*
+   
+      *姓氏, 名字 中间名, 称谓*
+   
+      *名字 姓氏*

例如，假设用户输入以下内容：

名字：Aphrodite

中间名：Maria

姓氏：Boura

称谓：Ms.

脚本应按以下所有格式显示用户的名字：

+   Ms. Aphrodite Maria Boura
+   
+   Aphrodite Maria Boura
+   
+   Boura, Aphrodite
+   
+   Boura, Aphrodite Maria
+   
+   Boura, Aphrodite Maria, Ms.
+   
+   Aphrodite Boura

+   2. 编写一个 PHP 脚本，创建并显示一个由五个字母组成的随机单词。第一个字母必须是大写字母。

+   3. 编写一个 PHP 脚本，提示用户输入其姓名，然后创建一个由从姓名中随机选取的三个小写字母和一个随机四位数组成的秘密密码。例如，如果用户输入 "Vassilis Bouras"，则秘密密码可能是 "sar1359"、"vbs7281" 或 "bor1459" 之一。

