

b 是一个保存值 abcd 的变量。

最后，我们还可以有布尔变量，它们只保存 true/false 值。例如：

```
var c = true;
var d = (7>5);
var e = (7<6);
```

变量 c、d 和 e 都是布尔变量。变量 c 被赋值为 true。变量 d 为 true（因为 7 大于 5）。变量 e 为 false（因为 7 不小于 6）。

## document.write()

document.write() 用于在网页上打印元素。括号内的任何内容都会打印在网页上。例如：

```
document.write("Example print");
```

上面的代码会在屏幕上打印出 “Example print” 这些字。

我们也可以在屏幕上打印变量。例如，

```
var a=7;
```

```
document.write(a)
```

上面的代码会在屏幕上打印出 7。

此外，我们还可以使用 “+” 运算符组合不同的元素。例如：

```
var a=7;
```

```
document.write("The number printed is "+a);
```

上面的代码会打印出 “The number printed is 7”。

## alert()

alert() 会在屏幕上弹出一个包含特定消息的弹窗。例如，

```
alert("Hello")
```

上面的代码会弹出一个显示 “Hello” 的弹窗。

![](img/443990a0ec620659ce8be783c0758bc6_253_0.png)

## prompt()

prompt() 具有相同的弹窗，但增加了一个允许用户输入的文本框。用户输入可以存储在一个变量中。例如：

```
var name = prompt("What is your name");
```

它会显示一个弹窗。当用户输入他的名字并点击“确定”后，该值会存储在变量 name 中。

![](img/443990a0ec620659ce8be783c0758bc6_254_0.png)

## document.getElementById().value

document.getElementById().value 用于将 HTML 元素获取到 JavaScript 变量中。因此，我们需要使用 HTML 元素的 id，并将其放在括号中。让我们看一个例子。

我们来看下面的 HTML 元素：

```
Enter number: <input name="x" type="number" id="test" size="20"><br>
```

JavaScript 代码：

```
var testv=document.getElementById("test").value;
```

这个 HTML 元素是一个表单文本框，用于获取用户输入的数字。在 JavaScript 中，用户输入的数字会被赋值给变量 testv。

## 如何添加注释

注释是添加到代码中用于记录或解释代码的内容。注释不会被执行，也不影响程序。在 JavaScript 中，注释是在注释内容前加两个正斜杠（"//"）来添加的。

```
<html>
<head>
<title>Print Name and Age.....</title>
</head>
<body>
<form id="form1">
Enter Name: <input name="Enter Name" type="text" id="name" size="20"><br>
Enter Favorite Hobby: <input type="text" id="hobby" size="20"><br>
Enter Age: <input type="number" id="age" size="20"><br>
</form>
<input type="button" onclick="writename()" value="Print Intro"></button>

<script>

function writename()
{
    //Creating variables
    var name=document.getElementById("name").value;
    var hobby=document.getElementById("hobby").value;
    var age=document.getElementById("age").value;

    //Prints name on screen
    document.write("Hi! "+name+"! I am "+age+" years old,My favorite hobby is "+hobby);
}

</script>
</body>
</html>
```

下面是注释的一个示例。注释以绿色显示并用红色圆圈标出。

## 示例 1

现在，让我们开始看一些例子。我们将从上一章中的 HTML 表单开始。我们将把所有用户输入赋值给变量，并使用 JavaScript 将它们打印在网页浏览器上。

下面的代码与上一章中的示例类似。添加了一个 JavaScript 函数，用于打印提交表单者的名字和国家。

