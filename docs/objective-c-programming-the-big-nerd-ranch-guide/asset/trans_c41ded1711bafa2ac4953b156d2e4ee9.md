

*布尔*（boolean）变量可以取真或假。从历史上看，C 程序员一直使用 `int` 来存储布尔值。Objective-C 程序员通常使用类型 `BOOL` 来表示布尔变量，因此我们在这里也使用它。（`BOOL` 只是整数类型的别名。）要在 C 函数中使用 `BOOL`，你需要包含相应的头文件：

```
#include <objc/objc.h>
```

关于语法的说明：如果跟随条件表达式的代码只包含一条语句，那么大括号是可选的。因此，以下代码与前面的示例等效。

```
BOOL isNotLegal = !((truckWeight > 0.0) && (truckWeight < 40000.0));
if (isNotLegal)
    printf("Truck weight is not within legal range.\n");
```

然而，如果代码包含不止一条语句，大括号是必需的。

```
BOOL isNotLegal = !((truckWeight > 0.0) && (truckWeight < 40000.0));
if (isNotLegal) {
    printf("Truck weight is not within legal range.\n");
    printf("Impound truck.\n");
}
```

为什么？想象一下如果你去掉了大括号会怎样。

```
BOOL isNotLegal = !((truckWeight > 0.0) && (truckWeight < 40000.0));
if (isNotLegal)
    printf("Truck weight is not within legal range.\n");
    printf("Impound truck.\n");
```

这段代码会让你非常不讨卡车司机的喜欢。在这种情况下，无论卡车重量多少，所有卡车都会被扣押。当编译器在条件表达式后找不到大括号时，只有下一条语句被视为 `if` 结构的一部分。因此，第二条语句总是会被执行。（那第二条语句的缩进呢？虽然缩进对于人类阅读代码非常有帮助，但对编译器来说毫无意义。）

## else if

如果有两种以上的可能性怎么办？你可以使用 `else if` 逐一进行测试。例如，想象一辆卡车属于以下三种重量类别之一：漂浮、轻量级和重量级。

```
if (truckWeight <= 0) {
    printf("A floating truck\n");
} else if (truckWeight < 40000.0) {
    printf("A light truck\n");
} else {
    printf("A heavy truck\n");
}
```

你可以拥有任意数量的 `else if` 子句。它们将按照出现的顺序逐一测试，直到其中某一个评估为真。这部分“按出现的顺序测试”非常重要。请务必按照正确的顺序排列你的条件，以避免出现假阳性。例如，如果你交换了上述示例中的前两个测试，你永远不会找到漂浮的卡车，因为漂浮的卡车也是轻量级卡车。最后的 `else` 子句是可选的，但当你想要捕获所有不符合之前条件的情况时，它很有用。

## 供好奇者参考：条件（三目）运算符

使用 if 和 else 来设置实例变量的值并不罕见。例如，你可能会有如下代码：

```
int minutesPerPound;
if (isBoneless)
    minutesPerPound = 15;
else
    minutesPerPound = 20;
```

只要你有一种场景，根据条件将值分配给变量，这就是*条件运算符*（即 ?）的一个候选场景。（你有时也会看到它被称为*三目运算符*。）

```
int minutesPerPound = isBoneless ? 15 : 20;
```

这一行代码与前面的示例等效。你不再编写 if 和 else，而是编写一个赋值语句。? 之前的部分是条件表达式。? 之后的值是条件表达式评估为真或假时的备选值。

如果这种写法让你觉得奇怪，继续直接使用 if 和 else 也是完全没问题的。我猜想，随着时间推移，你会接受三目运算符作为进行条件值分配的一种简洁方式。更重要的是，你会看到其他程序员使用它，理解它出现的含义会很有用！

## 挑战

考虑以下代码片段：

```
int i = 20;
int j = 25;

int k = ( i > j ) ? 10 : 5;

if ( 5 < j - k ) { // first expression
    printf("The first expression is true.");
} else if ( j > i ) { // second expression
    printf("The second expression is true.");
} else {
    printf("Neither expression is true.");
}
```

控制台将输出什么？

## 5 函数

