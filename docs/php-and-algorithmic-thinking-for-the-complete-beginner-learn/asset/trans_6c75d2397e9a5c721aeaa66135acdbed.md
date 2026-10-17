

```php
function get_age() {
    do {
        $x = trim(fgets(STDIN));
    } while (is_numeric($x) != true || $x <= 0);
    return $x;
}

function find_max($a) {
    $max_i = 0;
    for ($i = 1; $i <= PEOPLE - 1; $i++) {
        if ($a[$i] > $a[$max_i]) {
            $max_i = $i;
        }
    }
    return $max_i;
}

$first_names = array();
$last_names = array();
$ages = array();
for ($i = 0; $i <= PEOPLE - 1; $i++) {
    $first_names[$i] = trim(fgets(STDIN));
    $last_names[$i] = trim(fgets(STDIN));
    $ages[$i] = get_age();
}

$index_of_max = find_max($ages);

echo $first_names[$index_of_max];
echo $last_names[$index_of_max];
echo $ages[$index_of_max];
?>
```

## 3. 设计与以下 PHP 脚本对应的流程图。

```php
<?php
define("PEOPLE", 40);

function my_swap(&$x, &$y) {
    $temp = $x;
    $x = $y;
    $y = $temp;
}

function my_sort(&$a) {
    for ($m = 1; $m <= PEOPLE - 1; $m++) {
        for ($n = PEOPLE - 1; $n >= $m; $n--) {
            if ($a[$n] < $a[$n - 1]) {
                my_swap($a[$n], $a[$n-1]);
            }
        }
    }
}

function display_array($a, $ascending) {
    if ($ascending == true) {
        for ($i = 0; $i <= PEOPLE - 1; $i++) {
            echo $a[$i], "\n";
        }
    }
    else {
        for ($i = PEOPLE - 1; $i >= 0; $i--) {
            echo $a[$i], "\n";
        }
    }
}

$names = array();
for ($i = 0; $i <= PEOPLE - 1; $i++) {
    $names[$i] = trim(fgets(STDIN));
}

my_sort($names);
display_array($names, true);
display_array($names, false);
?>
```

## 4. 设计与以下 PHP 脚本对应的流程图。

```php
<?php
function get_consumption() {
    echo "Enter kWh consumed: ";
    $kwh = trim(fgets(STDIN));
    while (is_numeric($kwh) != true || $kwh < 0) {
        echo "Error! Enter kWh consumed: \n";
        $kwh = trim(fgets(STDIN));
    }
    return $kwh;
}
function find_amount($kwh) {
    if ($kwh <= 450) {
        $amount = $kwh * 0.07;
    }
    elseif ($kwh <= 2200) {
        $amount = 450 * 0.07 + ($kwh - 450) * 0.20;
    }
    else {
        $amount = 450 * 0.07 + 1750 * 0.20 + ($kwh - 1750) * 0.33;
    }
    $amount += 0.22 * $amount;
    return $amount;
}
do {
    $kwh = get_consumption();
    echo find_amount($kwh);
    echo "Repeat?\n";
    $answer = trim(fgets(STDIN));
} while (strtoupper($answer) == "YES");
?>
```

## 5. 编写与以下流程图对应的 PHP 脚本。

![](img/4d9a992abc5da7946ac44f9e6bf1d032_851_0.png)

![](img/4d9a992abc5da7946ac44f9e6bf1d032_851_1.png)

## 第 42 章 带子程序的流程图

![](img/4d9a992abc5da7946ac44f9e6bf1d032_852_0.png)

## 6. 编写与以下流程图对应的 PHP 脚本。

![](img/4d9a992abc5da7946ac44f9e6bf1d032_852_1.png)

## 带子程序的流程图

![](img/4d9a992abc5da7946ac44f9e6bf1d032_853_0.png)

## 第 43 章

### 带子程序的更多练习

### 43.1 带子程序的简单练习

### 练习 43.1-1 查找正整数的平均值

执行以下操作：

- i. 编写一个名为 `test_integer()` 的子程序，它通过形式参数列表接受一个数字，当传入的数字是整数时返回 `true`；否则必须返回 `false`。

- ii. 使用上述引用的子程序 `test_integer()`，编写一个 PHP 脚本，让用户重复输入整数值，直到输入一个实数为止。最后，脚本应显示输入的正整数的平均值。

#### 解答

由于子程序 `test_integer()` 返回一个值（`true` 或 `false`），因此可以将其编写为函数。解答如下所示。

