

## 清单 10-3：乔治·布尔会引以为傲

```java
import java.util.Scanner;

class NicePrice {
    public static void main(String args[]) {
        Scanner keyboard = new Scanner(System.in);
        int age;
        double price = 0.00;
        char reply;
        boolean isKid, isSenior, hasCoupon, hasNoCoupon;

        System.out.print("How old are you? ");
        age = keyboard.nextInt();

        System.out.print("Have a coupon? (Y/N) ");
        reply = keyboard.findWithinHorizon(".", 0).charAt(0);

        isKid = age < 12;
        isSenior = age >= 65;
        hasCoupon = reply == 'Y' || reply == 'y';
        hasNoCoupon = reply == 'N' || reply == 'n';

        if (!isKid && !isSenior) {
            price = 9.25;
        }
        if (isKid || isSenior) {
            price = 5.25;
        }

        if (hasCoupon) {
            price -= 2.00;
        }
        if (!hasCoupon && !hasNoCoupon) {
            System.out.println("Huh?");
        }

        System.out.print("Please pay $");
        System.out.print(price);
        System.out.print(". ");
        System.out.println("Enjoy the show!");

        keyboard.close();
    }
}
```

清单 10-3 代码的运行结果与图 10-5 中的内容相似。清单 10-2 与清单 10-3 之间唯一的区别在于布尔变量的使用。在清单 10-3 中，你在任何 if 语句开始之前就已经把所有小于号和双等号都处理完了。等你遇到这两个 if 语句时，条件已经可以使用简单的词语——比如 isKid、isSenior 和 hasCoupon。有了这些布尔变量，表达每个 if 语句的条件简直是轻而易举。你可以在第 8 章中了解更多关于布尔变量的内容。

添加一个布尔变量可以让你的代码更易于管理。但有些编程语言没有布尔变量，所以许多程序员更喜欢在使用 if 语句时临时构造条件。这就是为什么我在本书中混合使用这两种技术（使用布尔变量和不使用布尔变量的条件）。

## 将不同的逻辑运算符混合在一起

如果你读过清单 10-2，就会知道我当地的电影院提供折扣券。麻烦的是，我不能把优惠券和其他任何折扣叠加使用。我试图让检票员相信我还不满 12 岁，但他并不相信。这一招不奏效后，我又尝试把优惠券和老年人折扣搭配使用，但那也不管用。

电影院一定使用了某种软件来检查像我这样的人。它的代码大致如清单 10-4 所示。想观看代码运行过程，请看图 10-6。

图 10-6：
运行清单 10-4 中的代码。

```
How old are you? 7
Have a coupon? (Y/N) Y
Please pay $5.25. Enjoy the show!

How old are you? 25
Have a coupon? (Y/N) y
Please pay $7.25. Enjoy the show!

How old are you? 25
Have a coupon? (Y/N) n
Please pay $9.25. Enjoy the show!

How old are you? 85
Have a coupon? (Y/N) y
Please pay $5.25. Enjoy the show!

How old are you? 85
Have a coupon? (Y/N) Y
Please pay $5.25. Enjoy the show!
```

## 清单 10-4：儿童或老年人不另享折扣

```java
import java.util.Scanner;

class CheckAgeForDiscount {
    public static void main(String args[]) {
        Scanner keyboard = new Scanner(System.in);
        int age;
        double price = 0.00;
        char reply;

        System.out.print("How old are you? ");
        age = keyboard.nextInt();

        System.out.print("Have a coupon? (Y/N) ");
        reply = keyboard.findWithinHorizon(".", 0)
            .charAt(0);

        if (age >= 12 && age < 65) {
            price = 9.25;
        }
        if (age < 12 || age >= 65) {
            price = 5.25;
        }

        if ((reply == 'Y' || reply == 'y') &&
            (age >= 12 && age < 65)) {
            price -= 2.00;
        }

        System.out.print("Please pay $");
        System.out.print(price);
        System.out.print(".");
        System.out.println("Enjoy the show!");

        keyboard.close();
    }
}
```

清单 10-4 与其前辈清单 10-1 和 10-2 非常相似。最大的不同在于加粗的 if 语句。这个 if 语句测试两件事，而每件事本身又包含两个部分：

