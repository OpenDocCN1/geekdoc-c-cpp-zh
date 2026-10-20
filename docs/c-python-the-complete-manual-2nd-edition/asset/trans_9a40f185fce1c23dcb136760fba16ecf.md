

# 第5步

你还可以使用一个运算符来查看除法后的余数。例如：

```
10/3
```

将显示 3.333333333，当然这是 3.3 循环。如果你现在输入：

```
10%3
```

这将显示 1，即 10 除以 3 后的余数。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_30_0.png)

# 第6步

接下来是幂运算符，说得专业一点就是求幂。要计算某个数的幂，你可以在键盘上使用双乘号或双星号：

```
2**3
10**10
```

本质上，这就是 2x2x2，不过我们相信你已经掌握了数学运算符的基础知识。这就是在 Python 中的运算方法。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_30_1.png)

# 第7步

数字和表达式远不止这些。Python 内置了大量函数，用于处理数字集合、绝对值、复数以及大量数学表达式和毕达哥拉斯式的绕口难题。例如，要将数字转换为二进制，可以使用：

```
bin(3)
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_30_2.png)

# 第8步

它将以 '0b11' 的形式显示，即将整数转换为二进制，并在前面加上前缀 0b。如果你想去掉 0b 前缀，可以使用：

```
format(3, 'b')
```

Format 命令会将一个值（即数字 3）转换为由格式规范（即 'b' 部分）控制的格式化表示。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_30_3.png)

# 第9步

布尔表达式是一种逻辑语句，其结果要么为真，要么为假。我们可以用它们来比较数据，并测试数据是否相等、小于或大于。请在一个新文件中尝试以下代码：

```
a = 6
b = 7
print(1, a == 6)
print(2, a == 7)
print(3, a == 6 and b == 7)
print(4, a == 7 and b == 7)
print(5, not a == 7 and b == 7)
print(6, a == 7 or b == 7)
print(7, a == 7 or b == 6)
print(8, not (a == 7 and b == 6))
print(9, not a == 7 and b == 6)
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_30_4.png)

# 第10步

执行第9步中的代码，你会看到一系列 True 或 False 语句，这取决于两个定义值（6 和 7）的结果。这是你所了解内容的延伸，也是编程中的一个重要部分。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_30_5.png)

# 使用注释

在编写代码时，代码的流程、每个变量的作用、整个程序将如何运行等等，都在你的脑海中。另一个程序员可以逐行阅读代码，但随着时间的推移，代码会变得难以阅读。

# #注释！

程序员使用一种方法通过注释某些部分来保持代码的可读性。例如，如果使用了一个变量，程序员会注释该变量的用途。这只是良好的做法。

步骤1 首先，创建一个新的 IDLE 编辑器实例（文件 > 新建文件），并创建一个简单的变量和打印命令：

```
a=10
print("The value of A is,", a)
```

保存文件并执行代码。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_31_0.png)

步骤3 重新保存代码并执行。你可以看到，尽管添加了额外的行，IDLE Shell 中的输出仍然与之前相同。简单来说，井号（#）表示程序员可以插入的一行文本，用于告知他们自己和他人代码中发生的事情，而用户不会察觉。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_31_1.png)

步骤2 运行代码将返回一行：The value of A is, 10 到 IDLE Shell 窗口中，这正是我们所期望的。现在，添加一些你在代码中通常会看到的注释类型：

```
# Set the start value of A to 10
a=10
# Print the current value of A
print("The value of A is,", a)
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_31_2.png)

步骤4 假设我们创建的变量 A 是游戏中的生命数。每次玩家死亡，该值就减 1。程序员可以插入一段类似这样的代码：

```
a=a-1
print("You’ve just lost a life!")
print("You now have", a, "lives left!")
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_31_3.png)

# 第5步

虽然我们知道变量 A 是生命数，而且玩家刚刚失去一条命，但一个普通的浏览者或检查代码的人可能并不知道。想象一下，如果代码有两万行，而不仅仅是我们的七行，你就会明白注释有多有用了。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_32_0.png)

# 第6步

本质上，带有注释的新代码可能如下所示：

```
# Set the start value of A to 10
a=10
# Print the current value of A
print("The value of A is,", a)
# Player lost a life!
a=a-1
# Inform player, and display current value of A (lives)
print("You’ve just lost a life!")
print("You now have", a, "lives left!")
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_32_1.png)

# 第7步

你可以用不同的方式使用注释。例如，块注释是一大段文本，详细说明代码中发生的事情，比如告诉代码阅读者你打算使用哪些变量：

```
# This is the best game ever, and has been developed by a crack squad of Python experts
# who haven’t slept or washed in weeks. Despite being very smelly, the code at least
# works really well.
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_32_2.png)

# 第8步

行内注释是跟随一段代码的注释。以上面的示例为例，我们不把注释放在单独一行，而是可以这样写：

```
a=10 # Set the start value of A to 10
print("The value of A is,", a) # Print the current value of A
a=a-1 # Player lost a life!
print("You’ve just lost a life!")
print("You now have", a, "lives left!") # Inform player, and display current value of A (lives)
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_32_3.png)

# 第9步

注释符号即井号，也可以用来注释掉程序中你不想执行的代码段。例如，如果你想删除第一条 print 语句，可以这样做：

```
# print("The value of A is,", a)
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_32_4.png)

# 第10步

你还可以使用三个单引号来注释掉一个块注释或一段多行注释。将它们放在你想注释的内容前后，即可生效：

```
'''
This is the best game ever, and has been developed by a crack squad of Python experts who haven’t slept or washed in weeks. Despite being very smelly, the code at least works really well.
'''
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_32_5.png)

# 使用变量

我们已经在 Python 代码中看到了一些变量的示例，但还是值得仔细了解一下它们的运作方式，以及 Python 如何创建变量并为其赋值。

# 各种变量

在本教程中，你将使用 Python 3 IDLE Shell。如果你还没有打开，请打开 Python 3，或者关闭之前的 IDLE Shell 以清除任何旧代码。

步骤1 在某些编程语言中，你需要使用美元符号来表示字符串，字符串是由多个字符组成的变量，例如人的姓名。在 Python 中则没有必要。例如，在 Shell 中输入：name="David Hayward"（或者使用你自己的名字，除非你也叫 David Hayward）。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_33_0.png)

步骤2 你可以通过输入 type() 命令，并将变量名放在括号中来检查当前使用的变量类型。在我们的示例中，即：type(name)。添加一个新的字符串变量：title="Descended from Vikings"。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_33_1.png)

步骤3 你之前已经看到，变量可以通过在变量名之间使用加号来拼接。在我们的示例中，可以使用：print(name + ": " + title)。引号之间的中间部分允许我们添加一个冒号和一个空格，因为变量连接时没有空格，所以我们需要手动添加。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_33_2.png)

步骤4 你也可以在另一个变量中组合变量。例如，要将 name 和 title 这两个变量组合成一个新变量，我们使用：character=name + ": " + title

```
character=name + ": " + title
```

然后输出新变量的内容如下：

```
print(character)
```

数字存储为不同的变量：

```
age=44
```

```
Type(age)
```

正如我们所知，它们是整数。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_33_3.png)

