

*（续）*

把 `(myRandom.nextInt(26) + 'a')` 拼到该字符串末尾，你就得到了一个包含三个随机生成字符的字符串。因此你可以像这样把那个大字符串赋值给 `anAccount`。清单 19-3 中的语句就是这么工作的。

当你编写像清单 19-3 这样的程序时，必须非常小心地处理数字、`char` 值和字符串。我不是每天都做这类编程。所以在让本小节的示例正常工作之前，我经历了很多次失败的开头。没关系，我非常执着。

![](img/f938eba5f15e231d828a6255e7ec5523_395_0.png)

在清单 19-3 中，语句 `anAccount.balance = myRandom.nextInt(10000)` 将一个 `int` 值赋给了 `balance`。但 `balance` 是一个 `double` 变量，而不是 `int` 变量。这没问题。在罕见的宽容情况下，Java 允许你将 `int` 值赋给 `double` 变量。赋值的结果毫不意外。如果你将 `int` 值 8734 赋给 `double` 变量 `balance`，那么 `balance` 的值就变成了 8734.00。结果如图 19-3 的第一行所示。

![](img/f938eba5f15e231d828a6255e7ec5523_395_1.png)

使用 `double` 类型来存储金额通常不是一个好主意。在本书中，我使用 `double` 是为了尽可能让示例简单。但 `int` 类型更适合存储货币值，而 `BigDecimal` 类型则更佳。更多细节请参见第 7 章。

## 让对象自己干活

当我还是一个小对象时，我可没有你们现在拥有的对象那么聪明。例如，考虑清单 19-4 中的对象。这个对象不仅能显示自己，还能自己填充值。

### 清单 19-4：具有两个方法的类

```java
import java.util.Random;
import java.text.NumberFormat;
import static java.lang.System.out;

class BetterAccount {
    String lastName;
    int id;
    double balance;

    void fillWithData() {
        Random myRandom = new Random();
        lastName = "" +
            (char) (myRandom.nextInt(26) + 'A') +
            (char) (myRandom.nextInt(26) + 'a') +
            (char) (myRandom.nextInt(26) + 'a');

        id = myRandom.nextInt(10000);
        balance = myRandom.nextInt(10000);
    }

    void display() {
        NumberFormat currency =
            NumberFormat.getCurrencyInstance();

        out.print("The account with last name ");
        out.print(lastName);
        out.print(" and ID number ");
        out.print(id);
        out.print(" has balance ");
        out.println(currency.format(balance));
    }
}
```

我编写了一些代码来使用清单 19-4 中的类。这些新代码在清单 19-5 中。

### 清单 19-5：这太酷了！

```java
class ProcessBetterAccounts {

    public static void main(String args[]) {

        BetterAccount anAccount;

        for (int i = 0; i < 3; i++) {
            anAccount = new BetterAccount();
            anAccount.fillWithData();
            anAccount.display();
        }
    }
}
```

清单 19-5 相当巧妙。因为清单 19-4 中的代码非常聪明，所以清单 19-5 中的新代码几乎没什么工作要做。这段新代码只是创建一个 `BetterAccount` 对象，然后调用清单 19-4 中的方法。当你运行所有这些代码时，会得到类似图 19-3 的结果。

```java
out.print(id);
out.print(" has balance ");
out.println(currency.format(balance));
}
}
```

### 清单 19-7：调用 addInterest 方法

```java
import java.util.Random;

class ProcessNiceAccounts {

    public static void main(String args[]) {
        Random myRandom = new Random();
        NiceAccount anAccount;
        double interestRate;

        for (int i = 0; i < 3; i++) {
            anAccount = new NiceAccount();

            anAccount.lastName = "" +
                (char) (myRandom.nextInt(26) + 'A') +
                (char) (myRandom.nextInt(26) + 'A') +
                (char) (myRandom.nextInt(26) + 'a');
            anAccount.id = myRandom.nextInt(10000);
            anAccount.balance = myRandom.nextInt(10000);

            anAccount.display();

            interestRate = myRandom.nextInt(5);
            anAccount.addInterest(interestRate);

            anAccount.display();
            System.out.println();
        }
    }
}
```

在清单 19-7 中，这一行

```java
anAccount.addInterest(interestRate);
```

