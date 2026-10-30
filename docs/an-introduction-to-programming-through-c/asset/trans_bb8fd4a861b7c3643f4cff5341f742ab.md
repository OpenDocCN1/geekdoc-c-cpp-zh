
该条件求值为 false，称为条件失败。此时，then 分支（consequent）不会执行，即 tax 保持不变。类似地，在最后一个 if 语句中，条件是 income > 800000。这里的 then 分支，即 tax = 92000 + (income - 800000) * 0.3，当且仅当 income 的值大于 800000 时执行。

在 if 语句中可以指定更复杂的条件。例如，你可能希望仅当某两个条件都为 true 时才执行某个操作。换句话说，你希望 condition1 为 true 且 condition2 为 true。因此，我们的条件可以是两个或更多条件的合取（且）。写法如下。

```
condition1 && condition2 && ... && conditionn
```

字符 && 应读作“且”（and）。在我们的第二个 if 语句中就有这样的例子。这里，仅当两个子条件 income > 180000 和 income <= 500000 都为 true 时，复合条件才为 true。换句话说，仅当 income 位于 180000（不含）和 500000（含）之间时，复合条件才为 true。只有在这种情况下，tax 才会被设置为 (income - 180000)* 0.1，即 income 超过 180000 部分的 10%。

注意，我们还可以有这样的复合条件：只要一组条件中至少有一个成立，它就成立。这样的条件称为若干（子）条件的析取，表示如下：

```
condition1 || condition2 || ... || conditionn
```

字符 || 构成逻辑或运算符。也就是说，如果 condition1 为 true，或 condition2 为 true，等等，复合条件就为 true。最后，一个条件可以是另一个条件的否定，写法如下：

```
!condition
```

其中，条件 !condition 被称为 condition 的否定。当 condition 本身为 false 时，!condition 为 true；当 condition 为 true 时，!condition 为 false。我们注意到，第二个 if 语句也可以写成：

```
if(!((income <= 180000) || (income > 500000)))
    tax = (income - 180000)* 0.1;
```

请注意，如果 income 小于等于 180000 或大于 500000，即 income 不在 180000（不含）到 500000（含）的范围内，那么 (income <= 180000) || (income > 500000) 为 true。但开头的 ! 否定了这一条件，因此只有当 income 确实位于 180000（不含）到 500000（含）的范围内时，整个条件才为 true。这与程序中第二个 if 语句测试的条件完全相同！

清楚地理解上述程序的执行方式非常重要。执行过程一如既往，自上而下。在输出消息并读取 income 的值之后，程序执行第一个 if 语句。为此，程序会检查其中的条件；如果条件为 true，则执行 then 分支。接着执行第二个 if 语句。因此每个 if 语句都会被执行；这些条件被设计成

![](img/c7233aedab7e4c7cad32a7615b6a4783_94_0.png)

图 6.2：第一个所得税程序的流程图

使得只有一个 if 语句中的条件会求值为 true，因此只会执行一条 then 分支语句。也许整个程序的流程图（图 6.2）能更清楚地展示控制流的走向。注意，一旦我们发现某个条件为 true，例如 income 至多为 180000，我们就知道其他条件不可能为 true。因此自然会提出一个问题：为什么我们还要检查它们呢？

下一节将要讨论的更一般的 if 语句可以让你避免这些不必要的检查。但在讨论它之前，我们先讨论块的概念。

## 6.2 块

在上面讨论的 if 语句中，then 分支应是一条单独的语句。一般来说，如果某个条件成立，我们可能想执行多条语句，而不仅仅是一条。块结构在这种情况下可以帮到我们。

如前所述，块就是用花括号 { 和 } 组合在一起的一组语句。通过把语句放入块中，我们将它们变成了一条复合语句。块可以放在任何需要单条 C++ 语句的位置，例如作为 if 语句的 then 分支（consequent）部分。例如，假设我们希望当 income 超过 80 万时打印消息 “This person is in the highest tax bracket.”，同时还要计算税额，那么我们可以将程序中的第四个 if 语句替换为下面的代码。

```
if (income > 800000){
    tax = 92000+(income - 800000)* 0.3;
    cout << "This person is in the highest tax bracket." << endl;
}
```

你已经在 repeat 语句中使用过块。现在请注意，repeat 语句的一般形式是：

```
repeat (count) action
```

其中 action 可以是任何语句，包括块。因此我们可以写

```
repeat (10) cout << "Test." << endl;
```

这将导致消息 “Test.” 被打印 10 次。

## 6.3 if 语句的其他形式

if-else 语句具有以下形式。

```
if (condition) consequent
else alternate
```

![](img/c7233aedab7e4c7cad32a7615b6a4783_97_0.png)

图 6.4：最一般的 if，包含 3 个条件

```
tax = (income - 180000)* 0.1;
else if(income <= 800000)        // new third if
tax = 32000+(income - 500000)* 0.2;
else
tax = 92000+(income - 800000)* 0.3;

cout << "Tax is: " << tax << endl;
}
```

请记住，char 数据实际上是数值，因此使用运算符 == 来对它进行比较是完全可行的。这个程序会执行 100 条用户命令来移动海龟，然后停止。试试吧！

### 6.4.1 画布上的“按钮”

我们可以使用第 5.3 节的 Rectangle 形状在画布上构建“按钮”。通过点击这些按钮可以控制海龟。这又提供了一种海龟控制方式。

```
main_program{
    initCanvas();

    const float bFx=150,bFy=100, bLx=400,bLy=100, bWidth=150,bHeight=50;
    Rectangle buttonF(bFx,bFy,bWidth,bHeight), buttonL(bLx,bLy,bWidth,bHeight);

    Text tF(bFx,bFy,"Forward"), tL(bLx,bLy,"Left Turn");
    Turtle t;

    repeat(100){
        int clickPos = getClick();
        int cx = clickPos/65536;
        int cy = clickPos % 65536;

        if(bFx-bWidth/2<= cx && cx<= bFx+bWidth/2 &&
            bFy-bHeight/2 <= cy && cy <= bFy+bHeight/2) t.forward(100);

        if(bLx-bWidth/2<= cx && cx<= bLx+bWidth/2 &&
            bLy-bHeight/2 <= cy && cy <= bLy+bHeight/2) t.left(10);
    }
}
```

程序首先在屏幕上绘制矩形。请注意，我们没有直接写数字来给出按钮的坐标信息，而是先创建了 bFx、bFy 等具有特定值的名称，然后在创建按钮时使用这些名称。使用这样的名称很方便：如果以后想调整按钮布局，只需改变某个名称的值。如果没有名称，你就需要在数字出现的每个地方都进行修改。在当前例子中，如果想改变矩形的宽度，只需给 bWidth 赋一个不同的值，而不必操心宽度值需要在哪些地方修改。

接下来，将文本放入矩形中。然后进入一个循环。在循环内，我们等待用户点击。我们要检查点击是否位于这两个矩形之一内部。这是通过循环中的两个 if 语句完成的。每次检查包含两个部分：我们必须检查点击的 x 坐标是否位于矩形的左边缘和右边缘之间，即左边缘
