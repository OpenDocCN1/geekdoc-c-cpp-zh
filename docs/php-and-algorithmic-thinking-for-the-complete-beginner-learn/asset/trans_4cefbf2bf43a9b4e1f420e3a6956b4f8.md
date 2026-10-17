
## 解答

插入排序算法对于大规模数据来说效率较低，选择排序和冒泡排序算法也是如此，但插入排序通常比这两者表现更好。此外，在排序非常小的数组时，插入排序算法可能会非常快——甚至比快速排序算法还要快。

插入排序算法的原理类似于你整理扑克牌的方式。你先把所有牌面朝下放在桌上，这些牌就代表未排序的“数组”。一开始你的左手是空的，但最终这只手会拿满排好序的牌。过程如下：你每次从桌上拿起一张牌，然后将其插入到左手中正确的位置。为了找到一张牌的正确位置，你将它和左手里已有的每张牌从右到左逐一比较。最后，桌上不再有牌，而你的左手将拿着所有排好序的牌。

例如，让我们尝试按升序对以下数组进行排序。为了更好地理解这个示例，数组的前三个元素已经为你排好序。

![](img/4d9a992abc5da7946ac44f9e6bf1d032_723_0.png)

位于位置 3 的元素（即 8）被从数组中移除，其左侧所有值大于 8 的元素都向右移动。数组 A 变为

![](img/4d9a992abc5da7946ac44f9e6bf1d032_723_1.png)

现在空出了一个位置，于是将值 8 插入其中。数组变为

![](img/4d9a992abc5da7946ac44f9e6bf1d032_723_2.png)

位于位置 4 的元素（即 10）被从数组中移除，其左侧所有值大于 10 的元素都向右移动。数组 A 变为

![](img/4d9a992abc5da7946ac44f9e6bf1d032_723_3.png)

现在空出了一个位置，于是将值 10 插入其中。数组变为

位于位置 5 的元素被从数组中移除，其左侧所有值大于 18 的元素都向右移动。数组 A 变为

![](img/4d9a992abc5da7946ac44f9e6bf1d032_724_1.png)

现在空出了一个位置，于是将值 18 插入其中。数组变为

![](img/4d9a992abc5da7946ac44f9e6bf1d032_724_2.png)

位于位置 6 的元素被从数组中移除，其左侧所有值大于 9 的元素都向右移动。数组 A 变为

![](img/4d9a992abc5da7946ac44f9e6bf1d032_724_3.png)

现在空出了一个位置，于是将值 9 插入其中。这是该过程的最后一步。算法结束，数组现在已排好序。

![](img/4d9a992abc5da7946ac44f9e6bf1d032_724_4.png)

> **记住！** 该算法实际上所做的是逐一检查未排序的元素，并将每个元素插入到那些已被视为已排序的元素中的适当位置。

下面这段代码片段使用插入排序算法按升序对数组进行排序。

```text
for ($m = 1; $m <= ELEMENTS - 1; $m++) {
    //"Remove" the element at index position $m from the array and
    //keep it in variable $element
    $element = $a[$m];

    //Shift appropriate elements to the right
    $n = $m;
    while ($n > 0 && $a[$n - 1] > $element) {
        $a[$n] = $a[$n - 1];
        $n--;
    }
    //insert the previously "removed" element at index position $n
    $a[$n] = $element;
}
```

注意：位于索引位置 $m 的元素实际上并未从数组中移除，而是在执行右移时被覆盖。这就是为什么在移动元素之前，其值被保存在变量 $element 中。

注意：如果希望按降序对数组排序，只需将 while 语句的布尔表达式改为 $n > 0 && $a[$n - 1] < $element 即可。

记住！与之前的排序算法一样，要对字母数字数据排序，你不需要对算法做任何修改！

# 练习 37.4-11 三个最差耗时

十位赛车手在赛道上尽可能快地驾驶各自的赛车。每辆车跑 20 圈，并记录每一圈对应的耗时（以秒为单位）。编写一个 PHP 脚本，提示用户输入每位车手的姓名以及每一圈的耗时。然后，脚本应显示每位车手的姓名以及其三个最差耗时。使用插入排序算法。

# 解答

在本练习中，你需要以下两个数组。

![](img/4d9a992abc5da7946ac44f9e6bf1d032_725_0.png)

用户输入所有数据后，PHP 脚本必须按降序对数组的每一行进行排序，但最终只显示前三列。