所扮演的角色，与我的小超市示例中的 `goToTheSupermarketAndBuySome (bread)` 这一行相同。单词 `addInterest` 是方法名，括号中的单词 `interestRate` 是参数。从整体上看，这个语句告诉清单 19-6 中的代码执行它的 `addInterest` 方法。这个语句还告诉清单 19-6 在方法的计算中使用某个数字（即 `interestRate` 变量中存储的任何值）。`interestRate` 的值可以是 1.0、2.0，或者你调用 `myRandom.nextInt(5)` 得到的任何其他值。同样，`goToTheSupermarketAndBuySome` 方法也适用于面包、香蕉，或者你从超市需要的任何其他东西。

下一节将详细描述 `addInterest` 及其行为。与此同时，清单 19-6 和 19-7 中代码的一次运行结果如图 19-5 所示。

![](img/f938eba5f15e231d828a6255e7ec5523_399_0.png)

**图 19-5：** 运行清单 19-7 中的代码。

![](img/f938eba5f15e231d828a6255e7ec5523_399_1.png)

Java 对类型的使用有非常严格的规定。例如，你不能将 `double` 值（如 3.14）赋给 `int` 变量。（编译器根本不会去掉 `.14` 部分。你会得到一条错误消息。那又有什么新鲜的呢？）但 Java 在类型使用上也不是完全不讲道理。Java 允许你将 `int` 值（如 `myRandom.nextInt(5)`）赋给 `double` 变量（如 `interestRate`）。如果你将 `int` 值 2 赋给 `double` 变量 `interestRate`，那么 `interestRate` 的值就变成了 2.0。结果如图 19-5 的第二行所示。

## 传递值

当你调用方法时，可以动态地向该方法传递信息。这些信息位于方法的参数列表中。清单 19-7 中有一个对 `addInterest` 方法的调用：

```java
anAccount.addInterest(interestRate);
```

在循环的第一次迭代中，`interestRate` 的值是 2.0。（记住，我使用的是图 19-5 中的数据。）所以在程序运行的该时刻，这个方法调用表现得就像下面的语句：

```java
anAccount.addInterest(2.0);
```

计算机即将运行 `addInterest` 方法内部的代码（清单 19-6 中的一个方法）。但首先，计算机将值 2.0 传递给 `addInterest` 方法头中的参数。因此在 `addInterest` 方法内部，`rate` 的值变成了 2.0。有关这个想法的图示，请参见图 19-6。

当你调用方法时，可以动态地向该方法传递信息。这些信息就是方法的参数列表。`addInterest` 方法的方法头表明，`addInterest` 方法接受一条信息，并且这条信息必须是 `double` 类型：

```java
void addInterest(double rate)
```

确实，如果你查看对 `addInterest` 的调用（在 `ProcessNiceAccounts` 类的 `main` 方法中），该调用中有变量 `interestRate`，而 `interestRate` 是 `double` 类型。当我调用 `getInterest` 时，我给该方法传递了一个 `double` 类型的值。

## 方法如何使用对象的值

清单 19-6 中的 `addInterest` 方法被清单 19-7 中的 `main` 方法调用了三次。每次实际的账户余额和利率都不同：

- **在图 19-5 的第一次调用中，`balance` 是 8983.00，利率是 2.0。**
当进行这次调用时，表达式 `balance * (rate / 100.0)` 代表 `8983.00 * (2.0 / 100.00)`。参见图 19-7。

![](img/f938eba5f15e231d828a6255e7ec5523_401_0.png)

**在图 19-5 的第二次调用中，余额是 3756.00，利率是 0.0。**

当进行调用时，表达式 `balance * (rate / 100.0)` 代表 3756.00 * (0.0 / 100.00)。同样参见图 19-7。

**在图 19-5 的第三次调用中，余额是 8474.00，利率是 3.0。**

当进行 `addInterest` 调用时，表达式 `balance * (rate / 100.0)` 代表 8474.00 * (3.0 / 100.00)。

## 从方法获取值

假设你派一位朋友去买杂货。你以方法调用的形式提出购物请求。你会发出这样的调用：

```
goToTheSupermarketAndBuySome (bread);
goToTheSupermarketAndBuySome (bananas);
```

括号里的东西就是参数。每次调用 `goToTheSupermarketAndBuySome` 方法时，你都在方法的参数列表中放入一个不同的值。

现在，当你的朋友从超市回来时会发生什么？“这是你让我买的面包，”你的朋友说。由于执行了你的愿望，你的朋友返回了一些东西给你。你发出了一个方法调用，方法返回了信息（或者更好的是，方法返回了一些食物）。

返回给你的东西叫做方法的*返回值*，返回给你的东西的类型叫做方法的*返回类型*。

## 一个示例

要了解返回值和返回类型在真实 Java 程序中的工作方式，请查看清单 19-8 和 19-9 中的代码。

