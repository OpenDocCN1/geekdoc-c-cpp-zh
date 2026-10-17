

## Exercise 29.5-1 清理循环

以下代码片段计算数字 1、2、3、4、... 10000 的平均值。尝试尽可能多地将语句移到循环外部，以使脚本更高效。

```php
$s = 0;
for ($i = 1; $i <= 10000; $i++) {
    $s = $s + $i;
    $average = $s / 10000;
}
echo $average;
```

## Solution

初学者在计算平均值时最常见的错误之一，就是将计算平均值的语句放在循环内部。想想看！假设你想计算自己在学校的平均成绩。你的第一步是计算所有课程成绩的总和。然后，当所有成绩都加起来后，你会用这个总和除以你所修课程的数量。

> **注意：** 计算平均值是一个两步过程。

因此，在循环内部计算平均值是没有意义的。你可以将该语句移到循环外部，紧跟在循环之后，只让循环负责对数字求和，如下所示。

```php
$s = 0;
for ($i = 1; $i <= 10000; $i++) {
    $s = $s + $i;
}
$average = $s / 10000;
echo $average;
```

## Exercise 29.5-2 清理循环

*下面的公式*

$$S=\frac{1}{1+2^2+3^3+\cdots+N^N}+\frac{2}{1+2^2+3^3+\cdots+N^N}+\cdots+\frac{N}{1+2^2+3^3+\cdots+N^N}$$

使用以下 PHP 脚本求解，其中 $N$ 由用户给出。

```php
<?php
echo "Enter N: ";

$n = trim(fgets(STDIN));

$s = 0;

for ($i = 1; $i <= $n; $i++) {
    $denom = 0;
    for ($j = 1; $j <= $n; $j++) {
        $denom += pow($j, $j);
    }
    $s += $i / $denom;
}
echo $s;
?>
```

![](img/4d9a992abc5da7946ac44f9e6bf1d032_447_0.png)

*尝试尽可能多地将语句移到循环外部，以使脚本更高效。*

## Solution

正如你从公式中所见，分母对所有分数都是相同的。因此，为每个分数反复计算它是没有意义的。你可以只计算一次分母，并多次使用结果，如下所示。

```php
<?php
echo "Enter N: ";

$n = trim(fgets(STDIN));

$denom = 0;
for ($j = 1; $j <= $n; $j++) {
    $denom += pow($j, $j);
}

$s = 0;
for ($i = 1; $i <= $n; $i++) {
    $s += $i / $denom;
}
echo $s;
?>
```

## 29.7 从计数循环结构转换为前测试循环结构

从计数循环结构转换为前测试循环结构非常简单。你只需要获取 `for` 语句的 `counter` 变量，并在 `while` 语句中使用它，如下所示。

### 计数循环结构

```
for (counter = initial_value; counter OP1 final_value; counter = counter OP2 offset) {
    A statement or block of statements
}
```

![](img/4d9a992abc5da7946ac44f9e6bf1d032_449_0.png)

### 前测试循环结构

```
counter = initial_value;
while (counter OP1 final_value) {
    A statement or block of statements
    counter = counter OP2 offset;
}
```

其中

- `counter` 必须始终是一个变量。
- `initial_value`、`final_value` 和 `offset` 可以是常量值，甚至可以是变量或表达式。
- 当 counter 递增时，`OP1` 必须是 `<=`；当 counter 递减时，必须是 `>=`。
- 当 counter 递增时，`OP2` 必须是 `+`；当 counter 递减时，必须是 `−`。

> **记住！** 注意不要忘记在前测试循环结构末尾包含递增或递减 `counter` 变量的语句，否则循环将无限迭代！

### Exercise 29.7-1 转换 PHP 脚本

使用前测试循环结构重写以下 PHP 脚本。

```php
<?php
    $x = 2;

    for ($i = -4; $i <= 4; $i = $i + 1) {
        $x = pow($x, 2);
    }

echo $x;
?>
```

## Solution

以下是该练习的脚本，重新编写，并附有一些注释。

```php
<?php
    $x = 2;

    for ($i = -4; $i <= 4; $i = $i + 1) {
        $x = pow($x, 2);
    }

echo $x;
?>
```

![](img/4d9a992abc5da7946ac44f9e6bf1d032_450_0.png)

现在，一切都已澄清，可以使用前测试循环结构重写 PHP 脚本。

```php
<?php
    $x = 2;

    $i = -4;
    while ($i <= 4) {
        $x = pow($x, 2);
        $i = $i + 1;
    }

echo $x;
?>
```

