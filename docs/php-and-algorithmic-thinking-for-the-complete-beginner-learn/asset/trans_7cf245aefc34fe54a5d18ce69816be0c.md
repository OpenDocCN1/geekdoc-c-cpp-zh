

## 后测试循环结构

```php
if (Boolean_Expression) {
    do {
        A statement or block of statements
    } while (Boolean_Expression);
}
```

## 练习 29.10-1 转换 PHP 脚本

使用后测试循环结构重写以下 PHP 脚本。

```php
<?php
$a = trim(fgets(STDIN));
$b = trim(fgets(STDIN));

while ($b <= $a) {
    $a *= 2;
    $b = $b * 3;
}

echo $a, $b;
?>
```

## 解答

根据转换规则，使用后测试循环结构的 PHP 脚本变为

```php
<?php
$a = trim(fgets(STDIN));
$b = trim(fgets(STDIN));

if ($b <= $a) {
    do {
        $a *= 2;
        $b = $b * 3;
    } while ($b <= $a);
}

echo $a, $b;
?>
```

```php
$x = $x * 2;
$y = $y + 1;
}
echo $x;
?>
```

## 解答

根据转换规则，使用后测试循环结构的 PHP 脚本变为

```php
<?php
$x = 0;
$y = 1;
if ($y < 10) {
    do {
        $x = $x * 2;
        $y = $y + 1;
    } while ($y < 10);
}
echo $x;
?>
```

如你所见，变量 $y 不依赖于用户输入（它被赋予常量值 1）。这意味着，每当执行此脚本时，布尔表达式 ($y < 10) 肯定评估为真，因此执行流程进入循环。因此，在这种情况下，你实际上可以省略决策控制结构。保留它并没有错，但毫无疑问是多余的。

```php
<?php
$y = 1;
$x = 0;
do {
    $x = $x * 2;
    $y = $y + 1;
} while ($y < 10);
echo $x;
?>
```

# 29.11 从计数循环结构转换为后测试循环结构

此转换没有自己的规则，但你可以使用已经学过的规则，即，你可以从计数循环结构转换为中间前测试循环结构，最后转换为后测试循环结构，如下图所示。

![](img/4d9a992abc5da7946ac44f9e6bf1d032_468_0.png)

为方便起见，迄今所学的一切再次呈现如下。

# 计数循环结构

```
for (counter = initial_value; counter OP1 final_value; counter = counter OP2 offset) {
    A statement or block of statements
}
```

![](img/4d9a992abc5da7946ac44f9e6bf1d032_468_1.png)

# 前测试循环结构

```
counter = initial_value;
while (counter OP1 final_value) {
    A statement or block of statements
    counter = counter OP2 offset;
}
```

![](img/4d9a992abc5da7946ac44f9e6bf1d032_468_2.png)

# 后测试循环结构

```
counter = initial_value;
if (counter OP1 final_value) {
    do {
        A statement or block of statements
        counter = counter OP2 offset;
    } while (counter OP1 final_value);
}
```

where

+   - counter 必须始终是一个变量。

# 练习 29.11-1 转换 PHP 脚本

使用后测试循环结构重写以下 PHP 脚本。

```php
<?php
    $start = trim(fgets(STDIN));
    $end = trim(fgets(STDIN));
    $x = 5;

    for ($i = $start; $i <= $end; $i++) {
        $x = pow($x, 1.5);
    }
    echo $x;
?>
```

## 解答

中间前测试循环结构如下。

```php
<?php
    $start = trim(fgets(STDIN));
    $end = trim(fgets(STDIN));
    $x = 5;

    $i = $start;
    while ($i <= $end) {
        $x = pow($x, 1.5);
        $i++;
    }
    echo $x;
?>
```

最终的后测试循环结构为

```php
<?php
    $start = trim(fgets(STDIN));
    $end = trim(fgets(STDIN));

$x = 5;

$i = $start;
if ($i <= $end) {
    do {
        $x = pow($x, 1.5);
        $i++;
    } while ($i <= $end);
}
echo $x;
?>
```

## 练习 29.11-2 转换 PHP 脚本

使用后测试循环结构重写以下 PHP 脚本。

```php
<?php
$x = 10;

for ($i = -4; $i <= 4; $i++) {
    $x = pow($x, 2);
}
echo $x;
?>
```

## 解答

中间前测试循环结构如下。

