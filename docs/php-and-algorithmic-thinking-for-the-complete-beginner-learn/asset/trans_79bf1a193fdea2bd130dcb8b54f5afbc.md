

## 第31章 循环控制结构更多练习

-   对于 N = 1, M = 2，判定值等于 |1/2 − 0.333| = 0.1670
-   对于 N = 1, M = 3，判定值等于 |1/3 − 0.333| = 0.0003
-   对于 N = 1, M = 4，判定值等于 |1/4 − 0.333| = 0.0830
-   ...
-   对于 N = 100, M = 99，判定值等于 |100/99 − 0.333| = 0.6771
-   对于 N = 100, M = 100，判定值等于 |100/100 − 0.333| = 0.6670

如你所见，0.0003 是所有可能结果中的最小值。因此，N = 1 和 M = 3 的组合（对应分数 1/3）被认为是 0.333 的最佳近似。

以下是 PHP 脚本：

```php
<?php
do {
    echo "Enter a real number between 0 and 100: ";
    $x = trim(fgets(STDIN));
} while (is_numeric($x) != true || $x < 0 || $x > 100);

$best_n = 1;
$best_m = 1;
for ($n = 0; $n <= 100; $n++) {
    for ($m = 1; $m <= 100; $m++) {
        if (abs($n / $m - $x) < abs($best_n / $best_m - $x)) {
            $best_n = $n;
            $best_m = $m;
        }
    }
}

echo "The corresponding fraction is: ", $best_n, "/", $best_m;
?>
```

### 31.5 使用循环控制结构查找最小值和最大值

在第23章中，你学习了如何使用单分支决策结构在四个值中查找最小值和最大值。现在，下面的代码片段做了几乎相同的事情，但只使用一个变量 `$w` 来保存用户输入的所有值。

```php
$w = trim(fgets(STDIN));             //User enters 1st value
$max = $w;

$w = trim(fgets(STDIN));             //User enters 2nd value
if ($w > $max) {
    $max = $w;
}

$w = trim(fgets(STDIN));             //User enters 3rd value
if ($w > $max) {
    $max = $w;
}

$w = trim(fgets(STDIN));             //User enters 4th value
if ($w > $max) {
    $max = $w;
}
```

除了第一对语句外，其他所有语句块都是相同的；因此，只需将其中的一个块放入循环控制结构中并执行三次即可，如下所示。

```php
$w = trim(fgets(STDIN));             //User enters 1st value
$max = $w;

for ($i = 1; $i <= 3; $i++) {
    $w = trim(fgets(STDIN));         //User enters 2nd, 3rd and 4th value
    if ($w > $max) {
        $max = $w;
    }
}
```

当然，如果你想允许用户输入更多值，只需增加计数循环结构的`final_value`即可。

相应地，如果你想要一个能查找并显示10个人中最重者的脚本，解决方案如下。

```php
<?php
echo "Enter a weight: ";
$w = trim(fgets(STDIN));
$max = $w;

for ($i = 1; $i <= 9; $i++) {
    echo "Enter a weight: ";
    $w = trim(fgets(STDIN));
    if ($w > $max) {
        $max = $w;
    }
}
echo $max;
?>
```

> **注意：** 请注意，计数循环结构的迭代次数比给定的总数值个数少一次。

尽管这个 PHP 脚本运行得很好，但让我们做点不同的事情。与其提示用户在循环前输入一个值、在循环内输入九个值，不如让用户在循环内输入所有值。

这里出现的问题是：无论如何，在循环开始迭代之前，必须为变量 `$max` 赋一个初始值。你实际上可以赋一个“几乎任意”的初始值，但应该谨慎选择该值，因为错误的初始值可能导致不正确的结果。

在本练习中，所有给定值都与人的体重有关。由于不可能找到任何体重为负数的人（至少在地球上不存在），你可以安全地将变量 `$max` 的初始值设为 -1，如下所示。

```php
<?php
$max = -1;
for ($i = 1; $i <= 10; $i++) {
    echo "Enter a weight: ";
    $w = trim(fgets(STDIN));
    if ($w > $max) {
        $max = $w;
    }
}
echo $max;
?>
```

一旦执行流程进入循环，用户输入第一个值，决策控制结构验证为真。变量 `$max` 中的值 -1 被第一个给定值覆盖，之后执行流程正常进行。

