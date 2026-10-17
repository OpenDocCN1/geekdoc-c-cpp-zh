

//显示数组中出现次数最多的数字。
echo $max_i;

但是现在你已经接近本书的结尾，当然，你可以做一些更有创意的事情。不要将 `search_and_count()` 函数的每个结果分配给单独的变量 `$n1`、`$n2`、`$n3`、`$n4`、`$n5` 和 `$n6`，你可以将这些结果分配给名为 `$n` 的数组的位置 0、1、2、3、4 和 5，如下所示。

$n = array();
for ($i = 0; $i <= 5; $i++) {
$n[$i] = search_and_count($i + 1, $a);
}

接下来，当然，你可以像往常一样找到数组 `$n` 的最大值。完整的解决方案如下所示。

# file_43.1-5.php

```php
<?php
define("ELEMENTS", 100);
function dice() {
return rand(1, 6);
}
function search_and_count($x, $a) {
$count = 0;
for ($i = 0; $i <= ELEMENTS - 1; $i++) {
if ($a[$i] == $x) {
$count++;
}
}
return $count;
}
//Create array $a of random integers between 1 and 6
$a = array();
for ($i = 0; $i <= ELEMENTS - 1; $i++) {
$a[] = dice();
}
//Create array $n and
```

```php
//Display how many times each of the six numbers appears in array $a
$n = array();
for ($i = 0; $i <= 5; $i++) {
    $n[$i] = search_and_count($i + 1, $a);
    echo "Value ", $i + 1, " appears ", $n[$i], " times\n";
}

//Find maximum of array $n
$max = $n[0];
$max_i = 0;
for ($i = 1; $i <= 5; $i++) {
    if ($n[$i] > $max) {
        $max = $n[$i];
        $max_i = $i;
    }
}

//Display which number appears in the array most often.
echo "Value ", $max_i + 1, " appears in the array ", $max, " times";
?>
```

# 43.2 与子程序相关的一般性练习

# 练习 43.2-1 *验证数据输入*

*执行以下操作：*

+ i. 编写一个名为 `get_age()` 的子程序，提示用户输入其年龄并返回它。此外，该子程序应验证数据输入，并在用户输入任何非数字或非正值时显示错误消息。

+ ii. 编写一个名为 `find_max()` 的子程序，它通过其形式参数列表接受一个数组，并返回数组中最大值的索引位置。

+ iii. 使用上述引用的子程序 `get_age()` 和 `find_max()`，编写一个 PHP 脚本，提示用户将 50 人的名、姓和年龄输入到数组中，然后查找并显示年龄最大的人的姓名。

# 解决方案

由于子程序 `get_age()` 返回一个值，它可以编写为函数。子程序 `find_max()` 也是如此，因为它也返回一个值。主代码应提示用户输入名、姓和

```php
}

function my_sort(&$a, $ascending = true) {
    for ($m = 1; $m <= PEOPLE - 1; $m++) {
        for ($n = PEOPLE - 1; $n >= $m; $n--) {
            if ($ascending == true) {
                if ($a[$n] < $a[$n - 1]) {
                    my_swap($a[$n], $a[$n - 1]);
                }
            }
            else {
                if ($a[$n] > $a[$n - 1]) {
                    my_swap($a[$n], $a[$n - 1]);
                }
            }
        }
    }
}

function display_array($a) {
    for ($i = 0; $i <= PEOPLE - 1; $i++) {
        echo $a[$i], "\n";
    }
}

$names = array();
for ($i = 0; $i <= PEOPLE - 1; $i++) {
    echo "Enter a name: ";
    $names[$i] = trim(fgets(STDIN));
}

my_sort($names);                 //按升序对名称进行排序
display_array($names);           //并显示它们

my_sort($names, false);          //按降序对名称进行排序
display_array($names)            //并显示它们。
?>
```

> **注意:** 请注意，参数 `$ascending` 是一个可选参数。这意味着如果未为该参数传递任何值，则使用默认值 `true`。

```php
echo "Enter a non-negative number: ";
$kwh = trim(fgets(STDIN));
}
return $kwh;
}
function find_amount($kwh) {
if ($kwh <= 400) {
$amount = $kwh * 0.08;
} elseif ($kwh <= 2000) {
$amount = 400 * 0.08 + ($kwh - 400) * 0.22;
} elseif ($kwh <= 4000) {
$amount = 400 * 0.08 + 1100 * 0.22 + ($kwh - 1500) * 0.35;
} else {
$amount = 400 * 0.08 + 1100 * 0.22 + 1500 * 0.35 + ($kwh - 3000) * 0.50;
}
$amount += 0.26 * $amount;
return $amount;
}
do {
$kwh = get_consumption();
echo "You need to pay: $", find_amount($kwh), "\n";
echo "Would you like to repeat?\n";
$answer = trim(fgets(STDIN));
} while (strtoupper($answer) == "YES");
?>
```

