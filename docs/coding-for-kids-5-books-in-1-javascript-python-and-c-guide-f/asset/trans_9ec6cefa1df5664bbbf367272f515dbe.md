
上面的程序是上一章中的表单。我们只是添加了两行代码和一个函数。

这两行创建了一个 Home 按钮，它会运行函数 **redirect()**。**redirect()** 函数会再次运行该程序。**'form_JavaScript.html'** 是我们正在运行的文件名。你应将 **'form_JavaScript'** 改为你为 html 文件所起的任意名称。

### 输出 #1

![](img/443990a0ec620659ce8be783c0758bc6_311_0.png)

输入数字并点击 Submit 后，我们得到：

![](img/443990a0ec620659ce8be783c0758bc6_311_1.png)

现在，点击 Home 按钮后，我们得到：

![](img/443990a0ec620659ce8be783c0758bc6_311_2.png)

因此，它基本上是重新启动该 html 程序。

现在，让我们开始我们的第一个游戏。

## 游戏 1 — 猜随机数

在这个游戏中，我们将创建一个表单，通过文本框接收一个数字。该数字介于 0 和 10 之间。然后我们将该数字与通过 JavaScript（使用 Math.random()）生成的随机数进行比较。如果相同，则猜中的数字正确。如果不同，则我们告诉他们正确的数字。用户可以选择点击 Home 按钮并重试。请参见下面的代码和输出。

```html
<html>
<head><title>Guess Number</title>
<link rel="stylesheet" href="samplestyle.css" />
</head>
<body>
<form id="form1">
Guess Number between 0 and 10:<input name="name" type="number" id="num1" size="20"><br>
</form>
<button class="btn a" onclick="guessnumber()">Check</button>
<script>

function guessnumber()
{
var user=document.getElementById("num1").value;
var rand=Math.floor(Math.random()*10);
if (guess==rand)
{
    document.write("Congratulations. You guessed the right number");
}
else{
    document.write("Sorry. You guessed wrong. The correct number is "+rand);
}

document.write('<link rel="stylesheet" type="text/css" href="samplestyle.css" />');
document.write("<br>");
document.write('<button onclick="redirect()">Home</button>');

}

function redirect()
{
window.location.replace("GuessNumber.html");
}

</script>
</body>
</html>
```

### 输出：

![](img/443990a0ec620659ce8be783c0758bc6_312_0.png)

![](img/443990a0ec620659ce8be783c0758bc6_313_0.png)

如果我们点击 **Home**，就可以再次玩这个游戏。这个程序是练习条件循环和随机数生成器的好方法。

## 游戏 2 – 数学测验游戏

这个程序稍长一些，所以我把它分成了 2 张图片。它基本上会打印出 5 道简单的数学题，并通过表单接收这些题目的答案（它们的 id 为 **num1,num2,num3,num4,num5**）。这些答案会作为变量存储在 JavaScript 中（**answer1,answer2,answer3,answer4,answer5**）。使用 IF 函数将这些答案与正确答案进行比较。每当用户答对一题，计数器就加 1，最后打印计数器以查看用户答对了多少题。

```html
<html>
<head><title>Math Quiz</title></head>
<link rel="stylesheet" href="samplestyles.css" />
<body>
<form id="form1">
5*2 = :<input name="name" type="number" id="num1" size="20"><br>
7/2 = :<input name="name" type="float" id="num2" size="20"><br>
6*5 = :<input name="name" type="number" id="num3" size="20"><br>
14+29 = :<input name="name" type="number" id="num4" size="20"><br>
17-6 = :<input name="name" type="number" id="num5" size="20"><br>
</form>
<button class="btn" onclick="guessnumber()">Check</button>
<script>
function guessnumber()
{
var correct=0;

var answer1=parseInt(document.getElementById("num1").value);
var answer2=parseFloat(document.getElementById("num2").value);
var answer3=parseInt(document.getElementById("num3").value);
var answer4=parseInt(document.getElementById("num4").value);
var answer5=parseInt(document.getElementById("num5").value);

if (answer1==10)
{
    correct=correct+1;
}
if (answer2==3.5)
{
    correct=correct+1;
}
if (answer3==30)
{
    correct=correct+1;
}
if (answer4==43)
{
    correct=correct+1;
}
if (answer5==11)
{
    correct=correct+1;
}
document.write('<link rel="stylesheet" type="text/css" href="samplestyle.css" />');
document.write('You got '+correct+' answers correct');
}
</script>
</body>
</html>
```

### 输出：

![](img/443990a0ec620659ce8be783c0758bc6_315_0.png)

点击 **Check** 按钮后，我们得到：

