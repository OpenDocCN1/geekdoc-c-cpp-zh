
```java
class WhileDemo{
    public static void main(String args[]) {
        int i=1; // 设置值为 1
        while(i<=20) {
            System.out.println(i);// 显示 i
            i+=2; // 值加 2
        }
    }
}
```

在列表 6 中，使用 `while` 循环显示了奇数。首先，变量 `i` 被设置为 1。为了显示奇数，每次迭代 `i` 都会增加 2。当评估变为假时，由于 `i` 的值超过了 20，循环终止。图 6 显示了输出：

![](img/d3faa73f55d3d314bb5bfb277886900d_75_0.png)

▲ 图 6：WhileDemo 程序的输出

### do-while 循环

`do-while` 循环的工作方式类似于 `while` 循环，只要条件为真，就会执行一组语句。如果条件变为假，执行流将离开 `do-while` 循环。让我们在下一节中查看 `do-while` 循环。

```java
{
    statements;
}
while(condition);
```

## 列表 7：使用 do-while 循环语句

```java
class DowhileDemo {
    public static void main(String args[]) {
        do {
            int i=2;// 将值设置为 2
            System.out.println(i); // 显示 i
            i=2; // 将值加 2
        } while(i<=20);
    }
}
```

在列表 7 中，使用 `do-while` 循环以与 `while` 循环相同的方式了前十个偶数。然而，区别在于它们的实现方式。在列表 7 中，`i` 在评估条件表达式之前就会显示，而 `while` 循环是先检查条件，然后再执行语句。

首先，将 `i` 设置为 2。为了显示偶数，在每次迭代中 `i` 都加 2。当评估结果为假时，循环终止，即 `i` 的值超过 20 时，如图 7 所示：

![](img/d3faa73f55d3d314bb5bfb277886900d_76_0.png)

在图 7 中，使用 `do-while` 循环显示到 20 的偶数。在学习了 `while` 和 `do-while` 循环的基础区别后，让我们讨论另一种类型的迭代，称为 `for` 循环。

## 使用 for 循环

`for` 循环也类似于 `while` 循环，但语法上更紧凑。`for` 循环只要条件为真，就会执行一组语句。以下是 `for` 循环的通用语法：

```
for (初始化; 条件; 递增/递减)
    语句;
```

在上述语法中，`初始化` 用于设置计数器的初始值以控制迭代。为了实现此目的，可以声明一个变量。在循环的每个阶段都会评估一个布尔条件，以检查循环是否继续。如果条件评估为真，循环将继续；否则，它将终止。列表显示了你如何在程序中使用 `for` 循环（你可以在 Code/Chapter3 文件夹中找到 `ForDemo.java` 文件）：

- 使用 `for` 循环语句

```java
class ForDemo
{
    public static void main(String args[])
    {
        for(i=1;i<=20;i=i+2)
        {
            System.out.println(i);
        }
    }
}
```

通过循环的帮助显示了前十个奇数。首先，变量 `i` 设置为 1。为了显示奇数，`i` 在每次迭代中都加 2。一旦 `i` 的值超过 20，迭代即为假，循环终止，如图 8 所示：

![](img/d3faa73f55d3d314bb5bfb277886900d_77_0.png)

> ▲ 图 8：ForDemo 程序的输出

在图中，通过循环的帮助显示了到 20 的奇数。我们将讨论的下一种迭代语句是 `for-each` 循环。该循环为集合中的每个元素执行语句。让我们在下一节讨论 `for-each` 循环。

- 使用 for-each 循环

`for-each` 循环设计的背后理念是处理与集合相关的所有元素。集合通过一组对象来表示。数组是集合的一个示例，因为它存储一组对象，如整数值或字符串。同样，`java.util` 包中的类也是为了处理一组对象而开发的。`for-each` 循环为集合中的每个元素重复执行一组语句。以下是使用 `for-each` 循环的通用语法：

## 控制语句

```
for(var:collection)
{
    Statements;
}
```

在上述语法中，`var` 逐个代表集合中的每个元素。例如，如果有一个 5 个元素的集合，此循环将执行 5 次，`var` 将逐个代表这些元素。让我们通过列表 9 中的示例来理解 `for-each` 循环的使用（你可以在 Code(Chapter3) 文件夹中找到 `ForEachDemo.java` 文件）：

- 列表 9：使用 for-each 循环

```java
class ForEachDemo
{
    public static void main(String[] args)
    {
        int arr[]{1,3,5,7,9,11,13,15,17,19];//声明一个包含10个元素的数组
        System.out.println("前10个奇数如下:");
        for(int i:arr) // 使用 for 循环从数组中检索元素
            System.out.println(i); // i 代表数组的每个元素
        }
    }
}
```

