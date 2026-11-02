
标准计算机键盘。）因为 gumballsPerKid 只有九，所以 gumballsPerKid >= 10 为假。因此 eachKidGetsTen 变为假。哎呀！孩子们会把房子拆掉的！（在他们动手之前，先看看图 8-10。）

图 8-10：为 eachKidGetsTen 变量赋值。

![](img/6d9dcff12e52b997f3ad31445b712549_180_0.png)

## 表达式和条件

在清单 8-4 中，代码 gumballsPerKid >= 10 是一个表达式。表达式的值取决于存储在变量 gumballsPerKid 中的值。在糟糕的日子里，gumballsPerKid >= 10 的值为 false。因此变量 eachKidGetsTen 被赋值为 false。

值只能是 true 或 false 的像 gumballsPerKid >= 10 这样的表达式，有时被称为条件。

![](img/6d9dcff12e52b997f3ad31445b712549_180_1.png)

true 和 false 之类的值看起来似乎包含字符，但实际上并不包含。在内部，Java 虚拟机不会用字母 t-r-u-e 或 f-a-l-s-e 来存储布尔值。相反，JVM 存储的是代码，例如 false 为 0，true 为 1。当计算机显示一个布尔值（如 System.out.println(eachKidGetsTen) 中所示）时，Java 虚拟机会将像 0 这样的代码转换为五个字母的单词 false。

## 比较数字；比较字符

在清单 8-4 中，我将一个变量的值与数字 10 进行比较。我在表达式中使用 >= 运算符

```
gumballsPerKid >= 10
```

当然，大于或等于的比较只能让你走这么远。表 8-1 显示了你可以用来自行比较事物的运算符。

表 8-1 比较运算符

| 操作符符号 | 含义 | 示例 |
|---|---|---|
| == | 等于 | yourGuess == winningNumber |
| != | 不等于 | 5 != numberOfCows |
| < | 小于 | strikes < 3 |
| > | 大于 | numberOfBoxtops > 1000 |
| <= | 小于或等于 | numberOfCows + numberOfBulls <= 5 |
| >= | 大于或等于 | gumballsPerKid >= 10 |

使用表 8-1 中的运算符，你可以比较数字和字符。

![](img/6d9dcff12e52b997f3ad31445b712549_181_0.png)

注意表 8-1 第一行中的双等号。不要尝试使用单个等号来比较两个值。表达式 `yourGuess = winningNumber`（使用单个等号）并不会比较 `yourGuess` 与 `winningNumber`。相反，`yourGuess = winningNumber` 会改变 `yourGuess` 的值。（它将 `winningNumber` 的值赋给变量 `yourGuess`。）

你可以用 `==` 和 `!=` 运算符比较其他事物（除了数字和字符）。但在这样做时，你必须小心。有关更多信息，请参阅第 18 章。

## 比较数字

没有什么比比较数字更枯燥乏味的了。“真或假？五大于或等于十。” 假。五既不大于也不等于十。你明白我的意思吗？真无聊。

比较整数是显而易见的。但不幸的是，当你比较十进制数时，会出现一个问题。拿一个摄氏度转华氏度的程序来说。等等！不要随便拿一个这样的程序；请使用清单 8-5 中的程序。

### 清单 8-5：这里温暖舒适

```java
import java.util.Scanner;

class CelsiusToFahrenheit {
    public static void main(String args[]) {
        Scanner keyboard = new Scanner(System.in);
        double celsius, fahrenheit;

        System.out.print("Enter the Celsius temperature: ");
        celsius = keyboard.nextDouble();

        fahrenheit = 9.0 / 5.0 * celsius + 32.0;

        System.out.print("Room temperature? ");
        System.out.println(fahrenheit == 69.8);
        keyboard.close();
    }
}
```

如果你运行清单 8-5 中的代码并输入数字 21，计算机就会计算 9.0 / 5.0 * 21 + 32.0 的值。信不信由你，你想检查计算机的答案。（谁知道呢？也许计算机算错了！）你需要做一些算术，但请不要伸手去拿计算器。计算器只是一个小型计算机，这类机器会互相袒护。要检查计算机的工作，你需要手工做算术。什么？你说你害怕数学？好吧，别担心。我已经在图 8-11 中完成了所有的数学计算。