![](img/443990a0ec620659ce8be783c0758bc6_315_1.png)

这是一个很棒的练习程序。但你可能会想，孩子们只能使用这个程序一次，因为我们总是使用相同的数字。为了解决这个问题，我们在下一个游戏中生成随机数。

## 游戏 3 – 带随机数的数学测验

在下面的这个程序中，有 5 道数学题由 10 个随机数生成。这 10 个随机数是变量 **number1-number10**。题目的答案会被计算出来，并存储在变量 **answer1-answer5** 中。这 15 个变量被称为全局变量，因为它们位于任何函数之外。这意味着它们的值可以在程序中的任何位置被任何函数访问。

函数 **startquiz()** 使用这 10 个变量 **number1-number10** 将测验写到屏幕上，并创建一个表单来接收 5 个答案，其 id 为 **num1-num5**。点击 **Check** 按钮后，这 5 个答案会被发送到函数 **guessnumber()**，并存储为变量 **guess1-guess5**。使用 5 个不同的 IF 函数，将这 5 个答案（**guess1-guess5**）与计算出的答案（**answer1-answer5**）进行核对。每当有一个正确答案，计数器就会递增。最后，打印计数器以显示正确答案的数量。末尾还有一个 **Home** 按钮，让用户可以选择用全新的题目重新开始程序。这些题目是随机生成的，这意味着用户每次都会得到不同的题目。

```html
<html>
<head><title>Math Quiz</title></head>
<link rel="stylesheet" href="samplestyle.css" />
<body>
<button class="btn" onclick="startquiz()">Start Math Quiz</button>
<script>

var number1=Math.floor(Math.random()*10)+1;
var number2=Math.floor(Math.random()*10)+1;
var number3=Math.floor(Math.random()*10)+1;
var number4=Math.floor(Math.random()*10)+1;
var number5=Math.floor(Math.random()*50)+1;
var number6=Math.floor(Math.random()*50)+1;
var number7=Math.floor(Math.random()*50)+1;
var number8=Math.floor(Math.random()*50)+1;
var number9=Math.floor(Math.random()*50)+1;
var number10=Math.floor(Math.random()*50)+1;
var answer1=number1*number2;
var answer2=number3*number4;
var answer3=number5+number6;
var answer4=number7-number8;
var answer5=number9%number10;

function startquiz()
{
document.write(number1+" * "+number2+" = ");
document.write('<input name="name" type="number" id="num1" size="20"><br>');

document.write(number3+" * "+number4+" = ");
document.write('<input name="name" type="number" id="num2" size="20"><br>');

document.write(number5+" + "+number6+" = ");
document.write('<input name="name" type="number" id="num3" size="20"><br>');

document.write(number7+" - "+number8+" = ");
document.write('<input name="name" type="number" id="num4" size="20"><br>');

document.write(number9+" % "+number10+" = ");
document.write('<input name="name" type="number" id="num5" size="20"><br>');
document.write('<link rel="stylesheet" type="text/css" href="samplestyle.css" />');
document.write('<br>');
document.write('<button class="btn a" onclick="guessnumber()">Check</button><br>');
}
```

![](img/443990a0ec620659ce8be783c0758bc6_319_0.png)

点击 **Check** 按钮后，我们得到：

![](img/443990a0ec620659ce8be783c0758bc6_319_1.png)

现在，我们知道我们所有答案都正确了。现在，让我们再次点击 **Home**。我们点击 **Start Math Quiz** 再次来到这里，再做一次测验。由于数字是随机化的，我们会得到 5 道完全不同的题目。太棒了！！

- 3 * 8 =
- 9 * 8 =
- 18 + 6 =
- 48 - 21 =
- 2 % 39. 余数 =

Check

## 练习题

- 1. 编写一个程序，生成 0 到 10 之间的两个随机数。该程序计算它们的和与积。它在屏幕上打印出和与积，并要求用户猜这两个数字。用户通过表单输入猜测值，并将其与最初的两个数字进行核对。如果他猜对了，就会收到一条祝贺消息。如果他猜错了，程序会让他知道正确答案。最后，有一个重新启动程序并再次尝试的选项。
- 2. 编写一个程序，生成 0 到 20 之间的一个随机数。它将该数字平方，并在屏幕上打印平方值。然后，它要求用户猜这个数字是什么。用户通过表单输入该数字，程序检查它是否正确。
- 3. 编写一个程序，允许用户通过表单输入 3 个数字。这 3 个数字应当是三角形的 3 条边。然后程序检查这是否是一个直角三角形。程序会让用户知道它是否是直角三角形（提示：使用勾股定理进行检查）。