在列表 9 中，使用 `for-each` 循环显示数组的每个元素。在列表 9 中，有一个包含 10 个元素的数组类型集合。`for-each` 循环将执行 10 次，并代表这些元素，从而为这些每个元素执行语句，如图 9 所示：

![](img/d3faa73f55d3d314bb5bfb277886900d_78_0.png)

▲ 图 9：ForEachDemo 程序的输出

在图 9 中，使用 `for-each` 循环显示数组中的数字。除了程序中的单层循环，你还可以在程序中使用嵌套循环。让我们在下一节讨论嵌套循环。

- 使用嵌套循环

在 Java 中，可以嵌套条件语句以及迭代语句。嵌套语句可以是另一个条件语句中的条件语句（嵌套 `if` 语句），也可以包含其他迭代语句的迭代语句（嵌套 `for` 循环、`while` 循环或 `do-while` 循环）。

嵌套 `for` 循环是在循环内部的 `for` 循环。在嵌套循环的情况下，执行从外部 `for` 循环开始，控制传递到内部 `for` 循环。内部循环继续执行直到条件评估为真。一旦循环完成，执行将传递给外部循环进行下一次迭代，并执行直到评估返回真。让我们通过列表 10 所示的示例来理解嵌套循环的使用（你可以在 CD 中的 CodeChapter3 找到 `NestedLoopDemo.java` 文件）：

- 列表 10：使用嵌套循环语句

```java
class NestedLoopDemo {
    public static void main(String[] args) {
        int num1,num2;
        for(num2 = 0; num2 <= 3; num2++) {
            for(num1 = 0; num1 <= 2; num1++) {
                System.out.println(num2 + " " + num1);
            }
        }
    }
}
```

*(注：由于原始文本在之后出现了大量重复且逻辑混乱的描述，翻译已在逻辑最清晰的结束处停止。)*

# 68 第3章

```java
System.out.println(i);

}

}
```

在列表 11 中，展示了一个显示到无限大偶数的无限循环。为了避免无限情况，在条件语句中使用了一个 `break` 语句，该条件规定：如果 `i` 的值超过 10，则控制将跳出 `while` 循环。如果控制退出循环，将显示前 5 个数字，如图 11 所示：

```
Command Prompt
>Code\Chapter3\BreakDemo.Java
>Code\Chapter3\BreakDemo
5
10
>Code\Chapter3>
```

▲ 图 11：BreakDemo 程序的输出

在图 11 中，由于执行了 `break` 语句，显示了到 10 的偶数并且循环跳出了无限循环。

`break` 语句也可以作为 `goto` 语句的替代方案。Java 不直接支持 `goto` 语句；间接上可以通过标签的 `break` 语句来实现相同的功能。

不带标签的 `break` 语句有助于结束最近的嵌套 `do` 语句或 `switch` 语句的执行。让我们通过列表 12 示例来理解如何使用带标签的 `break` 语句（您可以在光盘 `Code\Chapter3` 文件夹中找到 `LabelBreakDemo.java` 程序）：

- 列表 12：使用标签 break 语句

```java
class LabelBreakDemo {
    public static void main(String[] args) {
        int i = 1;
        breaking:while(true) //循环将无限执行
        {
            if (i > 10)
                break breaking;
            
            System.out.println(i);
            i++;
        }
    }
}
```

在列表 12 中，展示了一个显示到无限大奇数的无限循环。为了避免这种情况，在条件语句中使用带标签的 `break` 语句，该条件规定：如果 `i` 的值超过 10，则控制将跳出 `while` 循环，只会显示前 5 个奇数，如图 12 所示。

# 控制语句的使用 69

![](img/d3faa73f55d3d314bb5bfb277886900d_82_0.png)

**图 12：LabelBreakDemo 程序的输出

在图 12 中，由于执行了 *break* 语句，*while* 循环终止，仅显示了到 10 的奇数。让我们在下一节中讨论 `continue` 语句。

## 使用 continue 语句

`continue` 语句有助于终止当前迭代，从而开始下一次迭代。当在没有标签的情况下使用 *continue* 时，它会启动最内层循环的新迭代。当它配合标签（代表包含它的循环的名称）使用时，它会启动带标签循环的新迭代。让我们通过列表 13 示例来理解 *continue* 语句的使用（查看光盘 *Code\Chapter3* 文件夹中的 *ContinueDemo.java* 文件）：

- 列表 13：使用 continue 语句

```java
class ContinueDemo{
    public static void main(String[] args) {
        for (int i=1;i<=20;i=i+2)
        {
            if (i == 12) // 如果 i 变为 12，则执行 continue 语句
            {
                continue;
            }
            System.out.println(i);
        }
    }
}
```

