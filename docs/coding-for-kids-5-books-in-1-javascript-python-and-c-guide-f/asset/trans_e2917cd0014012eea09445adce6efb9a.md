
```html
<html>
<head><title>JavaScript Lesson 5 - Arrays</title></head>
<body>
<link rel="stylesheet" href="samplestyle.css" />

<button onclick="createarray()">Print Array</button>

<script>
function createarray()
{
  document.write('<link rel="stylesheet" type="text/css" href="samplestyle.css" />');
  document.write('<br>');
  var nm = ["Jim","Tim","Kim","Bim","Sam"];
  var age=[7,56,40,34,56];
  var state=["Florida","California","Georgia","Illinois","Nevada"];
  document.write(nm[0]+' lives in '+state[0]+' state and age is '+age[0]+'<br>');
  document.write(nm[1]+' lives in '+state[1]+' state and age is '+age[1]+'<br>');
  document.write(nm[2]+' lives in '+state[2]+' state and age is '+age[2]+'<br>');
  document.write(nm[3]+' lives in '+state[3]+' state and age is '+age[3]+'<br>');
  document.write(nm[4]+' lives in '+state[4]+' state and age is '+age[4]+'<br>');
  nm.push("Y");// Adding another index to the array
  age.push(20);
  state.push("California");
  document.write(nm[5]+' lives in '+state[5]+' state and age is '+age[5]+'<br>');
}
</script>
</body>
</html>
```

### 输出

![](img/443990a0ec620659ce8be783c0758bc6_333_0.png)

点击**打印数组**后，我们得到……

## 示例 2 – 通过表单为数组赋值

在这个示例中，我们通过 HTML 表单输入姓名、年龄和州。在 JavaScript 中，我们将表单元素赋值给变量。

通过表单输入 3 个姓名、年龄和州位置，并使用 **document.getElementById** 将它们输入到 3 个数组中。

最后使用 **document.write()** 打印数组。

```html
<html>
<head><title>JavaScript Lesson 5 - Arrays</title></head>
<body>
<link rel="stylesheet" href="samplestyle.css" />
Enter Name1 <input name="name" type="text" id="name0" size="20"><br>
Enter Age1 <input name="age" type="number" id="age0" size="20"><br>
Enter State1 <input name="state" type="text" id="state0" size="20"><br>

Enter Name2 <input name="name" type="text" id="name1" size="20"><br>
Enter Age2 <input name="age" type="number" id="age1" size="20"><br>
Enter State2 <input name="state" type="text" id="state1" size="20"><br>

Enter Name3 <input name="name" type="text" id="name2" size="20"><br>
Enter Age3 <input name="age" type="number" id="age2" size="20"><br>
Enter State3 <input name="state" type="text" id="state2" size="20"><br>
<button onclick="createarray()">Start Program</button>

<script>
function createarray()
{
var nm=[];
var age=[];
var state=[];

nm[0]=document.getElementById("name0").value;
age[0]=document.getElementById("age0").value;
state[0]=document.getElementById("state0").value;
nm[1]=document.getElementById("name1").value;
age[1]=document.getElementById("age1").value;
state[1]=document.getElementById("state1").value;
nm[2]=document.getElementById("name2").value;
age[2]=document.getElementById("age2").value;
state[2]=document.getElementById("state2").value;

document.write('<link rel="stylesheet" type="text/css" href="samplestyle.css" />');
document.write('<br>');
document.write(nm[0] + " is " +age[0]+ " years old and lives in " +state[0]+"<br>");
document.write(nm[1] + " is " +age[1]+ " years old and lives in " +state[1]+"<br>");
document.write(nm[2] + " is " +age[2]+ " years old and lives in " +state[2]+"<br>");
}
</script>
```

### 输出

- 输入姓名1：Mather
- 输入年龄1：35
- 输入州1：伊利诺伊州
- 输入姓名2：Timmy
- 输入年龄2：23
- 输入州2：佐治亚州
- 输入姓名3：Mahama
- 输入年龄3：67
- 输入州3：加利福尼亚州
- 启动程序

点击**启动程序**后，我们得到：

Mather 35 岁，住在伊利诺伊州

Timmy 23 岁，住在佐治亚州

Mahama 67 岁，住在加利福尼亚州

## 示例 3 – 猜世界各国首都

在这个程序中，我们编写一个测验，询问用户世界上某个随机国家的首都，并检查答案是否正确。

程序中有一个按钮运行 **worldquiz()** 函数。在该函数中，我们声明两个数组。一个数组包含世界上所有国家；另一个包含所有首都。

你可以从下面获取这些数组的值：