如果你在 NetBeans IDE 中输入并执行这两个脚本，你会发现它们都显示相同的结果。

### Exercise 29.7-2 转换 PHP 脚本

使用前测试循环结构重写以下 PHP 脚本。

```php
<?php
    $f = trim(fgets(STDIN));
    $x = 3;

    for ($j = 20; $j >= $f; $j -= 5) {
        $x = $x / 2;
    }

    echo $x;
?>
```

## Solution

以下是该练习的脚本，重新编写，并附有一些注释。

```php
<?php
    $final = trim(fgets(STDIN));
    $x = 3;

    for ($j = 20;       $j >= $f;       $j -= 5) {
        $x = $x / 2;
    }

    echo $x;
?>
```

![](img/4d9a992abc5da7946ac44f9e6bf1d032_451_0.png)

现在，一切都已澄清，可以使用前测试循环结构重写 PHP 脚本。

```php
<?php
    $f = trim(fgets(STDIN));
    $x = 3;

    $j = 20;
    while ($j >= $f) {
        $x = $x / 2;
        $j -= 5;
    }

echo $x;
?>
```

## 29.8 从前测试循环结构转换为计数循环结构

在 PHP 中，将前测试循环结构转换为计数循环结构可以非常容易地完成，适用于任何形式的 while 语句。但是，你需要意识到，在计算机编程语言中，除了 PHP 之外，例如 Visual Basic、Pascal 和 Delphi（仅举几例），你可以进行这种转换，但只能在特定情况下进行。在本章的其余部分，你将遇到不应该始终进行转换的情况。

以下是前测试循环结构的一般形式，在大多数编程语言中实际上都可以进行转换。

### 前测试循环结构

```
counter = initial_value;
while (counter OP3 final_value1) {
    A statement or block of statements 1
    counter = counter OP2 offset;
    A statement or block of statements 2
}
```

![](img/4d9a992abc5da7946ac44f9e6bf1d032_452_0.png)

### 计数循环结构

```
for (counter = initial_value; counter OP1 final_value2; counter = counter OP2 offset)
{
    A statement or block of statements 1
    A statement or block of statements 2
}
```

其中

- `counter` 必须始终是一个变量。
- `initial_value`、`final_value1`、`final_value2` 和 `offset` 可以是常量值，甚至可以是变量或表达式。但是，在变量或表达式的情况下，内容或结果在循环内部必须相应保持不变。
- **OP1** 当 *counter* 递增时必须是 `<=`，当 *counter* 递减时必须是 `>=`。
- **OP2** 当 *counter* 递增时必须是 `+`，当 *counter* 递减时必须是 `−`。
- **OP3** 可以是任何比较运算符（<, >, <=, >=, ==, !=）。
- 语句或语句块 2 中任何现有的 *counter* 变量必须替换为表达式 *counter OP2 offset*。

你现在可能有点困惑。别担心！下面的示例将帮助你理清思路。

### Exercise 29.8-1 转换 PHP 脚本

使用计数循环结构重写以下 PHP 脚本。

```php
<?php
  $S = 0;
  $i = 1;

  while ($i <= 9) {
      $S = $S + pow($i, 2);
      $i += 2;
  }

echo $S;
?>
```

## Solution

以下是该练习的脚本，重新编写，并附有一些注释。

![](img/4d9a992abc5da7946ac44f9e6bf1d032_453_0.png)

## 循环控制结构的技巧和窍门

以下是该练习的脚本，重新编写，并附有一些注释。

```php
<?php
    $s = 0;
    $y = 0;

    while ($y != -3) {
        $s = $s + 2 * $y;
        $y = $y - 2;
    }

    echo $s;
?>
```

![](img/4d9a992abc5da7946ac44f9e6bf1d032_455_0.png)

一些额外说明：

- 由于 `counter` 递减，`OP1` 必须是 `>=`。
- 由于 `offset` 是 2，且变量 `$y` 递减，并且循环的布尔表达式是 `$y != -3`，可以清楚地看出，前测试循环结构进行迭代的 `$y` 的最后一个值是 -1。因此，`final_value2` 必须是 -1。
- 在语句或语句块 1 中，变量 `counter` 必须保持不变。

现在，一切都已澄清，可以使用计数循环结构重写 PHP 脚本。

```php
<?php
    $s = 0;
    for ($y = 5; $y >= -1; $y = $y - 2) {
        $s = $s + 2 * $y;
    }
    echo $s;
?>
```

### Exercise 29.8-3 转换 PHP 脚本

使用计数循环结构重写以下 PHP 脚本。