#### 练习 31.5-1 验证并查找最小值和最大值

编写一个 PHP 脚本，提示用户输入10个人的体重，然后找出最重和最轻的人。此外，脚本应验证数据输入，并在用户输入任何非数字、负数、零值或大于1500的值时显示错误消息。

#### 解决方案

借助上一个练习作为指导，你现在应该可以闭着眼睛完成这个练习了！

要验证数据输入，你只需替换上一个练习中的以下两行代码：

```php
echo "Enter a weight: ";
$w = trim(fgets(STDIN));
```

替换为以下代码片段：

```php
echo "Enter a weight: ";
$w = trim(fgets(STDIN));
while (is_numeric($w) != true || $w < 1 || $w > 1500) {
    echo "Invalid value! Please enter a weight between 1 and 1500! \n";
    $w = trim(fgets(STDIN));
}
```

最终脚本如下。

**file_31.5-1.php**

```php
<?php
$max = -1;
$min = 1500;
for ($i = 1; $i <= 10; $i++) {
    echo "Enter a weight: ";
    $w = trim(fgets(STDIN));
    while (is_numeric($w) != true || $w < 1 || $w > 1500) {
        echo "Invalid value! Please enter a weight between 1 and 1500! \n";
        $w = trim(fgets(STDIN));
    }
    if ($w > $max) {
        $max = $w;
    }
    if ($w < $min) {
        $min = $w;
    }
}
echo $min, $max;
?>
```

**注意：** 请注意，这种方法并非在所有情况下都适用。如果某个练习需要提示用户输入任意数字（不仅仅是正数），则不能应用此方法，因为用户可能只输入负值。如果发生这种情况，初始值 -1 永远不会被任何给定值覆盖。只有当你知道给定值的下限时，才能使用此方法查找最大值；或者只有当你知道给定值的上限时，才能使用此方法查找最小值。例如，如果练习需要找到最轻的人，你可以将变量 `$min` 的初始值设为 +1500，因为地球上没有人会那么重！顺便提一下，Jon Brower Minnoch 是美国人，在他的巅峰体重时期，他是人类有记录以来最重的人，体重约为1,400磅！！！！

#### 练习 31.5-2 验证并查找最高温度

编写一个 PHP 脚本，提示用户反复输入行星的名称和平均温度，直到输入单词“STOP”（作为名称）为止。最后，脚本应显示最热行星的名称。此外，由于 -459.67°（华氏度）是可能的最低温度（称为绝对零度），脚本应验证数据输入，并在用户输入非数字值或低于绝对零度的值时显示错误消息。

#### 解决方案

首先，让我们编写不使用数据验证的 PHP 脚本。根据“终极”规则，前测循环结构的一般形式应如下：

```php
echo "Enter the name of a planet: ";
$name = trim(fgets(STDIN));    //Initialization of $name
while (strtoupper($name) != "STOP") {
    A statement or block of statements

    echo "Enter the name of a planet: ";
    $name = trim(fgets(STDIN));    //Update/alteration of $name
}
```

现在，让我们添加其余语句，仍然不进行数据输入验证。请记住，由于值 -459.67° 是温度标度的下限，你可以使用低于此值的值作为变量 `$max` 的初始值。

```php
<?php
$max = -460;
$m_name = "";
echo "Enter the name of a planet: ";
$name = trim(fgets(STDIN));
while (strtoupper($name) != "STOP") {
    echo "Enter its average temperature: ";
    $t = trim(fgets(STDIN));
    if ($t > $max) {
        $max = $t;
        $m_name = $name;
    }
    echo "Enter the name of a planet: ";
    $name = trim(fgets(STDIN));
}
if ($m_name != "") {
    echo "The hottest planet is: ", $m_name;
} else {
    echo "Nothing Entered!";
}
?>
```

> **注意：** `if ($m_name != "")` 语句是必需的，因为用户有可能从一开始就输入单词“STOP”。

要验证数据输入，你只需替换以下两行代码：

```php
echo "Enter its average temperature: ";
$t = trim(fgets(STDIN));
```

替换为以下代码片段：

```php
echo "Enter its average temperature: ";
$t = trim(fgets(STDIN));
while (is_numeric($t) != true || $t < -459.67) {
    echo "Invalid value!\n";
    echo "Enter an average temperature greater than -459.67 degrees!\n";
    $t = trim(fgets(STDIN));
}
```

