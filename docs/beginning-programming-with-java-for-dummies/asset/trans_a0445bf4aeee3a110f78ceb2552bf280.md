
## 揭示静态的黑暗

我喜欢引用自己。当我引用自己的话时，不需要书面许可。不必担心侵犯版权，也永远不会收到律师函。最棒的是，我可以随意更改和歪曲自己的话。当我转述自己的想法时，不可能被错误引用。

本着这种精神，以下是前一节的一段引文：

> “任何静态的东西都属于整个类，而不属于该类的任何特定实例……要调用静态方法，需要使用类名加上一个点。”

多么深刻！在清单18-6中，我介绍了一个名为parseInt的静态方法。下面同样的引文应用于静态parseInt方法：

> 静态parseInt方法属于整个Integer类，而不属于Integer类的任何特定实例……要调用静态parseInt方法，需要使用Integer类的名称加上一个点。你会编写类似Integer.parseInt(reply)的代码。

那太好了！我在第3章中介绍的System.out又是怎么回事呢？我也可以把我的引文应用上去。

> 静态out变量属于整个System类，而不属于System类的任何特定实例……要引用静态out变量，需要使用System类的名称加上一个点。你会编写类似System.out.println()的代码。

如果你想一想System.out的含义，这种静态的说法就讲得通了。毕竟，System.out这个名字指的是Java程序发送文本输出的地方。（当你使用Eclipse时，System.out这个名字指的是Eclipse的控制台视图。）一个典型的程序只有一个发送文本输出的地方。因此，一个Java程序只有一个out变量。无论你创建多少个对象——三个、十个还是没有——你只有一个out变量。当你把某个东西设为static时，你就确保了程序只有这样一个东西。

好，那么！out变量是静态的。

要缩写静态变量（或静态方法）的名称，你不使用普通的import声明。相反，你使用静态导入声明。这就是为什么在第9章及之后，我用static这个词来导入out变量：

```
import static java.lang.System.out;
```

![](img/f938eba5f15e231d828a6255e7ec5523_390_0.png)

图19-2：两个对象，每个都有自己的display方法。

## 调用方法

要把前一节的想法付诸实践，你需要更多代码。因此下一个清单（见清单19-3）创建Account类的实例。

### 清单19-3：使用清单19-1中的代码

```java
import java.util.Random;

class ProcessAccounts {

    public static void main(String args[]) {

        Random myRandom = new Random();
        Account anAccount;

        for (int i = 0; i < 3; i++) {
            anAccount = new Account();

            anAccount.lastName = "" +
                    (char) (myRandom.nextInt(26) + 'A') +
                    (char) (myRandom.nextInt(26) + 'a') +
                    (char) (myRandom.nextInt(26) + 'a');

            anAccount.id = myRandom.nextInt(10000);
            anAccount.balance = myRandom.nextInt(10000);
            anAccount.display();
        }
    }
}
```

以下是清单19-3中操作的总结：

```
Do the following three times:
    Create a new object (an instance of
        the Account class).
    Randomly generate values for the object's lastName,
        id and balance.
    Call the object's display method.
```

三个display调用中的第一个打印第一个对象的lastName、id和balance值。第二个display调用打印第二个对象的lastName、id和balance值。依此类推。

清单19-3代码的一次运行如图19-3所示。

![](img/f938eba5f15e231d828a6255e7ec5523_391_0.png)

**图19-3：** 运行清单19-3中的代码。

![](img/f938eba5f15e231d828a6255e7ec5523_391_1.png)

关于清单19-3中的代码，你的运行结果可能会有所不同。你不会看到与图19-3完全相同的值。事实上，如果你多次运行清单19-3，你（几乎肯定）每次都会得到不同的三字母名字、不同的ID号码和不同的账户余额。这就是程序随机生成值时发生的情况。

## 控制流

假设你正在运行清单19-3中的代码。计算机执行到display方法调用：

```
anAccount.display();
```

此时，计算机开始运行display方法内部的代码。换句话说，计算机跳转到Account类代码（清单19-1中的代码）的中间。

执行完display方法的代码（那一大片print和println调用）后，计算机返回到清单19-3中它离开的位置。也就是说，计算机回到display方法调用处，并从这里继续执行。

因此，当你运行清单19-3中的代码时，每次循环迭代中的操作流程并不完全是从上到下。相反，操作从`for`循环转到display方法，然后再回到`for`循环。整个过程如图19-4所示。

![](img/f938eba5f15e231d828a6255e7ec5523_392_0.png)

## 使用标点

在清单19-3中，注意点号的使用。要引用存储在anAccount对象中的lastName，你编写