# 更多数组练习

使用“由内到外”的方法，下面的代码片段使用插入排序算法，仅对二维数组 `$elapsed_times` 的第一行（行索引 0）按降序排序。假设变量 `$i` 的值为 0。

```php
for ($m = 1; $m <= LAPS - 1; $m++) {
    $element = $elapsed_times[$i][$m];
    $n = $m;
    while($n > 0 && $elapsed_times[$i][$n - 1] < $element) {
        $elapsed_times[$i][$n] = $elapsed_times[$i][$n - 1];
        $n--;
    }
    $elapsed_times[$i][$n] = $element;
}
```

现在，为了对所有行进行排序，你需要将此代码片段嵌套在一个计数循环结构中，遍历所有行，如下所示。

```php
for ($i = 0; $i <= CARS - 1; $i++) {
    for ($m = 1; $m <= LAPS - 1; $m++) {
        $element = $elapsed_times[$i][$m];
        $n = $m;
        while($n > 0 && $elapsed_times[$i][$n - 1] < $element) {
            $elapsed_times[$i][$n] = $elapsed_times[$i][$n - 1];
            $n--;
        }
        $elapsed_times[$i][$n] = $element;
    }
}
```

现在，让我们专注于给定的练习。最终的 PHP 脚本如下。

```php
// file_37.4-11.php
<?php
define("CARS", 10);
define("LAPS", 20);

// Read names and elapsed times all together
$names = array();
$elapsed_times = array(array());
for ($i = 0; $i <= CARS - 1; $i++) {
    echo "Enter name for driver No. ", $i + 1, ": ";
    $names[$i] = trim(fgets(STDIN));
    for ($j = 0; $j <= LAPS - 1; $j++) {
        echo "Enter elapsed time for lap No. ", $j + 1, ": ";
```

# 练习 37.5-1 线性搜索算法——在一维数组中搜索可能多次出现的相同值

编写一个代码片段，在一维数组中搜索给定的值。假设数组中可能多次出现相同的值。使用线性搜索算法。

# 解答

线性（或顺序）搜索算法先检查数组的第一个元素是否等于给定值，然后检查第二个元素，再检查第三个元素，依此类推，直到数组末尾。由于这种逐元素检查的过程相当慢，因此线性搜索算法适用于元素较少的数组。

下面的代码片段演示了该算法。它在数组 `$haystack` 中查找给定的值 `$needle`！

```php
echo "Enter a value to search: ";
$needle = trim(fgets(STDIN));

$found = false;
for ($i = 0; $i <= ELEMENTS - 1; $i++) {
    if ($haystack[$i] == $needle) {
        echo $needle, " found at position: ", $i, "\n";
        $found = true;
    }
}

if ($found == false) {
    echo "Nothing found!";
}
```

# 练习 37.5-2 显示所有同名者的姓氏

编写一个 PHP 脚本，提示用户输入 20 个人的姓名：将名字存入数组 `$first_names`，将姓氏存入数组 `$last_names`。然后，脚本应询问用户一个名字，并在输入后搜索并显示所有名字与给定名字相同的人的姓氏。

# 解答

解决方案如下。

```php
<?php
define("PEOPLE", 20);

$first_names = array();
$last_names = array();
for ($i = 0; $i <= PEOPLE - 1; $i++) {
    echo "Enter first name: ";
    $first_names[$i] = trim(fgets(STDIN));
    echo "Enter last name: ";
    $last_names[$i] = trim(fgets(STDIN));
}

echo "Enter a first name to search: ";
$needle = trim(fgets(STDIN));

$found = false;
for ($i = 0; $i <= PEOPLE - 1; $i++) {
    if (strtoupper($first_names[$i]) == strtoupper($needle)) {
        echo $last_names[$i], "\n";
        $found = true;
    }
}

if ($found == false) {
    echo "No one found!";
}
?>
```

> **注意：** 尽管在题目的表述中不太明显，但数组 `$first_names` 确实可能多次包含同一个值。例如，遇到两个名叫“John”的人有多罕见呢？

> **注意：** 由于脚本处理的是字母数字数据，因此需要使用 `strtoupper()` 函数，以确保脚本对任何给定值都能正确运行。例如，如果数组 `$first_names` 中存在值 “John”，而用户想要搜索“JOHN”，`strtoupper()` 函数可确保脚本找到所有 John。