```
<html>
<head><title>Sample Form</title></head>
<body>
<form id="form1">
Enter First Name:<input name="firstname" type="text" id="firstname" size="20"><br>
Enter Last Name:<input name="lname" type="text" id="lname" size="20"><br><br>
Enter Address: <textarea name="TextBox" cols="40" rows="5" id="txtarea"></textarea><br><br>
Enter Country: <select id="country" name="country">
        <option value="USA">USA</option>
        <option value="Mexico">Mexico</option>
        <option value="Canada">Canada</option>
        <option value="Australia">Australia</option>
        <option value="India">Australia</option>
</select>
Date of Birth: <input type="date" id="dobirth" name="trip-start"
 value="2020-07-01"
 min="1918-01-01" max="2020-06-31"><br>
<button onclick="printcountry()">Submit</button>

<script>
function printcountry()
{
var fname = document.getElementById("firstname").value;
var lname = document.getElementById("lname").value;
var address = document.getElementById("txtarea").value;
var country = document.getElementById("country").value;
var dob = document.getElementById("dobirth").value;
document.write(fname+" lives in "+country);
}
</script>

</body>
</html>
```

### 输出：

![](img/443990a0ec620659ce8be783c0758bc6_257_0.png)

点击**提交**后，我们会看到：

![](img/443990a0ec620659ce8be783c0758bc6_257_1.png)

### 代码解释

因此，我们添加的主要部分是函数 `printcountry()`。我们还将该函数添加到了按钮的 onclick 元素中。（`onclick="printcountry()"`）。

```
<script type="text/javascript">
<!--
function printName()
{
var fname = document.getElementById('fname').value;
var lname = document.getElementById('lname').value;
var address = document.getElementById('address').value;
var country = document.getElementById('country').value;
var dob = document.getElementById('dob').value;
document.write(fname + " " + dob);
}
//-->
</script>
```

在这个函数中，我们声明了五个变量 [fname](#)、[lname](#)、[address](#)、[country](#)、[dob](#)。这些变量分别被赋值为表单中输入的名字、姓氏、地址、国家和出生日期。这是通过 [document.getElementById()](#) 值的 JavaScript 元素完成的。最后，我们使用 document.write() 打印出表单中输入的名字和出生日期。

## 示例 2

在第二个示例中，我们创建一个简单的 JavaScript 函数，它接收 3 个数字并将它们相乘。

### 输出：

```
<html>
<head><title>Sample Form</title></head>
<body>
<form>
Enter First Number:<input name="number1" type="number" id="num1" size="20"><br>
Enter Second Number:<input name="number2" type="number" id="num2" size="20"><br>
Enter Third Number:<input name="number3" type="number" id="num3" size="20"><br><br>
<input type="button" value="multiplication()" onclick="multiplynum()">
</form>
<script>
function multiplynum()
{
var n1 = document.getElementById("num1").value;
var n2 = document.getElementById("num2").value;
var n3 = document.getElementById("num3").value;
document.write("The product of the three numbers is " + n1*n2*n3);
}
</script>
</body>
</html>
```

一旦我们点击提交，我们会得到：

![](img/443990a0ec620659ce8be783c0758bc6_259_0.png)

### 代码解释：

在上面的代码中，我们在表单中接收三个数字，其 id 分别为 num1、num2 和 num3。

当按钮被点击时，它会运行 **multiplynum()** JavaScript 函数。

在函数中，三个变量 n1、n2、n3 分别被赋值为表单中 id 为 num1、num2 和 num3 的三个数字。

最后，我们在最后一行使用 document.write() 打印出这三个数字 n1*n2*n3 的乘积。

## 练习问题

- 1. 创建[上一章的练习问题 1](#)中的表单。像制作一份正式的简历一样，将表单中的所有信息打印到网页上。如果看起来足够好，可以随意打印出来交给雇主。
- 2. 创建[上一章的练习问题 2](#)中的表单。将完整的购物清单打印到 HTML 网页上。然后你可以将它打印在一张纸上，去购物。
- 3. 创建一个接收两个数字的表单。它有 4 个按钮，按钮文本分别为 Add、Subtract、Multiply 和 Divide。这 4 个按钮分别执行 4 个不同的函数，对这两个数字进行加、减、乘、除，并打印出结果。