```
anAccount.lastName
```

要让anAccount对象显示自身，你编写

```
anAccount.display();
```

太棒了！当你引用对象的变量或调用对象的方法时，唯一的区别是括号：

- 要引用对象的变量，不使用括号。
- 要调用对象的方法，使用括号。

![](img/f938eba5f15e231d828a6255e7ec5523_392_1.png)

当你调用方法时，在方法名后面加上括号。即使括号内没有任何内容，也要这样做。

## 多才多艺的加号

清单19-3中的程序使用了一些巧妙的小技巧。在Java中，你可以用加号做两件不同的事情：

- **你可以用加号对数字进行加法运算。** 例如，你可以编写

  ```
  numberOfSheep = 2 + 5;
  ```

- **你可以用加号连接字符串。** 当你连接字符串时，你把它们紧挨着挤在一起。例如，表达式

  ```
  "Barry" + " " + "Burd"
  ```

  把Barry、一个空格和Burd挤在一起。新的挤在一起的字符串是（你猜对了）Barry Burd。

在清单19-3中，语句

```
anAccount.lastName = "" +
    (char) (myRandom.nextInt(26) + 'A') +
    (char) (myRandom.nextInt(26) + 'a') +
    (char) (myRandom.nextInt(26) + 'a');
```

其中有许多加号，其中一些加号将内容连接在一起。第一个内容是一个神秘的空字符串（""）。这个空字符串是不可见的，所以它不会妨碍你看到第二、第三和第四个内容。

在空字符串之后，程序连接第二个内容。这第二个内容是表达式`(char) (myRandom.nextInt(26) + 'A')`的值。这个表达式看起来可能很复杂，但实际上没什么大不了的。这个表达式表示一个大写字母（随机生成的任意大写字母）。

在空字符串和大写字母之后，程序连接第三个内容。这第三个内容是表达式`(char) (myRandom.nextInt(26) + 'a')`的值。这个表达式表示一个小写字母（随机生成的任意小写字母）。

在所有这些内容之后，程序再连接另一个小写字母。所以总的来说，你得到了一个随机生成的三字母名字。更多细节，请参阅后面的侧边栏。

## 随机生成单词

大多数程序在第一次运行时都不能正确工作，而有些程序不经过大量反复试验也无法工作。本节中的代码就是一个很好的例子。

为了编写本节的代码，我需要一种随机生成三字母单词的方法。经过大约十几次尝试，我让代码运行起来了。但我没有就此止步。我继续工作了几个小时，寻找一种简单的随机生成三字母单词的方法。最后，我确定了以下代码（在清单19-3中）：

```
anAccount.lastName = "" +
    (char) (myRandom.nextInt(26) + 'A') +
    (char) (myRandom.nextInt(26) + 'a') +
    (char) (myRandom.nextInt(26) + 'a');
```

这段代码并不简单，但远没有我最初可运行的版本那么糟糕。总之，下面是这段代码的工作原理：

- **每次调用** `myRandom.nextInt(26)` **都会生成一个从0到25的数字。**
- **加上'A'会得到一个从65到90的数字。**

为了存储字母'A'，计算机在其内存中放入数字65。这就是为什么0加上'A'得到65，以及25加上'A'得到90的原因。（关于字母以数字形式存储的更多信息，请参阅第8章末尾关于Unicode字符的讨论。）

- **将`(char)`应用于数字会将该数字转换为char值。**

为了存储字母'A'到'Z'，计算机在其内存中放入数字65到90。因此，将`(char)`应用于65到90之间的数字会将该数字转换为大写字母。关于应用`(char)`这类转换的更多信息，请参阅第7章中关于类型转换的讨论。

稍作停顿，简要总结一下。表达式`(char) (myRandom.nextInt(26) + 'A')`表示一个随机生成的大写字母。类似地，`(char) (myRandom.nextInt(26) + 'a')`表示一个随机生成的小写字母。

注意！接下来的几步可能有点棘手。

- **Java不允许你将char值赋给字符串变量。**

所以清单19-3中的以下语句会导致编译错误：

```
//Bad statement:
anAccount.lastName = (char) (myRandom.nextInt(26) + 'A');
```

- **在Java中，你可以使用加号将char值添加到字符串中。这样做时，结果是字符串。**

所以`"" + (char) (myRandom.nextInt(26) + 'A')`是一个包含一个随机生成的大写字符的字符串。当你把`(char) (myRandom.nextInt(26) + 'a')`添加到该字符串的末尾时，你会得到另一个字符串——一个包含两个随机生成的字符的字符串。最后，当你再加上另一个`(char)`