```php
<?php
function test_integer($number) {
    $return_value = false;
    if ($number == intval($number)) {
        $return_value = true;
    }
    return $return_value;
}

$sum = 0;
$count = 0;
$x = trim(fgets(STDIN));
while(test_integer($x) == true) {
    if ($x > 0) {
        $sum += $x;
        $count++;
    }
    $x = trim(fgets(STDIN));
}

if ($count > 0) {
    echo $sum / $count;
}
?>
```

### 练习 43.1-2 查找奇数正整数的和

执行以下操作：

- i. 编写一个名为 `test_integer` 的子程序，它通过形式参数列表接受一个数字，当传入的数字是整数时返回 `true`；否则必须返回 `false`。

- ii. 编写一个名为 `test_odd` 的子程序，它通过形式参数列表接受一个数字，当传入的数字是奇数时返回 `true`；否则必须返回 `false`。

- iii. 编写一个名为 `test_positive` 的子程序，它通过形式参数列表接受一个数字，当传入的数字是正数时返回 `true`；否则必须返回 `false`。

- iv. 使用上述引用的三个子程序，编写一个 PHP 脚本，让用户重复输入数值，直到输入一个负数为止。最后，脚本应显示输入的奇数正整数的和。

#### 解答

本练习与前一个练习非常相似。每个子程序返回一个值（可以是 `true` 或 `false`），因此所有子程序都可以编写为函数。解答如下所示。

```php
<?php

function test_integer($number) {
    $return_value = false;
    if ($number == intval($number)) {
        $return_value = true;
    }
    return $return_value;
}

function test_odd($number) {
    $return_value = false;
    if ($number % 2 != 0) {
        $return_value = true;
    }
    return $return_value;
}

function test_positive($number) {
    $return_value = false;
    if ($number > 0) {
        $return_value = true;
    }
    return $return_value;
}

$sum = 0;
$x = trim(fgets(STDIN));
while(test_positive($x) == true) {
    if (test_integer($x) == true && test_odd($x) == true) {
        $sum += $x;
    }
    $x = trim(fgets(STDIN));
}
echo $sum;
?>
```

### 练习 43.1-3 查找 y 的值

编写一个 PHP 脚本，查找并显示以下公式中 y 的值（如果可能）。

![](img/4d9a992abc5da7946ac44f9e6bf1d032_857_0.png)

对于公式的每一部分，编写一个子程序，该子程序通过形式参数列表接受 x，然后计算并显示结果。当计算不可能时，应显示错误消息。

#### 解答

由于公式有两部分，必须编写两个子程序。每个子程序应计算并显示相应公式的结果，或在计算不可能时显示错误消息。由于这两个子程序不返回结果，因此可以将它们都编写为过程。解答如下所示。

```php
<?php
function formula1($x) {
    if ($x == 5) {
        echo "Error! Division by zero";
    }
    else {
        $y = 3 * $x / ($x - 5) + (7 - $x) / (2 * $x);
        echo $y;
    }
}

function formula2($x) {
    if ($x == -2) {
        echo "Error! Division by zero";
    }
    else {
        $y = (45 - $x) / ($x + 2) + 3 * $x;
        echo $y;
    }
}

echo "Enter a value for x: ";
$x = trim(fgets(STDIN));
if ($x >= 1) {
    formula1($x);
}
else {
    formula2($x);
}
?>
```

### 练习 43.1-4 掷骰子，掷骰子，掷……骰子！

执行以下操作：

- i. 编写一个名为 `dice()` 的子程序，它返回 1 到 6 之间的随机整数。

- ii. 编写一个名为 `search_and_count()` 的子程序，它通过形式参数列表接受一个整数和一个数组，并返回该整数在数组中出现的次数。

显示数组中每个数字出现的次数，以及哪个数字出现的次数最多。

#### 解答

如果不使用循环控制结构来解决此练习，它将类似于以下内容。

```php
//变量 $n1 被赋值为数组 $a 中值 1 出现的次数
$n1 = search_and_count(1, $a);
//变量 $n2 被赋值为数组 $a 中值 2 出现的次数
$n2 = search_and_count(2, $a).
.
.
//变量 $n6 被赋值为数组 $a 中值 6 出现的次数
$n6 = search_and_count(6, $a);
//显示数组 $a 中每个数字出现的次数
echo $n1, $n2, $n3, $n4, $n5, $n6;
//查找 $n1, $n2,... $n6 的最大值
$max = $n1;
$max_i = 1;
if ($n2 > $max) {
    $max = $n2;
    $max_i = 2;
}
if ($n3 > $max) {
    $max = $n3;
    $max_i = 3;
}
.
.
.
if ($n6 > $max) {
    $max = $n6;
    $max_i = 6;
}
```