在第 3 章中，我引入了变量的概念：与一块数据相关联的名称。函数则是与一段代码相关联的名称。你可以向函数传递信息。你可以让函数执行代码。你可以让函数向返回信息。

函数是编程的基础，所以本章内容很多——三个新项目、一个新工具以及许多新思想。让我们从一个演示函数用途的练习开始。

### 我什么时候应该使用函数？

假设你正在编写一个程序，向完成 Big Nerd Ranch 课程的学生表示祝贺。在担心如何从数据库获取学生名单或如何在华丽的 Big Nerd Ranch 纸张上打印证书之前，你想先实验一下将印在证书上的消息。

为了进行这个实验，创建一个新的项目：一个名为 ClassCertificates 的 C Command Line Tool。你在编写这个程序时的第一想法可能是：

```
int main (int argc, const char * argv[]) 
{
    printf("Mark has done as much Cocoa Programming as I could fit into 5 days\n");
    printf("Bo has done as much Objective-C Programming as I could fit into 2 days\n");
    printf("Mike has done as much Python Programming as I could fit into 5 days\n");
    printf("Ted has done as much 105 Programming as I could fit into 5 days\n");

    return 0;
}
```

输入所有这些内容这件事让你感到烦恼吗？它是否显得令人恼火地重复？如果是这样，你就具备了优秀程序员的潜质。当你发现自己正在重复性质非常相似的工作（在这种情况下，是 `printf` 语句中的文字）时，你就应该开始思考将函数作为完成相同任务的更好方式。

### 我如何编写和使用函数？

既然你已经意识到你需要一个函数，那么你需要编写一个。在你的 ClassCertificates 项目中打开 `main.c`，并在 `main` 函数之前添加一个新函数。将这个函数命名为 `congratulateStudent`。

#### 第 5 章 函数

```
#include <stdio.h>

void congratulateStudent(char *student, char *course, int numDays)
{
    printf("%s has done as much %s Programming as I could fit into %d days.\n",
           student, course, numDays);
}
```

（想知道 %s 和 %d 是什么意思吗？先别急，我们将在下一章讨论它们。）

现在编辑 main 函数以使用你的新函数：

```
int main(int argc, const char *argv[])
{
    congratulateStudent("Mark", "Cocoa", 5);
    congratulateStudent("Bo", "Objective-C", 2);
    congratulateStudent("Mike", "Python", 5);
    congratulateStudent("Ted", "iOS", 5);

    return 0;
}
```

构建并运行程序。你很可能得到一个标有黄色小三角形内带感叹号的*警告*。Xcode 中的警告不会阻止你的程序运行；它只是引起你对可能问题的注意。警告文本位于代码的右侧。这个警告类似于 `No previous prototype for function 'congratulateStudent'`。暂时忽略这个警告，我们将在本节末尾回头讨论它。

在日志导航器中找到你的输出。它应该与你手动输入所有内容所看到的结果完全相同。

```
Mark has done as much Cocoa Programming as I could fit into 5 days.
Bo has done as much Objective-C Programming as I could fit into 2 days.
Mike has done as much Python Programming as I could fit into 5 days.
Ted has done as much iOS Programming as I could fit into 5 days.
```

想想你在这里做了什么。你注意到了一种重复的模式。你将问题的所有共同特征（重复的文本）移入了一个单独的函数。这留下了差异（学生姓名、课程名称、天数数量）。你通过向函数添加三个*参数*来处理这些差异。让我们再看一下命名函数的这一行。

```
void congratulateStudent(char *student, char *course, int numDays)
```

每个参数都有两部分：参数所代表的数据类型和参数的名称。参数用逗号分隔，放在函数名称右侧的括号内。

那函数名称左侧的 `void` 是什么？它是从函数返回的信息类型。当你没有要返回的信息时，使用关键字 `void`。我们将在本章后面详细讨论返回。

你也在 **main** 中使用了，或者说*调用*了，你的新函数。当你调用 **congratulateStudent** 时，你传递了值。传递给函数的值被称为*实参*。实参的值随后被分配给对应的参数名称。该参数名称可以在函数内部作为包含传入值的变量使用。

