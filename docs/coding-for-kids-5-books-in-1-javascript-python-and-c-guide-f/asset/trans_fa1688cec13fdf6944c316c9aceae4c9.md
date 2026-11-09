

## 示例 #1

```html
<html>
<head><title>Print 1 to 20</title></head>
<body>

<button onclick="printtotwenty()">Print To 20</button>

<script>

function printtotwenty()
{

for (i=1;i<=20;i++)
{
    document.write(i+"<br>");
}

}

</script>

</body>
</html>
```

在这个函数中，我们创建了一个函数 `printtotwenty`，它打印从1到20的数字。标题为“打印到20”的按钮激活该函数。
在函数中有一个 for 循环：

`for (i=1; i<=20; i++)`

上面这行代码表示循环从1运行到20；每次递增1。
`document.write` 每次打印 `i` 的值。

下面是结果：

![](img/443990a0ec620659ce8be783c0758bc6_176_0.png)

点击按钮后，我们得到：

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12
- 13
- 14
- 15
- 16
- 17
- 18
- 19
- 20

按计划打印出1到20。所以，接下来，我们将做同一个程序的不同版本。不只是打印1到20；我们将让你选择要打印多少个数字。只需在文本框中输入循环长度，它就会打印出来。

## 示例 #2

```html
<html>
<head><title>JavaScript Greetings......</title></head>
<body>
<form id="form1">
Loop Length: <input type="number" id="loop" size="20"><br>
</form>

<button onclick="printttowenty()">Print To 100</button>
<button onclick="printlooplength()">Print Loop Length</button>

<script>

function printttowenty()
{

for (i=1;i<=20;i++)
{
    document.write(i+"<br>");
}

}

function printlooplength()
{
var looplength=parseInt(document.getElementById("loop").value);

var j=1;
for (j=1;j<=looplength;j++)
{
    document.write(j+"<br>");
}
}

</script>

</body>
</html>
```

现在，运行程序后，我们得到：

循环长度：50

打印到100   打印循环长度

所以，现在点击**“打印循环长度！”**

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12
- 13
- 14
- 15
- 16
- 17
- 18
- 19
- 20
- 21
- 22
- 23
- 24
- 25
- 26
- 27
- 28
- 29
- 30
- 31
- 32
- 33
- 34
- 35
- 36
- 37
- 38
- 39
- 40
- 41
- 42
- 43
- 44
- 45
- 46
- 47
- 48
- 49
- 50

所以，它打印从1到50。如果你想打印1到100，那么在文本框中输入100并点击同一个按钮。

上面的程序有一个额外的文本框和额外的按钮。文本框用于接受 `loop` 的长度，按钮链接到一个名为 `printlooplength()` 的函数，该函数打印 for 循环。变量 `looplength` 存储你在文本框中输入的值。for 循环从1运行到 `looplength`。在上面的例子中，`looplength` 是50；所以它从1运行到50。每次运行时，它使用 `document.write` 函数打印计数器。

## 示例 #3

现在，我们将用循环做一些更酷的事情。我们将根据循环长度打印一个星号图案。

```html
<html>
<head><title>JavaScript Greetings......</title></head>
<body>
<form id="form1">
Loop Length: <input type="number" id="loop" size="20"><br>
Star Loop Length: <input type="number" id="starloop" size="20"><br>
</form>

<button onclick="printtwenty()">Print To 100</button>
<button onclick="printlooplength()">Print Loop Length</button>
<button onclick="looplengthstar()">Print Star Loop</button>

<script>

function printtwenty()
{
for (i=1;i<=20;i++)
{
document.write(i+"<br>");
}
}

function printlooplength()
{
var looplength=parseInt(document.getElementById("loop").value);

var j=1;
for (i=1;i<=looplength;i++)
{
document.write(i+"<br>");
}
}
function looplengthstar()
{
var looplength=parseInt(document.getElementById("starloop").value);

for (i=1;i<=looplength;i++) {
    for (j=1;j<=i;j++)
    {
        document.write("*");
    }
    document.write("<br>");
}
}

</script>

</body>
</html>
```