✓ **顾客有优惠券吗？**
也就是说，顾客输入的答案是 Y 或 y 吗？

✓ **顾客是否属于常规年龄段？**
也就是说，顾客是否至少 12 岁且小于 65 岁？

在清单 10-4 中，我使用 && 运算符将第 1 项和第 2 项连接起来。我这样做是因为，要想让顾客有资格获得 2.00 美元的折扣，这两项（第 1 项和第 2 项）都必须为真，如图 10-7 所示。

![](img/6d9dcff12e52b997f3ad31445b712549_220_0.png)

图 10-7：
回复和年龄条件必须都为真。

## 使用圆括号

清单 10-4 展示了关于条件的某个重要事项。有时，你需要使用圆括号才能让条件正确工作。例如，下面这个不正确的 if 语句：

```
//This code is incorrect:
if (reply == 'Y' || reply == 'y' &&
    age >= 12 && age < 65) {
    price -= 2.00;
}
```

将这段代码与清单 10-4 中的正确代码进行比较。这段不正确的代码没有用圆括号把 reply == 'Y' 和 reply == 'y' 分组，也没有把 age >= 12 和 age < 65 分组。结果就是图 10-8 中那对令人费解的运行结果。

图 10-8：
大写之罪。

![](img/6d9dcff12e52b997f3ad31445b712549_220_1.png)

在图 10-8 中，请注意，尽管两次运行的年龄都是 85 岁，但输入 y 和 Y 却得出了不同的票价。这是因为，在没有圆括号的情况下，任何 && 运算符都会在 || 运算符之前被求值。（Java 编程语言的规则是——先求值 &&，再求值 ||。）当 reply 为 Y 时，这个不正确的 if 语句中的条件就变成了下面这种形式：

```
reply == 'Y' || some-other-stuff-that-doesn't-matter
```

只要 reply == 'Y' 为真，整个条件就自动为真，如图 10-9 所示。

![](img/6d9dcff12e52b997f3ad31445b712549_221_0.png)

图 10-9：“真或假”的结果为“真”。

## 构建嵌套

那是 1968 年，电视剧《囚徒》正在播出。在最后一集中，剧中的英雄遇到了他的宿敌“一号”。起初，一号戴着一个诡异的笑脸/哭脸面具；当面具摘下来时，里面还有一个猴子面具。要想知道猴子面具后面是什么，你得把整部剧的 DVD 看完。但与此同时，请注意这种分层：面具里藏着面具。你也可以用 if 语句做类似的事情。本节的示例将展示具体做法。

不过还是先看一下清单 10-4。在这段代码中，条件 `age >= 12 && age < 65` 被测试了两次。两次，计算机都要将 12、65 和年龄值送入其复杂的电路丛林中，而且两次得到的答案完全相同。这很浪费，但浪费并不是你唯一要担心的问题。

如果你决定修改老年人票的年龄限制呢？从现在起，100 岁以下的人不再享受老年人折扣。你在代码中翻找，看到了第一个 `age >= 12 && age < 65` 测试。你把 65 改成 100，拍拍自己的背，然后回家。问题是，你只改了这两个 `age >= 12 && age < 65` 测试中的一个，却没有改另一个。如果能把所有 `age >= 12 && age < 65` 的判断都集中在一处，岂不是更好？

清单 10-5 前来救场。在清单 10-5 中，我把所有 if 语句都融合成一个大的代码块。代码虽然密集，但能出色地完成任务。

## 清单 10-5：嵌套 if 语句

```java
import java.util.Scanner;

class AnotherAgeCheck {

    public static void main(String args[]) {
        Scanner keyboard = new Scanner(System.in);
        int age;
        double price = 0.00;
        char reply;

        System.out.print("How old are you? ");
        age = keyboard.nextInt();

        System.out.print("Have a coupon? (Y/N) ");
        reply = keyboard.findWithinHorizon(".",
            0).charAt(0);

        if (age >= 12 && age < 65) {
            price = 9.25;
            if (reply == 'Y' || reply == 'y') {
                price -= 2.00;
            }
        } else {
            price = 5.25;
        }

        System.out.print("Please pay $");
        System.out.print(price);
        System.out.print(".");
        System.out.println("Enjoy the show!");

        keyboard.close();
    }
}
```

