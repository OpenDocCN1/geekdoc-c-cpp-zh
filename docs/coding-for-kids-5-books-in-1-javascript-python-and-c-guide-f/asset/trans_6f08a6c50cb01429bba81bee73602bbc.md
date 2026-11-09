

```html
<html>
<head><title>Sample Form</title></head>
<body>
<form id="form1">

<button onclick="multiplynum()">Parse Integers</button>

<script>
function multiplynum()
{
xi=parseInt("5.2");
yi=parseInt(5.01);
zi=parseInt(5.65);
xf=parseFloat("5.2");
yf=parseFloat(5.01);
zf=parseFloat(5.65);
document.write("xi= "+xi+"<br>");
document.write("yi= "+yi+"<br>");
document.write("zi= "+zi+"<br>");
document.write("xf= "+xf+"<br>");
document.write("yf= "+yf+"<br>");
document.write("zf= "+zf+"<br>");
}
</script>


</body>
</html>
```

### 输出：

```
xi= 5
yi= 5
zi= 5
xf= 5.2
yf= 5.01
zf= 5.65
```

我们可以看到，`parseInt` 和 `parseFloat` 的结果是不同的。对于 `xi` 和 `xf`，我们传入字符串 “5.2”。因为它位于引号内，所以被视为字符串。尽管引号内是数字，但如果不对其执行 `parseInt` 或 `parseFloat`，就无法在任何数学运算中使用它。在执行 `parseInt` 或 `parseFloat` 之后，它就变成了数字。我们还要注意，对于所有值，`parseInt` 会去掉小数点并使其成为整数。它不是向上或向下取整，只是去掉小数部分。`parseFloat` 则保留小数值。所以，如果你想处理小数，请使用 `parseFloat`。如果你不想要小数，则使用 `parseInt`。

## 数字取整 – Math.ceil()、Math.floor() 和 Math.round()

接下来，我们来讨论数字取整。我们会用到函数 **Math.ceil()、Math.floor() 和 Math.round()**。`Math.ceil()` 向上取整到较高的小数值，`Math.floor()` 向下取整到较低的小数值，而 `Math.round()` 则取最接近的值（无论是向上还是向下）。让我们看一个示例程序。

```html
<html>
<head><title>Sample Form</title></head>
<body>
<form id="form1">

<button onclick="multiplynum()">Round numbers</button>

<script>
function multiplynum()
{
xc=Math.ceil(5.2);
yc=Math.ceil(7.8);
zc=Math.ceil(4.5);
xf=Math.floor(5.2);
yf=Math.floor(7.8);
zf=Math.floor(4.5);
xr=Math.round(5.2);
yr=Math.round(7.8);
zr=Math.round(4.5);
document.write("Example of Math.ceil<br>");
document.write("xc= "+xc+"<br>");
document.write("yc= "+yc+"<br>");
document.write("zc= "+zc+"<br>");
document.write("Example of Math.floor<br>");
document.write("xf= "+xf+"<br>");
document.write("yf= "+yf+"<br>");
document.write("zf= "+zf+"<br>");
document.write("Example of Math.round<br>");
document.write("xr= "+xr+"<br>");
document.write("yr= "+yr+"<br>");
document.write("zr= "+zr+"<br>");
}
</script>

</form>
</body>
</html>
```

在代码中，我们将 3 个小数分别传入 `Math.floor()`、`Math.ceil()` 和 `Math.round()`，输出结果展示了这些函数的用法。

### 输出：

```
Example of Math.ceil
xc= 6
yc= 8
zc= 5
Example of Math.floor
xf= 5
yf= 7
zf= 4
Example of Math.round
xr= 5
yr= 8
zr= 5
```

## 加、减、乘、除

这似乎不言自明，但鉴于任何基本计算都至关重要，我还是要介绍一下这 4 种基本数学运算。

```html
<html>
<head><title>Sample Form</title></head>
<body>
<form id="form1">
Enter First Number:<input name="number1" type="number" id="num1" size="20"><br>
Enter Second Number:<input name="number2" type="number" id="num2" size="20"><br><br>

<button onclick="test()">Calculate</button>

<script>
function test()
{
var n1 = parseInt(document.getElementById("num1").value);
var n2 = parseInt(document.getElementById("num2").value);
var sum=n1+n2;
var difference=n1-n2;
var product=n1*n2;
var quotient=n1/n2;

document.write("The sum is "+sum+"<br>");
document.write("The difference is "+difference+"<br>");
document.write("The product is "+product+"<br>");
document.write("The quotient is "+quotient);
}
</script>

</body>
</html>
```

在代码中，我们通过一个 HTML 表单接收两个数字。这两个数字被赋值给变量 `n1` 和 `n2`。

然后我们计算总和、差、积和商，并将它们赋值给 4 个不同的变量。

最后，使用 `document.write()` 将这 4 个变量打印出来。

### 输出：

```
Enter First Number: 3
Enter Second Number: 5
Calculate

The sum is 8
The difference is -2
The product is 15
The quotient is 0.6
```

## 取模运算

