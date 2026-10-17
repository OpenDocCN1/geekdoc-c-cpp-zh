
```php
$f = 5.5;

$b = array(1,2,3,4,5);

$a = array('a' => 'b', 'c' => 'd');

printf("My values are: %d, %.2f, %d, %d, %s\n", $i, $f, $b[0], $a['a']);

?>
```

我们带回熟悉的测试代码，并用 `printf` 语句替换我们的输出。我们看到对于整数使用 `%d`，对于浮点数使用 `%f`（在本例中为小数点后两位），对于字符串使用 `%s`（在本例中为数组）。

### 注意

格式字符串语法可能非常复杂，选项比我们提供的多。要查看字符串格式的列表以及 `sprintf` 函数，请访问 `php.net/manual/en/function/sprintf.php`。

### 控制语句

现在我们有了处理 PHP 的基础。所以，让我们处理我们可以创建的一些条件和循环。我们将涵盖三种循环：`for` 循环、`foreach` 循环和 `while` 循环。这三个循环结构提供了足够的功能来处理任何代码块。我们还需要查看条件语句，以理解如何根据条件控制块的执行。为了实现这一点，我们将编写一些代码，遍历访问服务器变量和环境变量的一些内置数组。

```php
<?php

if(function_exists('php_uname'))

{

    print "Server Uname is: ";

    print php_uname();

    print "\n";

}

foreach ($ENV as $i) {

    print "$ENV[$i] = {$ENV[$i]}\n";

}

$keys = array_keys($SERVER);

for($i = 0; $i < count($keys); $i++) {

    if ($keys[$i] == '_' || $keys[$i] == 'ORACLE_HOME') {

        continue;

    }

    print "$SERVER[$keys[$i]] = {$SERVER[$keys[$i]}\n";

}

$i = 0;

$keys = array_keys($_GET);

while($i < count($keys)) {

    print "$GET[$keys[$i]] = {$GET[$keys[$i]}\n";

    $i++;

}

?>
```