# ## 43.3 复习练习

完成以下练习。

+ 1. 执行以下操作：

+ i. 编写一个名为 `factorial()` 的子程序，它通过其形式参数列表接受一个整数并返回其阶乘。

+ ii. 使用上述引用的子程序 `factorial()`，编写一个名为 `my_sin()` 的子程序，它通过其形式参数列表接受一个值，并使用泰勒级数（如下所示）返回 x 的正弦值，精度为 0.0000000001。

\(sinx=x-\frac{x^3}{3!}+\frac{x^5}{5!}-\frac{x^7}{7!}+\cdots\)

提示：请记住 x 是弧度，且 \(\frac{x^1}{1!}=x\)。

+ iii. 编写一个名为 `degrees_to_rad()` 的子程序，它通过其形式参数列表接受一个角度（度数）并返回其弧度等效值。已知 \(2\pi=360^\circ\)。

+ iv. 使用上述引用的子程序 `my_sin()` 和 `degrees_to_rad()`，编写一个 PHP 脚本，显示从 \(0^\circ\) 到 \(360^\circ\) 的所有整数的正弦值。

+ 2. 执行以下操作：

+ i. 编写一个名为 `is_leap()` 的子程序，它通过其形式参数列表接受一个年份，并根据该年份是否为闰年返回 `true` 或 `false`。

+ ii. 编写一个名为 `num_of_days()` 的子程序，它接受一个月份和一个年份，并返回该月份的天数。如果该月份是二月且年份是闰年，则子程序必须返回值 29。提示：使用上述引用的子程序 `is_leap()`。

+ iii. 编写一个名为 `check_date()` 的子程序，它接受一个日期、一个月份和一个年份，并根据该日期是否有效返回 `true` 或 `false`。

+ iv. 使用上述引用的子程序，编写一个 PHP 脚本，提示用户输入一个日期（日期、月份和年份），然后计算并显示从给定年份开始到给定日期之间经过的天数。此外，脚本应验证数据输入，并在用户输入任何非日期值时显示错误消息。

+ 3. 在一款计算机游戏中，玩家掷两个骰子。骰子点数和最大的玩家得一分。十次掷骰子后，获胜者是点数总和最大的玩家。执行以下操作：

+ i. 编写一个名为 `dice()` 的子程序，它返回 1 到 6 之间的随机整数。

+ ii. 使用上述引用的子程序 `dice()`，编写一个 PHP 脚本，提示两名玩家输入他们的姓名，然后每个玩家依次“掷”两个骰子。此过程重复十次，获胜者是点数总和最大的玩家。

+ 4. LAV 汽车租赁公司租出了 40 辆汽车，分为三类：混合动力、汽油和柴油。公司根据以下表格收取汽车费用。

| 天数 | 汽油 | 柴油 | 混合动力 |
|---|---|---|---|
| 1 – 5 | $24 每天 | $28 每天 | $30 每天 |
| 6 – 8 | $22 每天 | $25 每天 | $28 每天 |
| 9 及以上 | $18 每天 | $21 每天 | $23 每天 |

# 执行以下操作：

+ i. 编写一个名为 `get_choice()` 的子程序，它显示以下菜单。

1. 汽油
2. 柴油
3. 混合动力

然后子程序提示用户输入汽车类型（1、2 或 3）并将其返回给调用者。

+ ii. 编写一个名为 `get_days()` 的子程序，它提示用户输入租赁总天数并将其返回给调用者。

+ iii. 编写一个名为 `get_charge()` 的子程序，它接受汽车类型（1、2 或 3）和租赁总天数通过其形式参数列表，然后根据前一表格返回应付金额。联邦、州和地方税费在每张账单上增加总共 10%。

+ iv. 使用上述引用的子程序 `get_choice()`、`get_days()` 和 `get_charge()`，编写一个 PHP 脚本，提示用户输入租赁汽车的所有必要信息，然后显示以下内容：

1. 每辆汽车的应付总金额（含税）
2. 租赁的混合动力汽车总数
3. 公司在扣除税费后获得的总净利润

请注意，费率是累进的。

# 5. TAM（电视受众测量）是媒体研究中专门用于量化和定性电视受众信息的分支。

LAV 电视受众测量公司统计 10 个不同电视频道的主要新闻节目的观众人数。该公司需要一个软件应用程序来获取一些有用信息。执行以下操作：

+ i. 编写一个名为 `get_data()` 的子程序，它提示用户将频道名称和每周每天（周一至周日）主要新闻节目的观众人数输入到两个数组中。然后它将这些数组返回给调用者。