[https://drive.google.com/file/d/1VBnrlk290oVmh3Vn8Jv2EgFBL1w8vSd/view?usp=sharing](https://drive.google.com/file/d/1VBnrlk290oVmh3Vn8Jv2EgFBL1w8vSd/view?usp=sharing)

然后，我们选择 0 到 x 之间的随机数，x 是数组的长度。这个随机数从数组中随机选取一个国家。我们使用 **Math.random()** 和 **Math.floor()** 来实现。

我们使用 **prompt** 接收用户对首都的猜测。我们将用户猜测与实际首都进行比较。然后，我们向用户发送一条消息，告诉他们正确还是错误（如果错误，则附上正确首都）。

然后，用户可以通过运行 **redirect()** 函数的 **主页** 按钮重新启动程序。redirect 函数运行‘**GuessWorldCapitals.html**’，这是文件名。代码和输出如下所示。

```html
<html>
<head><title>Guess World Capitals</title>
<link rel="stylesheet" href="styles.css" />
</head>
<body>
<button class="btn a" onclick="worldquiz()">Start Quiz</button>
<script>
function worldquiz()
{
var countries = ["Afghanistan","Albania","Algeria","Andorra","Angola","Antigua and Barbuda","Argentina","Armenia",
var capitals = ["Kabul","Tirana (Tirane)","Algiers","Andorra la Vella","Luanda","Saint John's","Buenos Aires","Yer
var randomcountrynumber = Math.floor(Math.random() * countries.length);
var chosencountry = countries[randomcountrynumber];
var chosencapital = capitals[randomcountrynumber];
var guess = prompt("What is the capital of "+chosencountry+" ?");
if (guess.toUpperCase()==chosencapital.toUpperCase())
{
    document.write("<p>Congratulations. You are correct.</p>");
}
else
{
    document.write("<p>Wrong. The capital is "+chosencapital+"</p>");
}
document.write('<link rel="stylesheet" type="text/css" href="styles.css" />');
document.write('<br>');
document.write('<button onclick="redirect()">Home</button>');
}
function redirect()
{
window.location.replace("GuessWorldCapitals.html");
}
</script>
</body>
</html>
```

### 输出 #1

![](img/443990a0ec620659ce8be783c0758bc6_338_0.png)

点击开始测验

![](img/443990a0ec620659ce8be783c0758bc6_339_0.png)

![](img/443990a0ec620659ce8be783c0758bc6_339_1.png)

### 输出 #2

![](img/443990a0ec620659ce8be783c0758bc6_339_2.png)

错误。首都是亚的斯亚贝巴

[主页]

## 示例 4 – 随机笑话

这个程序打印从笑话列表中随机选取的一个笑话。这个按钮运行 **writejoke()** 函数。在该函数中，我们声明一个包含所有笑话的数组。你可以从下面获取所有值：

[https://drive.google.com/file/d/1xDN9dt2Gvj-mdPmi5ATCnP1tv0ZtZ5/view?usp=sharing](https://drive.google.com/file/d/1xDN9dt2Gvj-mdPmi5ATCnP1tv0ZtZ5/view?usp=sharing)

然后，我们选择 0 到 x 之间的随机数，x 是数组的长度。这个随机数随机选取一个笑话。我们使用 **Math.random()** 和 **Math.floor()** 来实现。

然后，我们使用 **document.write()** 函数打印出笑话。

然后，用户可以通过运行 **redirect()** 函数的 **主页** 按钮重新启动程序。

```html
<html>
<head><title>Random Duck Joke</title>
<link rel="stylesheet" href="samplestyle.css" />
</head>
<body>
<button class="btn a" onclick="writejoke()">Get A Duck Joke</button>
<script>
var duckjokes = [
"Why did the duck cross the road? It was the chicken's day off",
"Why did the duck detective get promoted? He quacked the case",
"Why did the tiger cross the road? To eat the duck and then her",
"What did the duck do when he saw the clown? He started quacking up",
"Why is the duck always standing straight? To hide his butt-quack",
"Which is the heaviest bird? The crane",
"Why did the duck go to prison? He became a quackpot.",
"Why did the bee do his own haircuts? He did buzzcuts",
"Why did the duck lose the race? Because he was a lame duck",
"What happened after the duck got injured? He went to a ducktor!",
"Where did the duck eat breakfast? Quacker barrel",
"Why did the hen keep its nest warm? Because it was eggstremely cold outside",
"Why did the duck not like the soup? Because it had no quackers!",
"Why were the two ducks always together? They were stuck together with duck-tape",
"Why do swans avoid the stock market? Because they're afraid of the black-swan",
"How do ducks know if it's about to rain? Because they checked the feather-forecast",
"What did the duck do on July 4th? It burst quackers",
]
function writejoke()
{
var chosenjoke = duckjokes[Math.floor(Math.random() * duckjokes.length)];

document.write(chosenjoke);
document.write('<link rel="stylesheet" type="text/css" href="samplestyle.css" />');
document.write('<br>');
document.write('<button onclick="redirect()">Home</button>');
}
function redirect()
{
window.location.replace("RandomJoke.html");
}
</script>
</body>
</html>
```