取模运算返回两个数之间的余数。它看起来像百分号 `%`。下面是一个示例：

```html
<html>
<head><title>Sample Form</title></head>
<body>
<form id="form1">
Enter First Number:<input name="number1" type="number" id="num1" size="20"><br>
Enter Second Number:<input name="number2" type="number" id="num2" size="20"><br><br>

<button onclick="test()">Calculate Remainder</button>

<script>
function test()
{
var n1 = parseInt(document.getElementById("num1").value);
var n2 = parseInt(document.getElementById("num2").value);
var remainder=n1%n2;

document.write("The remainder when "+n1+" is divided by "+n2+" is "+remainder+"<br>");

}
</script>


</body>
</html>
```

上述代码通过一个 HTML 表单获取两个数字，并计算两者之间的余数，如下面的输出所示。

### 输出：

![](img/443990a0ec620659ce8be783c0758bc6_280_0.png)

点击 **“计算余数”** 按钮后

![](img/443990a0ec620659ce8be783c0758bc6_280_1.png)

## Math.random()

`Math.random()` 返回一个介于 0 和 1 之间的随机数。如果我们想获得一个介于 0 和 10 之间的随机数，可以将其乘以 10，然后对结果取整（使用 `Math.round()`）。让我们看几个示例。

```html
<html>
<head><title>Sample Form</title></head>
<body>

<button onclick="test()">Random Numbers</button>

<script>
function test()
{
var n1 = Math.random();
var n2 = Math.round(Math.random()*50);
var n3 = Math.round(Math.random()*50);
var n4 = Math.round(Math.random()*1000);

var remainder=n1%n2;

document.write("Random number between 0 and 1 = <strong>"+n1+"</strong><br>");
document.write("1st Random number between 0 and 50 = <strong>"+n2+"</strong><br>");
document.write("2nd Random number between 0 and 50 = <strong>"+n3+"</strong><br>");
document.write("Random number between 0 and 1000 = <strong>"+n4+"</strong><br>");

}
</script>

</body>
</html>
```

在上面的示例中，`n1` 是介于 0 和 1 之间的随机数。`n2` 和 `n3` 是介于 0 和 50 之间的两个不同随机数。你应该能看到 `n2` 和 `n3` 是不同的，因为这两个数字都是随机生成的。`n4` 返回一个介于 0 和 1000 之间的随机数。我们可以在下面的输出中看到结果。由于数字是随机生成的，每次运行程序时我们都会得到不同的结果。

`Math.random()` 是一个有趣的函数，在本书中我们会在很多游戏里用到它。

### 输出：

## 指数和对数

在 JavaScript 中，指数运算使用 `Math.pow()` 函数完成，自然对数使用 `Math.log()` 完成。如果我们要计算以 10 为底的对数，可以使用 `Math.log10()`。

```html
<html>
<head><title>Sample Form</title></head>
<body>

<button onclick="test()">Random Number</button>

<script>
function test()
{
var n1 = Math.pow(6,2);
var n2 = Math.pow(7,3);
var n3 = Math.log(100);
var n4 = Math.log10(100);

document.write("6 raised to the power 2 = <strong>"+n1+"</strong><br>");
document.write("7 raised to the power 3 = <strong>"+n2+"</strong><br>");
document.write("The natural logarithm of 100 is = <strong>"+n3+"</strong><br>");
document.write("Logarithm (to the base 10) of 100 is = <strong>"+n4+"</strong><br>");

}
</script>

</body>
</html>
```

在上面的代码中，我们有两个使用 `Math.pow(x,y)` 的指数示例。基本上，在两种情况下都是 `x` 的 `y` 次幂。`n1` 和 `n2` 给出指数结果。`n3` 显示 100 的自然对数，`n4` 显示 100 的以 10 为底的对数。

### 输出：

6 的 2 次方 = **36**  
7 的 3 次方 = **343**  
100 的自然对数为 = **4.605170185988092**  
100 的以 10 为底的对数为 = **2**

## 平方根

`Math.sqrt()` 用于求平方根，`Math.abs()` 用于求一个数的绝对值。

下面是一些示例：

```html
<html>
<head><title>Sample Form</title></head>
<body>

<button onclick="test()">Test</button>

<script>
function test()
{
var n1 = Math.sqrt(36);
var n2 = Math.sqrt(75);
var n3 = Math.abs(13);
var n4 = Math.abs(-14);

document.write("The square root of 36 = <strong>"+n1+"</strong><br>");
document.write("The square root of 75 = <strong>"+n2+"</strong><br>");
document.write("The absolute value of 13 is = <strong>"+n3+"</strong><br>");
document.write("The absolute value of -14 = <strong>"+n4+"</strong><br>");
}
</script>

</body>
</html>
```

在上面的代码中，`n1` 和 `n2` 是平方根函数的示例；而 `n3` 和 `n4` 是绝对值函数的示例。

如果你还没听说过绝对值函数，它基本上会返回一个正值，无论这个数是正数还是负数。所以，13 和 -13 都会返回绝对值 13。

### 输出：