输出如下：

![](img/443990a0ec620659ce8be783c0758bc6_183_0.png)

输入20，然后点击“打印星号循环”后，我们得到：

```
*
**
***
****
*****
******
*******
********
*********
**********
***********
************
*************
**************
***************
****************
*****************
******************
*******************
********************
```

上面的程序有一个额外的文本框和额外的按钮。文本框用于接受 `starloop` 的长度，按钮链接到一个名为 `looplengthstar()` 的函数，该函数打印星号循环。`Looplengthstar()` 是一个嵌套的 for 循环，这意味着它有一个循环在另一个循环内部。变量 `looplength` 存储你输入的星号循环长度的值。第一个 for 循环从1到 `looplength`。所以，在上面的例子中，第一个循环从1到20。因此，在其中，还有另一个 for 循环。第二个循环基本上在一行中打印 `*`。它打印 `*` 的次数取决于第一个循环中的计数器。例如，如果第一个循环计数器是5（i==5）；那么第二个循环打印星号5次。类似这样 `*****`。所以，每次第一个循环增加并移动到下一行时，第二个循环都会这样做。

## 练习：

你可以复制上面的示例，一旦你能够运行它们并理解代码；你可以尝试下面的一些问题。

- 1. 斐波那契数列是一组这样的数字：0,1,1,2,3,5,8,13.... 每个数字是前两个数字之和。使用 for 循环，打印序列的前20个数字。
- 2. 编写一个程序，在文本框中输入一个数字，并打印一个倒置的星号循环。
- 3. 编写一个程序，在文本框中输入一个数字，并打印其各位数字之和。

## 数组

### 什么是数组？

数组基本上是一组存储在单个名称下的项目。它们通过该名称的不同索引进行访问。例如，在JavaScript中：

`var name[5]` 是一个大小为5的数组。第一个元素是 `name[0]`，第二个元素是 `name[1]`，依此类推。

所以，如果我们想给数组赋值：

```javascript
var name[5]=["Abhi", "Bob", "Aaron", "Steve", "Mark"]
```

上面创建了一个大小为5的数组。要在JavaScript中打印第一个元素，我们这样做：

```javascript
document.write(name[0]);
```

这会打印出 Abhi，它是数组的第一个元素。

如果我们这样做：

```javascript
document.write(name[4]);
```

这会打印出 Mark，它是数组的最后一个元素。

如果我们想向数组添加一个元素，请使用 push 函数，如下所示：

```javascript
name.push("Carl");
```

```javascript
document.write(name[5]);
```

这会打印出 Carl，它是数组的新元素。

现在，让我们看几个例子：

### 示例 1

在这个例子中，我们在JavaScript中创建3个数组并给它们赋值，然后在屏幕上打印它们。

```html
<html>
<head><title>Arrays 1</title></head>
<body>

<button onclick="createarray()">Create Array</button>

<script>

function createarray()
{
var name = ["Bob","Peter","Nick"];
var age=[32,10,11];
var loc=new Array("New York","Rockford","Kansas");// 2nd way to start array
document.write(name[0]+' lives in '+loc[0]+' and age is '+age[0]+'<br>');
document.write(name[1]+' lives in '+loc[1]+' and age is '+age[1]+'<br>');
document.write(name[2]+' lives in '+loc[2]+' and age is '+age[2]+'<br>');
name.push("Steve");
age.push(20);
loc.push("Miami");
document.write(name[3]+' lives in '+loc[3]+' and age is '+age[3]+'<br>');
}

</script>

</body>
</html>
```

上面的例子中，`createarray()` 创建了3个数组 `name`、`age` 和 `loc`。每个数组分配了三个元素。它们使用 `document.write()` 打印在屏幕上。

之后，我们使用 `push` 为所有3个数组添加第四个元素，然后也将其打印出来。