```php
<?php
$x = 10;

$i = -4;
while ($i <= 4) {
    $x = pow($x, 2);
    $i++;
}
echo $x;
?>
```

后测试循环结构为

```php
<?php

$x = 10;

$i = -4;
if ($i <= 4) {
    do {
        $x = pow($x, 2);
        $i++;
    } while ($i <= 4);
}

echo $x;

?>
```

在这种情况下，由于变量 `$i` 不依赖于用户输入（它被赋予常量值 -4），决策结构是多余的，可以省略。

```php
<?php

$x = 10;

$i = -4;
do {
    $x = pow($x, 2);
    $i++;
} while ($i <= 4);

echo $x;

?>
```

# 29.12 从后测试循环结构转换为计数循环结构

此转换没有自己的规则，但你可以使用已经学过的规则，即，你可以从后测试循环结构转换为中间前测试循环结构，最后转换为计数循环结构，如下图所示。

![](img/4d9a992abc5da7946ac44f9e6bf1d032_471_0.png)

请记住，在 PHP 以外的计算机编程语言中，例如 Visual Basic、Pascal 和 Delphi（仅举几例），你可以进行此类转换，但仅在特定情况下。在大多数编程语言中实际上可以进行转换的后测试循环结构的一般形式如下。

# 后测试循环结构

```
counter = initial_value;
do {
    A statement or block of statements 1
    counter = counter OP2 offset;
    A statement or block of statements 2
} while (counter OP3 final_valuel);
```

# 前测试循环结构

```
counter = initial_value;
A statement or block of statements 1
counter = counter OP2 offset;
A statement or block of statements 2
while (counter OP3 final_valuel) {
    A statement or block of statements 1
    counter = counter OP2 offset;
    A statement or block of statements 2
}
```

# 计数循环结构

```
counter = initial_value;
A statement or block of statements 1
counter = counter OP2 offset;
A statement or block of statements 2
for (counter = initial_value OP2 offset;
    counter OP1 final_value2;
    counter = counter OP2 offset) {
    A statement or block of statements 1
    A statement or block of statements 2
}
```

+   - **where**
+     - `counter` 必须始终是一个变量。
+     - `initial value`、`final value1`、`final value2` 和 `offset` 可以是常量值，甚至可以是变量或表达式。但是，如果是变量或表达式，则内容或结果在循环内必须相应保持不变。
+     - `OP1` 在 `counter` 递增时必须为 `<=`，在 `counter` 递减时必须为 `>=`。
+     - `OP2` 在 `counter` 递增时必须为 `+`，在 `counter` 递减时必须为 `-`。
+     - `OP3` 可以是任何比较运算符（`<`、`>`、`<=`、`>=`、`==`、`!=`）。
+     - 在语句或语句块 2（位于循环内部）中，任何现有的 `counter` 变量都必须替换为表达式 `counter OP2 offset`。

# 练习 29.12-1 转换 PHP 脚本

使用计数循环结构重写以下 PHP 脚本。

```php
<?php
$s = 0;
$a = trim(fgets(STDIN));
$i = $a;
do {
    $s = $s + pow($i, 2);
    $i = $i + 1;
} while ($i != 10);
echo $s;
?>
```

## 解答

中间前测试循环结构如下。

```php
<?php
$s = 0;
$a = trim(fgets(STDIN));
$i = $a;
$s = $s + pow($i, 2);
$i = $i + 1;
while ($i != 10) {
    $s = $s + pow($i, 2);
    $i = $i + 1;
}
```

![](img/4d9a992abc5da7946ac44f9e6bf1d032_473_0.png)

最终的计数循环结构变为

```php
<?php
$s = 0;
$a = trim(fgets(STDIN));
$i = $a;
$s = $s + pow($i, 2);
$i = $i + 1;

for ($i = $a + 1; $i <= 9; $i = $i + 1) {
    $s = $s + pow($i, 2);
}
echo $s;
?>
```

# 练习 29.12-2 转换 PHP 脚本

使用计数循环结构重写以下 PHP 脚本。

```php
<?php
$s = 0;
$a = trim(fgets(STDIN));
$i = $a;
do {
    $s = $s + $i;
    $i = $i + 3;
    $s = $s + pow($i, 2);
} while ($i < 60);
echo $s;
?>
```

## 解答

中间前测试循环结构如下。

```php
<?php
$s = 0;
```

