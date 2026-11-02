
图 19-6:
向方法参数传递值。

![](img/6d9dcff12e52b997f3ad31445b712549_400_0.png)

这里有一个有趣的现象。addInterest 方法头中的参数是 rate。但在 ProcessNiceAccounts 类内部，方法调用中的参数是 interestRate。这是可以的。事实上，这是标准做法。

在清单 19-6 和 19-7 中，参数的名称不必相同。唯一重要的是两个参数（rate 和 interestRate）具有相同的类型。在清单 19-6 和 19-7 中，这两个参数的类型都是 double。所以一切都很好。

在 addInterest 方法内部，+= 赋值运算符将 balance * (rate / 100.0) 加到现有的 balance 值上。有关 += 赋值运算符的一些信息，请参阅第 7 章。

## 使用方法头

在接下来的几个要点中，我对 addInterest 方法头（在清单 19-6 中）做一些观察：

- ✔ 单词 `void` 告诉计算机，当 `addInterest` 方法被调用时，`addInterest` 方法不会向调用它的地方发送返回值。
- 下一节有一个方法发送返回值的示例。
- ✔ 单词 `addInterest` 是方法的名字。
- 这就是你在为 `ProcessNiceAccounts` 类编写代码时调用该方法时使用的名称（参见清单 19-7）。
- ✔ 头中的括号包含调用方法时将传递给方法的所有内容的占位符。

当你调用方法时，可以即时向该方法传递信息。这些信息是方法的参数列表。addInterest 方法的头说 addInterest 方法接受一个信息，并且该信息必须是 double 类型：

```
void addInterest(double rate)
```

确实如此，如果你查看对 addInterest 的调用（在 ProcessNiceAccounts 类的 main 方法中），该调用包含变量 interestRate。而 interestRate 的类型是 double。当我调用 getInterest 时，我给方法一个 double 类型的值。

## 方法如何使用对象的值

清单 19-6 中的 addInterest 方法从清单 19-7 中的 main 方法被调用三次。每次实际的账户余额和利率都不同：

在图 19-5 的第一次调用中，balance 为 8983.00，利率为 2.0。

当此调用被执行时，表达式 balance * (rate / 100.0) 代表 8983.00 * (2.0 / 100.0)。参见图 19-7。

![](img/6d9dcff12e52b997f3ad31445b712549_401_0.png)

图 19-7：Cb 的账户和 Bry 的账户。

✓ **在图 19-5 的第二次调用中，balance 为 3756.00，利率为 0.0。**

当调用被执行时，表达式 `balance * (rate / 100.0)` 代表 `3756.00 * (0.0 / 100.00)`。再次参见图 19-7。

✓ **在图 19-5 的第三次调用中，balance 为 8474.00，利率为 3.0。**

当 `addInterest` 调用被执行时，表达式 `balance * (rate / 100.0)` 代表 `8474.00 * (3.0 / 100.00)`。

## 从方法获取值

假设你派朋友去买杂货。你以方法调用的形式提出杂货请求。你发出如下调用：

```
goToTheSupermarketAndBuySome (bread);
goToTheSupermarketAndBuySome (bananas);
```

括号中的东西是参数。每次调用你的 `goToTheSupermarketAndBuySome` 方法时，你在方法参数列表中放入不同的值。

现在当你的朋友从超市回来时会发生什么？"这是你让我买的面包，"你的朋友说。作为实现你愿望的结果，你的朋友向你返回了一些东西。你进行了一个方法调用，而方法返回信息（或者更好的是，方法返回一些食物）。

返回给你的东西称为方法的 *返回值*，而返回给你的东西的类型称为方法的 *返回类型*。

## 一个示例

要了解返回值和返回类型在真实 Java 程序中如何工作，请查看清单 19-8 和 19-9 中的代码。

## 清单 19-8：返回值的 方法

```
import java.text.NumberFormat;
import static java.lang.System.out;

class GoodAccount {
    String lastName;
    int id;
    double balance;

    double getInterest(double rate) {
        double interest;

        out.print("Adding ");
        out.print(rate);
        out.println(" percent...");

        interest = balance * (rate / 100.0);
        return interest;
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

## 清单 19-9：调用清单 19-8 中的方法

```
import java.util.Random;
import java.text.NumberFormat;

class ProcessGoodAccounts {

    public static void main(String args[]) {
        Random myRandom = new Random();
        NumberFormat currency =
            NumberFormat.getCurrencyInstance();
        GoodAccount anAccount;
        double interestRate;
        double yearlyInterest;
```

当 getInterest 被调用时会发生什么（你可以在图 19-9 中跟随）：

- balance 的值为 9508.00，rate 的值为 2.0。因此 balance * (rate / 100.0) 的值为 190.16 —— 一百九十美元十六美分。
- 值 190.16 被赋给 interest 变量，因此语句
```
return interest;
```
具有相同的效果
```
return 190.16;
```
- return 语句将此值 190.16 发送回调用该方法的代码。在此过程中，清单 19-9 中的整个方法调用 —— anAccount.getInterest(interestRate) —— 取得值 190.16。
- 最后，值 190.16 被赋给变量 yearlyInterest。

![](img/6d9dcff12e52b997f3ad31445b712549_405_0.png)

图 19-9
方法调用是一个具有值 的表达式。

![](img/6d9dcff12e52b997f3ad31445b712549_405_1.png)

如果方法返回任何内容，那么对该方法的调用就是一个具有值的表达式。该值可以被打印、赋给变量、加到其他东西上，或任何操作。你可以用任何其他类型的值做的任何事情，都可以用方法调用来做。

## 使用方法头（再次）

当你创建方法或方法调用时，必须小心一致地使用 Java 的类型。因此请确保检查以下内容：

- 在清单 19-8 中，`getInterest` 方法的头以单词 `double` 开始。因此当方法被执行时，它应该向调用它的地方发送一个 double 值。
- 同样在清单 19-8 中，`getInterest` 方法中的最后一句是 `return interest`。因此方法返回存储在 interest 变量中的任何值，而 interest 变量的类型为 double。迄今为止，一切都很好。
- 在清单 19-9 中，对 `getInterest` 的调用返回的值被赋给名为 `yearlyInterest` 的变量。确实如此，`yearlyInterest` 的类型为 double。

这就确定了！在清单 19-8 和 19-9 中，方法 `getInterest` 的处理中类型的用法是一致的。我太兴奋了！

## 第 20 章

## Oooey GUI Was a Worm

## 本章内容

- 开始行动
- 显示图像
- 使用按钮和文本框

有一个关于马戏团杂技演员跳过老鼠的精彩老笑话。不幸的是，如果我把这个笑话收录在这本书里，我会被起诉侵犯版权。

无论如何，这个笑话讲的是从小处着手，逐步做大。这就是你在阅读 *Beginning Programming with Java For Dummies, 4th Edition* 时所做的事情。

本书中的大多数程序都是基于文本的。*基于文本* 的程序没有窗口，没有对话框，没有此类东西。在基于文本的程序中，用户在 Console 视图中输入字符，程序在同一 Console 视图中显示输出。

如今，公开可用的基于文本的程序非常少。几乎所有程序都使用 GUI —— *图形用户界面*。所以如果你已经读到现在本书的每个字，你可能正在对自己说：“我什么时候才能知道如何创建 GUI？”

好吧，现在就是时候了！本章向你介绍 Java 中 GUI 编程的世界。

你可以通过访问本书的网站 (allmycode.com/BeginProg) 查看本书中许多示例的 GUI 版本。

![](img/6d9dcff12e52b997f3ad31445b712549_408_0.png)
