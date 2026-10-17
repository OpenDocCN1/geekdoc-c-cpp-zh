

## 第 36 章
带数组的流程图

```php
for ($i = 0; $i <= ROWS - 1; $i++) {
    for ($j = 0; $j <= COLUMNS - 1; $j++) {
        if ($a[$i][$j] > $max) {
            $max = $a[$i][$j];
        }
    }
}

echo $max;
?>
```

# 解答

在此 PHP 脚本中，有两个嵌套的循环控制结构，其中第二个嵌套了一个单选分支决策结构。相应的流程图如下所示。

![](img/4d9a992abc5da7946ac44f9e6bf1d032_657_0.png)

# 解答

此练习非常简单。后测试循环结构嵌套于前测试循环结构中（或者，如果你愿意，也可以是计数循环结构）。你必须克服的唯一障碍是，内部后测试循环结构的真分支和假分支的位置并不完全正确，因为必须向上走的是真分支，而不是假分支。正如你已经学到的，可以交换两个分支，但你还需要否定相应的布尔表达式。代码片段如下。

```php
for ($i = 0; $i <= CITIES - 1; $i++) {
    do {
        $b[$i] = trim(fgets(STDIN));
    } while ($b[$i] >= 0);
}
```

# ## 练习 36.3-2 编写 PHP 脚本

编写与以下流程图对应的 PHP 脚本。

![](img/4d9a992abc5da7946ac44f9e6bf1d032_659_0.png)

# 解答

在此练习中，双选分支决策结构嵌套于后测试循环结构中。相应的 PHP 脚本如下。

```php
<?php
$i = 1;
$m = 0;
$n = 0;
$pos = array();
$neg = array();
do {
    $b = trim(fgets(STDIN));
    if ($b < 0) {
        $pos[$m] = $b;
        $m++;
    } else {
        $neg[$n] = $b;
        $n++;
    }
    $i++;
} while ($i < 90);
echo "The End";
?>
```

# 练习 36.3-3 编写 PHP 脚本

编写与以下流程图片段对应的 PHP 脚本。

![](img/4d9a992abc5da7946ac44f9e6bf1d032_661_0.png)

# ## 解答

此流程图中有一个单决策结构嵌套于前测试循环结构中，而该前测试循环结构又嵌套于另一个前测试循环结构中。

由于变量 i 和 j 用作数组 a 的索引位置，你可以假设它们是整数。因此，可以将两个布尔表达式分别更改为 i <= CITIES - 1 和 j <= CITIZENS - 1。此更改有助于你使用计数循环结构编写相应的 PHP 脚本，如下所示。

```php
$max_i = 0;
$max_j = 0;
for ($i = 0; $i <= CITIES - 1; $i++) {
    for ($j = 0; $j <= CITIZENS - 1; $j++) {
        if ($a[$i][$j] > $a[$max_i][$max_j]) {
            $max_i = $i;
            $max_j = $j;
        }
    }
}
```

```php
echo ${a[$max_i][$max_j]};
```

# ## 36.4 复习练习

完成以下练习。

+   1. 设计与以下 PHP 脚本对应的流程图。

```php
<?php

define("ELEMENTS", 30);

$values = array();
for ($i = 0; $i <= ELEMENTS - 1; $i++) {
    echo "Enter a two-digit integer: ";
    $values[$i] = trim(fgets(STDIN));
}

for ($i = 0; $i <= ELEMENTS - 1; $i++) {
    $digit1 = intval($values[$i] / 10);
    $digit2 = $values[$i] % 10;
    if ($digit1 < $digit2) {
        echo $values[$i];
    }
}
?>
```

+   2. 设计与以下 PHP 脚本对应的流程图。

```php
<?php

define("ELEMENTS", 20);

$values = array();
for ($i = 0; $i <= ELEMENTS - 1; $i++) {
    echo "Enter a three-digit integer: ";
    $values[$i] = trim(fgets(STDIN));
}

$sum = 0;
for ($i = 0; $i <= ELEMENTS - 1; $i++) {
    $digit3 = $values[$i] % 10;
    $r = intval($values[$i] / 10);

    $digit2 = $r % 10;
    $digit1 = intval($r / 10);
}
```

```php
}
}
for ($i = 0; $i <= N - 1; $i++) {
    for ($j = 0; $j <= N - 1; $j++) {
        echo $a[$i][$j];
    }
}
?>
```

# 5. 设计与以下代码片段对应的流程图。

```php
$average = array();
for ($i = 0; $i <= ROWS - 1; $i++) {
    $average[$i] = 0;
    for ($j = 0; $j <= COLUMNS - 1; $j++) {
        $average[$i] += $values[$i][$j];
    }
    $average[$i] /= COLUMNS;
}
for ($i = 0; $i <= ROWS - 1; $i++) {
    if ($average[$i] > 89)
        echo $average[$i];
}
```

# 6. 编写与以下流程图片段对应的 PHP 脚本。

![](img/4d9a992abc5da7946ac44f9e6bf1d032_664_0.png)

# ## 7. 编写与以下流程图片段对应的 PHP 脚本。