![](img/6d9dcff12e52b997f3ad31445b712549_182_0.png)

图 8-11：华氏温度正好是 69.8。

如果你手工做算术，9.0 / 5.0 * 21 + 32.0 的值正好是 69.8。所以运行清单 8-5 中的代码并将 celsius 的值设为 21。你在显示 fahrenheit == 69.8 的值时应该得到 true，对吧？

好吧，不是。看看图 8-12 中的运行结果。当计算机计算 fahrenheit == 69.8 时，结果是 false，而不是 true。这里发生了什么？

![](img/6d9dcff12e52b997f3ad31445b712549_183_0.png)

![](img/6d9dcff12e52b997f3ad31445b712549_183_1.png)

分组分隔符因国家而异。图 8-12 所示的运行结果在世界几乎各地都适用。但如果摄氏温度是二十一点五度，你在某些国家输入 21.5（带点），在其他国家输入 21,5（带逗号）。你的计算机硬件没有内置的“国家测量仪”，但在安装计算机操作系统时，你会告诉它你住在哪个国家。Java 程序访问此信息并用它来自定义 nextDouble 方法的工作方式。

一点侦探工作可以大有帮助。所以回顾一下事实：

- ✓ **事实：** `fahrenheit` 的值应正好为 69.8。
- ✓ **事实：** 如果 `fahrenheit` 为 69.8，那么 `fahrenheit == 69.8` 为 true。
- ✓ **事实：** 在图 8-12 中，计算机显示单词 false。所以表达式 `fahrenheit == 69.8` 不是 true。

你如何调和这些事实？几乎可以肯定 fahrenheit == 69.8 为 false，这说明 fahrenheit 的值有什么问题？在清单 8-5 中，fahrenheit 的值 nowhere 被显示。这可能是问题所在吗？

在这一点上，我使用一个流行的程序员技巧。我添加语句来显示 fahrenheit 的值。

```java
fahrenheit = 9.0 / 5.0 * celsius + 32.0;
System.out.print("fahrenheit: ");    //Added
System.out.println(fahrenheit);      //Added
```

增强代码的运行结果显示在图 8-13 中。正如你所见，计算机没有达到目标。与预期的值 69.8 不同，计算机对 9.0 / 5.0 * 21 + 32.0 的值是 69.8000000000001。这就是没办法的事。计算机用零和一进行所有算术运算，所以计算机的算术运算看起来不像图 8-11 中的十进制算术。计算机的答案并不错误。答案只是稍微不准确。

图 8-13：fahrenheit 变量的完整值。

![](img/6d9dcff12e52b997f3ad31445b712549_184_0.png)

在第 7 章的一个示例中，Java 的取余运算符 (%) 给出的答案是 0.129999999999999，而不是你期望的 0.13。本节示例中也发生了同样的奇怪现象。但本节的代码并没有使用奇特的取余运算符。本节的代码使用你老朋友——除法、乘法和加法。

所以在比较两个数字是否相等（使用 ==）或不相等（使用 !=）时要小心。当你使用 Java 的 `double` 类型或 Java 的 `float` 类型时，细微的不准确性几乎可以在任何地方潜入。而几个细微的不准确性会相互累积，成为非常大的不准确性。当你比较两个 `double` 值或两个 `float` 值时，它们几乎永远不会完全相等。

![](img/6d9dcff12e52b997f3ad31445b712549_184_1.png)

> 如果你的程序没有按你认为的方式运行，请检查你对变量值的怀疑。向你的代码添加 `print` 和 `println` 语句。

![](img/6d9dcff12e52b997f3ad31445b712549_184_2.png)

> 当你比较 `double` 值时，给自己一些余地。不要比较精确相等，而是问某个值是否合理地接近预期值。例如，使用像 `fahrenheit >= 69.8 - 0.01 && fahrenheit <= 69.8 + 0.01` 这样的条件来判断 `fahrenheit` 是否在 69.8 的 0.01 范围内。要了解更多关于包含 Java `&&` 运算符的条件的信息，请参阅第 10 章。