在列表 13 中，结果显示了除了 12 以外的偶数。这是得益于 *if* 条件的，当变量 *i* 的值变为 12 时会执行该条件。在列表 13 中，在 *i* 的值变为 12 之前，成功显示了偶数。当 *i* 的值变为 12 时，执行控制退出当前循环并返回 *for* 循环。下一次迭代开始显示剩余的偶数，直到 *i* 的值超过 20，如图 13 所示：

# 第3章

![](img/d3faa73f55d3d314bb5bfb277886900d_83_0.png)

图 13：ContinueDemo 程序的输出

在图 13 中，由于执行了 `continue` 语句，12 没有显示，循环的下一次迭代开始。

以上是关于 `continue` 语句的所有内容。现在让我们讨论 `return` 语句中提供的另一种跳转语句。

- * 使用 return 语句

`return` 语句导致执行控制返回方法的调用者。让我们通过列表 14 示例来理解 `return` 语句的使用（您可以在光盘 `CD\Chapter3` 文件夹中找到 `ReturnDemo.java` 文件）：

- 列表 14：使用 return 语句

```java
class ReturnDemo{
    public static void main(String args[])
    {
        int input=-Integer.parseInt(args[0]);
        int result=square(input);
        System.out.println(result);
    }
    public static int square(int x)
    {
        return x*x;
    }
}
```

在列表 14 中，`square()` 方法接受一个整数值，计算其平方值，并将该值返回给 `main()` 方法（即它的调用方法）。在 `main()` 方法中，我们得到了列表 14 的输出：![](img/d3faa73f55d3d314bb5bfb277886900d_82_0.png)

图 14：ReturnDemo 程序的输出

## 总结

在本章中，你学习了 break、continue 和 return 语句。

从以下输出中选择上述代码段的输出结果。

- a. Grade A

b. Grade A

Grade B

- c. Grade A

Grade B

Fail

- d. Fail

Ans. 选项 c 正确。

Q8. 下列哪项是 while 循环的正确声明？

- a.

```java
while(int j)
{
j++;
System.out.println(j);
}
```

- b.

```java
int j=1;
while(j<5)
{
System.out.println(j);
j++;
}
```

- c.

```java
while(j)
{
j++;
System.out.println(j);
}
```

- d.

```java
int j=10;
while(j>=1)
{
System.out.println(j);
j--;
}
```

Ans. 选项 b 和 d 正确。

Q9. 下列哪项是 do-while 循环的正确语法？

- a.

```java
do
{
<statements>
}while(condition)
```

- b.

```java
do {
  <statements>
}while(condition);
```

- c.

```java
do {
  <statements>
  while(condition);
}
```

- d.

```java
while(condition) {
  <statements>
}
```

Ans. 选项 b 正确。

Q10. 下列哪个语句用作 goto 语句的替代？

- a. continue

- b. Labeled break

- c. default

- d. return

Ans. 选项 b 正确。

## 短答题

Q1. while 循环和 do-while 循环的主要区别是什么？

Ans. while 循环和 do-while 循环都会重复执行代码块，直到指定的条件变为假。while 和 do-while 循环的基本区别在于：在 while 循环中，指定的条件在开始时检查；而在 do-while 循环中，指定的条件在执行执行语句之后检查。在 while 循环中，循环内部的代码可能一次都不执行；而在 do-while 循环中，循环至少执行一次，因为条件是在循环结束时验证的。

Q2. 简要解释 for-each 循环。

Ans. for-each 循环的设计基本概念是处理与集合相关的所有元素。集合通过一组对象表示。for-each 循环为集合中的每个元素重复执行一组语句。它执行的次数等于集合中元素的数量。

Q3. 列出 Java 支持的各种选择语句（Selection statements）？

Ans. 选择语句导致程序在评估条件表达式并选择待执行代码时，执行一段代码块。Java 中有多种选择语句。这些语句如下：

# 使用控制语句

- if 语句

- if-else 语句

- 多 if-else 语句

- switch 语句

Q4. 解释 if 语句和 if-else 语句之间的区别？

Ans. if 语句是一种条件结构，用于帮助评估表达式的布尔值。如果表达式返回真，则执行条件表达式后面的语句，否则不执行。if-else 语句用于在条件句返回假的情况下提供另一种备选行动方案。例如，当条件句评估结果为假时，if 句中编写的语句将被执行。

Q5. 迭代语句（iteration statements）的基本思想是什么？

Ans. 多次重复执行相同的代码被称为循环或迭代。重复语句序列的过程一直持续直到满足特定条件。当该条件为假时，迭代结束，循环完成。Java 中有很多类型的迭代语句，如 while、do-while、for 循环和 for-each 循环。在 Java 中，迭代语句被称为循环。

Q6. 简要解释 continue 语句？