![](img/4d9a992abc5da7946ac44f9e6bf1d032_665_0.png)

# ## 8. 编写与以下流程图片段对应的 PHP 脚本。

![](img/4d9a992abc5da7946ac44f9e6bf1d032_665_1.png)

# 第 37 章

# 数组的更多练习

# 第 37 章 数组的更多练习

![](img/4d9a992abc5da7946ac44f9e6bf1d032_669_0.png)

相应的 PHP 脚本如下。

```php
<?php
define("ELEMENTS_OF_A", 10);
define("ELEMENTS_OF_NEW", ELEMENTS_OF_A - 2);

$a = array();
for ($i = 0; $i <= ELEMENTS_OF_A - 1; $i++) {
    $a[$i] = trim(fgets(STDIN));
}
```

```php
$new = array();
for ($i = 0; $i <= ELEMENTS_OF_NEW - 1; $i++) {
    $new[$i] = ($a[$i] + $a[$i + 1] + $a[$i + 2]) / 3;
}

for ($i = 0; $i <= ELEMENTS_OF_NEW - 1; $i++) {
    echo $new[$i], "\t";
}
?>
```

# 练习 37.1-2 创建包含最大值的数组

设计一个流程图并编写相应的 PHP 脚本，让用户向每个包含 20 个元素的数组 $a 和 $b 中输入数值。然后，算法（以及相应的脚本）应创建一个包含 20 个元素的新数组 $new。新数组的每个位置应包含数组 $a 和 $b 中对应位置的最大值。

# 解答

这里没有什么新内容！你需要四个计数循环结构：两个用于读取数组 $a 和 $b 的值，一个用于创建数组 $new，一个用于在屏幕上显示数组 $new。流程图如下所示。

![](img/4d9a992abc5da7946ac44f9e6bf1d032_670_0.png)

![](img/4d9a992abc5da7946ac44f9e6bf1d032_671_0.png)

相应的 PHP 脚本如下所示。

# file_37.1-2.php

```php
<?php
define("ELEMENTS", 20);

//Read arrays $a and $b
$a = array();
for ($i = 0; $i <= ELEMENTS - 1; $i++) {
    $a[$i] = trim(fgets(STDIN));
}
$b = array();
for ($i = 0; $i <= ELEMENTS - 1; $i++) {
    $b[$i] = trim(fgets(STDIN));
}
//Create array $new
$new = array();
for ($i = 0; $i <= ELEMENTS - 1; $i++) {
    if ($a[$i] > $b[$i]) {
        $new[$i] = $a[$i];
    } else {
        $new[$i] = $b[$i];
    }
}
//Display array $new
for ($i = 0; $i <= ELEMENTS - 1; $i++) {
    echo $new[$i], "\n";
}
?>
```

# 练习 37.1-3 合并一维数组

编写一个 PHP 脚本，让用户向分别包含 20 个和 30 个元素的数组 $a 和 $b 中输入数值。然后，脚本应创建一个包含 50 个元素的新数组 $new。该新数组的前 20 个位置应包含数组 $a 的元素，接下来的 30 个位置应包含数组 $b 的元素。

# 解答

正如你在下面的示例中所见，数组 $a 的元素索引位置与数组 $new 的索引位置之间存在一对一对应关系。数组 $a 中位置 0 的元素存储在数组 $new 的位置 0，数组 $a 中位置 1 的元素存储在数组 $new 的位置 1，以此类推。但是，数组 $b 的元素索引位置与数组 $new 的索引位置之间不存在一对一对应关系。数组 $a 中位置 0 的元素应存储在数组 $new 的位置 20，数组 $a 中位置 1 的元素应存储在数组 $new 的位置 21，以此类推。

![](img/4d9a992abc5da7946ac44f9e6bf1d032_673_0.png)

为了将数组 `$a` 的值赋给数组 `$new`，你可以使用以下代码片段。

```php
for ($i = 0; $i <= ELEMENTS_OF_A - 1; $i++) {
    $new[$i] = $a[$i];
}
```

但是，要将数组 `$b` 的值赋给数组 `$new`，你的代码片段应该有很大不同。

```php
for ($i = 0; $i <= ELEMENTS_OF_B - 1; $i++) {
    $new[ELEMENTS_OF_A + $i] = $a[$i];
}
```

最终的 PHP 脚本如下。

```php
// file_37.1-3.php
<?php
define("ELEMENTS_OF_A", 20);
define("ELEMENTS_OF_B", 30);
define("ELEMENTS_OF_NEW", ELEMENTS_OF_A + ELEMENTS_OF_B);

//Read arrays $a and $b
$a = array();
for ($i = 0; $i <= ELEMENTS_OF_A - 1; $i++) {
    $a[$i] = trim(fgets(STDIN));
}
$b = array();
for ($i = 0; $i <= ELEMENTS_OF_B - 1; $i++) {
    $b[$i] = trim(fgets(STDIN));
}

//Create array $new
$new = array();
for ($i = 0; $i <= ELEMENTS_OF_A - 1; $i++) {
    $new[$i] = $a[$i];
}
```

