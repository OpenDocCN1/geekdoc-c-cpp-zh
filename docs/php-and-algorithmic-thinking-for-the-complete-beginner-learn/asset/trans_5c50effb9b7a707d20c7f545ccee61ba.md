

```php
$s = 0.5 * $a * $t * $t;

echo "Your car traveled ", $s, " meters";
?>
```

## Exercise 10.1-5 开尔文转华氏度

编写一个 PHP 脚本，将华氏度¹的温度值转换为开尔文²等效值。所需公式为

1.8 × 开尔文 = 华氏度 + 459.67

### 解答

给定的公式不能直接在脚本中使用。在 PHP 等计算机语言中，不允许编写

```
1.8 * $kelvin = $fahrenheit + 459.67
```

记住！在等号（=）左侧的位置，只能存在一个单一变量。这个变量实际上是 RAM 中可存储值的一个区域。

该脚本将华氏度转换为开尔文。华氏度的值是已知值，由用户提供，而开尔文的值是 PHP 脚本需要计算的值。因此，你需要求解开尔文。经过一些计算，公式变为

开尔文 = (华氏度 + 459.67) / 1.8

PHP 脚本如下所示。

### file_10.1-5.php

```php
<?php
echo "Enter a temperature in Fahrenheit: ";
$fahrenheit = trim(fgets(STDIN));

$kelvin = ($fahrenheit + 459.67) / 1.8;
```

¹ Daniel Gabriel Fahrenheit (1686–1736) 是一位德国物理学家、工程师和玻璃吹制工，最著名的是发明了酒精温度计和水银温度计，并开发了以他名字命名的温度标尺。

² William Thomson, 1st Baron Kelvin (1824–1907)，是一位出生于爱尔兰的英国数学物理学家和工程师。他广为人知的是开发了绝对零度（开尔文温度标尺）的基础，因此温度测量单位以他命名。他发现了热电学中的汤姆逊效应，并帮助发展了热力学第二定律。

### file_10.1-7.php

```php
<?php
echo "Enter the price of a product: ";
$price_before_discount = trim(fgets(STDIN));

echo "Enter the discount offered (0 - 100): ";
$discount = trim(fgets(STDIN));

$discount_amount = $price_before_discount * $discount / 100;
$price_after_discount = $price_before_discount - $discount_amount;

echo "The price after discount is: ", $price_after_discount;
?>
```

## Exercise 10.1-8 计算销售税率和折扣

编写一个 PHP 脚本，提示用户输入商品的不含税价格以及以百分比表示的折扣（范围为 0 到 100）。然后脚本应计算并显示新价格。假设销售税率为 19%。

### 解答

这个练习只是前两个练习的组合！

### file_10.1-8.php

```php
<?php
define("VAT", 0.19);

echo "Enter the price of a product: ";
$price_before_discount = trim(fgets(STDIN));

echo "Enter the discount offered (0 - 100): ";
$discount = trim(fgets(STDIN));

$discount_amount = $price_before_discount * $discount / 100;
$price_after_discount = $price_before_discount - $discount_amount;

$sales_tax = $price_after_discount * VAT;
$price_after_tax = $price_after_discount + $sales_tax;

echo "The discounted after-tax price is: ", $price_after_tax;
?>
```

## 10.2 复习练习

完成以下练习。

1. 编写一个 PHP 脚本，提示用户输入底和高的值，然后计算并显示三角形的面积。

2. 编写一个 PHP 脚本，提示用户输入三角形的两个角，然后计算并显示第三个角。

   提示：任何三角形的内角和均为 180 度

3. 编写一个 PHP 脚本，让学生输入四次测试的成绩，然后计算并显示平均成绩。

4. 编写一个 PHP 脚本，提示用户输入半径的值，然后计算并显示圆的周长。

5. 编写一个 PHP 脚本，提示用户输入餐厅餐费，然后计算并显示 10% 小费、7% 销售税以及三者总和的金额。

6. 一辆汽车从静止开始，沿直线水平道路以恒定加速度行驶给定的秒数。编写一个 PHP 脚本，提示用户输入加速度（m/sec²）和行驶时间（sec），然后计算行驶距离。所需公式为

   $$S = u_0 t + \frac{1}{2}at^2$$

7. 编写一个 PHP 脚本，提示用户输入华氏度的温度，然后将其转换为摄氏度等效值。所需公式为

   $$\frac{C}{5} = \frac{F - 32}{9}$$

8. 身体质量指数（BMI）常用于判断一个人相对于身高是否超重或体重不足。计算 BMI 的公式为

   $$BMI = \frac{weight \cdot 703}{height^2}$$

   编写一个 PHP 脚本，提示用户输入体重（磅）和身高（英寸），然后计算并显示用户的 BMI。

9. 编写一个 PHP 脚本，提示用户输入小计和小费率（范围为 0 到 100），然后计算小费和总金额。例如，如果用户输入 30 和 10，PHP 脚本应显示“Tip is $3.00 and Total is $33.00”。

³ Anders Celsius (1701–1744) 是一位瑞典天文学家、物理学家和数学家。他在瑞典乌普萨拉创立了乌普萨拉天文台，并提出了以他名字命名的摄氏温度标尺。

## 第 11 章 操作数字

```php
<?php
echo pi();             // outputs: 3.1415926535898
?>
```

### 幂运算

`pow (number, exp)`

返回 number 的 exp 次幂的结果。

### 示例

```php
<?php
$a = 2;
$b = 3;
echo pow($a, $b), "\n";       // outputs: 8

$c = pow(3,2);
echo $c, "\n";                // outputs: 9
?>
```

> **注意：** 函数 `pow()` 也可用于计算数字的平方根。从数学上可知，\(\sqrt[z]{X}=X^{1/z}\)。因此，你可以写 `$y = pow($x, 1/2)` 来计算 `$x` 的平方根，或者甚至可以写 `$y = pow($x, 1/3)` 来计算 `$x` 的立方根，以此类推！

### 随机数

`rand (minimum_value, maximum_value)`

返回 minimum_value 和 maximum_value 之间的伪随机整数。

### 示例

```php
<?php
echo rand(2, 10), "\n";       // outputs: 8
echo rand(0, 10)/10, "\n";    // outputs: 0.5
echo rand(20, 25), "\n";       // outputs: 22
?>
```

> **注意：** 随机数在计算机游戏中应用广泛。例如，“敌人”可能会在随机时间出现或朝随机方向移动。此外，随机数还用于模拟程序、统计程序、计算机安全中的数据加密等。

### 四舍五入

`round (number, [ precision ])`

返回 number 四舍五入到指定精度后的值。

### 示例

```php
<?php

$a = 5.312;
$b = 5.315;

echo round($a, 2), "\n";        // outputs: 5.31
echo round($b, 2), "\n";        // outputs: 5.32
echo round(2.3447, 3), "\n";   // outputs: 2.345
?>
```

### 正弦

`sin (number)`

返回 *number* 的正弦值。*number* 的值必须用弧度表示。

### 示例

```php
<?php

$a = sin(3 * pi() / 2);
echo $a;                         // outputs: -1
?>
```

### 平方根

`sqrt (number)`

返回 *number* 的平方根。

### 示例

```php
<?php

echo sqrt(2), "\n";             // outputs: 1.4142135623731
echo sqrt(9), "\n";             // outputs: 3
?>
```

### 正切

`tan (number)`

返回 *number* 的正切值。*number* 的值必须用弧度表示。

### 示例

```php
<?php

$a = tan(10);
echo $a;                         // outputs: 0.64836082745909
?>
```

## Exercise 11.2-1 计算两点之间的距离

编写一个 PHP 脚本，提示用户输入两个点的坐标（x, y），然后计算它们之间的直线距离。所需公式为

$$d = \sqrt{(x_1 - x_2)^2 + (y_1 - y_2)^2}$$

### 解答

在这个练习中，你需要使用两个函数：`pow()` 函数，返回数字的幂运算结果；以及 `sqrt()` 函数，返回数字的平方根。

为了简化问题，分别计算 $(x_1 - x_2)^2$ 和 $(y_1 - y_2)^2$，并将结果赋值给两个临时变量。

PHP 脚本如下所示。

```php
<?php

echo "Enter coordinates for point A: ";
$x1 = trim(fgets(STDIN));
$y1 = trim(fgets(STDIN));

echo "Enter coordinates for point B: ";
$x2 = trim(fgets(STDIN));
$y2 = trim(fgets(STDIN));

$x_temp = pow($x1 - $x2, 2);
$y_temp = pow($y1 - $y2, 2);

$d = sqrt($x_temp + $y_temp);

echo "Distance between points: ", $d;
?>
```

现在让我们看看另一种方法。

你应该意识到，实际上可以将一个函数嵌套在另一个函数中。这样做时，嵌套函数的结果会作为外部函数的参数使用。这是大多数程序员偏好的编程风格，因为它可以节省大量代码行。当然，如果嵌套层数过多，就没有人能理解你的代码了。嵌套最多四层是可以接受的。

使用嵌套函数的 PHP 脚本如下所示。

```php
<?php

echo "Enter coordinates for point A: ";
```

