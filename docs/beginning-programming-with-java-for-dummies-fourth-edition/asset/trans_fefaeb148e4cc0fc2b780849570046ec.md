
**图 9-2：** 一个随机数决定你的命运。

![](img/6d9dcff12e52b997f3ad31445b712549_195_0.png)

要得到一个真实的 if 语句，请为三个占位符 Condition、SomeStatements 和 OtherStatements 替换有意义的文本。以下是我在清单 9-1 中进行替换的方式：

- ✓ 我用 `randomNumber > 5` 替换 Condition。
- ✓ 我用 `System.out.println("Yes. Isn't it obvious?");` 替换 SomeStatements。
- ✓ 我用 `System.out.println("No, and don't ask again.");` 替换 OtherStatements。

替换在图 9-3 中说明。

**图 9-3：** 一个 if 语句及其格式。

![](img/6d9dcff12e52b997f3ad31445b712549_195_1.png)

有时我需要为 if 语句的各个部分使用替代名称。我称它们为 if 子句和 else 子句。

```
if (Condition) {
    if clause
} else {
    else clause
}
```

一个 if 语句是复合语句的一个例子——一种在其内部包含其他语句的语句。清单 9-1 中的 if 语句包含两个 println 调用，而这些对 println 的调用就是语句。

注意我在清单 9-1 的 if 语句中使用括号和分号的方式。特别是，注意以下几点：

- 条件必须放在括号中。
- if 子句中的语句以分号结束。else 子句中的语句也是如此。
- 条件之后没有分号。
- else 之后没有分号。

作为一名初学者程序员，你可能会认为这些规则是任意的。但事实并非如此。这些规则属于一个精心设计的语法。它们就像英语句子的语法规则，但它们甚至更合乎逻辑！（对不起，Melba。）

表 9-1 向你展示了在破坏 if 语句标点规则时可能出现的问题。该表的最后两项是最臭名昭著的。在这两种情况下，编译器不会捕获错误。这会让你产生一种虚假的安全感。问题是，当你运行程序时，代码的行为不是你所期望的。

**表 9-1 常见的 if 语句错误信息**

| 错误 | 示例 | 最可能的消息或结果 |
|---|---|---|
| 缺少条件周围的括号 | `if randomNumber > 5 {` | '(' expected Syntax error on token "if", ( expected after this token |
| if 子句或 else 子句内部的语句后缺少分号 | `if (randomNumber > 5) { System.out.println("Y")}` | ',' expected Syntax error, insert ";" to complete BlockStatements |
| 条件后立即出现分号 | `if (randomNumber > 5); { System.out.println("Y");} else {` | 'else' without 'if' Syntax error on token "else", delete this token |
| else 之后立即出现分号 | `} else; {` | 程序可以无错误编译，但 else 之后的那条语句无论条件为真还是为假都会始终执行。 |
| 缺少大括号 | `if (randomNumber > 5) System.out.println("Y");else System.out.println("N");` | 程序有时可以无错误编译，但程序的运行可能不会按你期望的方式执行。（所以底线是，不要省略大括号。） |

当你编写代码时，将 if 语句视为一个不可分割的单元会有所帮助。与其输入整行第一行（条件等），不如尝试输入 if 语句的骨架大纲。

```
if () {        // To do: Fill in the condition.
               // To do: Fill in SomeStatements.
} else {
               // To do: Fill in OtherStatements.
}
```

在整个大纲就位后，你就可以开始处理待办事项清单上的项目。当你将这种思考方式应用于复合语句时，犯错的可能性更小。

## 一个完整的程序

清单 9-2 包含一个带有简单 if 语句的完整程序。该清单的代码表现得像一个电子神谕。向程序提出一个是非问题，程序会回答你。当然，你问题的答案是随机生成的。但谁在乎呢？提问本身很有趣。

### 清单 9-2：我无所不知

```
import java.util.Scanner;
import java.util.Random;

class AnswerYesOrNo {

    public static void main(String args[]) {
        Scanner keyboard = new Scanner(System.in);
        Random myRandom = new Random();
        int randomNumber;

        System.out.print("Type your question, my child: ");
        keyboard.nextLine();

        randomNumber = myRandom.nextInt(10) + 1;

        if (randomNumber > 5) {
            System.out.println("Yes. Isn't it obvious?");
        } else {
            System.out.println("No, and don't ask again.");
        }

        keyboard.close();
    }
}
```

图 9-4 显示了清单 9-2 中程序的几次运行。该程序的操作分为四个部分：

1. **提示用户。**
    调用 System.out.print，告诉用户输入一个问题。
2. **从键盘获取用户的问题。**

在图 9-4 中，我运行 AnswerYesOrNo 程序四次，每次输入不同的问题。与此同时，在清单 9-2 中，语句 `keyboard.nextLine();` 吞掉了我的问题并且完全不做任何处理。这是一个异常，但你很聪明，所以你可以处理它。

![](img/6d9dcff12e52b997f3ad31445b712549_199_0.png)

![](img/6d9dcff12e52b997f3ad31445b712549_199_1.png)

![](img/6d9dcff12e52b997f3ad31445b712549_199_2.png)

![](img/6d9dcff12e52b997f3ad31445b712549_199_3.png)

图 9-4：无所不知的 Java 程序运行情况。

通常，当程序从键盘获取输入时，程序会做些什么来处理输入。例如，程序可以将输入分配给变量：

```
amount = keyboard.nextDouble();
```

或者，程序可以将输入显示在屏幕上：

```
System.out.println(keyboard.nextLine());
```

但清单 9-2 中的代码不同。当这个 AnswerYesOrNo 程序运行时，用户必须输入一些内容。（对 getLine 的调用会等待用户输入一些内容然后按 Enter。）但 AnswerYesOrNo 程序不需要存储输入以供进一步分析。（计算机做的事情就像我妻子问我是否打算收拾好自己时我做的那样。我忽略问题并编造一个任意答案。）因此程序对用户的输入不做任何处理。keyboard.nextLine 的调用就这样单独放在一条语句中，什么也不做，像一个大黑洞一样。这对于程序来说是不寻常的，但电子神谕是一个不寻常的东西。它需要一些稍微不寻常的代码。

3. **获取一个随机数——任意 1 到 10 的 int 值。**

好吧，聪明人。你刚刚丢弃了用户的输入。你将如何对用户的问题回答是或否？

没问题！完全没问题！你将随机显示一个答案。用户不会知道区别。（哈，哈！）只要你能生成随机数就可以做到这一点。1 到 10 的数字就足够了。

在清单 9-2 中，关于 Random 和 myRandom 的内容看起来很像熟悉的 Scanner 代码。从初学者程序员的角度来看，Random 和 Scanner 的工作方式几乎相同。当然，有一个重要的区别。对 Random 类的 `nextInt(10)` 方法的调用不会从键盘获取任何内容。相反，这个 `nextInt(10)` 方法从天而降地获取一个数字。

名称 Random 在 Java API 中定义。清单 9-2 中的 `myRandom.nextInt(10)` 调用获取一个 0 到 9 的数字。然后我的代码加上 1（得到 1 到 10 的数字）并将该数字分配给变量 randomNumber。完成后，你就可以回答用户的问题了。

在 Java 的 API 中，单词 Random 是 Java 类的名称，而 nextInt 是 Java 方法的名称。有关类与方法之间关系的更多信息，请参阅第 17、18 和 19 章。

![](img/6d9dcff12e52b997f3ad31445b712549_200_0.png)

4. **回答是或否。**

调用 `myRandom.nextInt(10)` 就像在电视游戏节目上旋转一个轮子。轮子上标有 1 到 10 的槽位。清单 9-2 中的 if 语句将你的数字转换为是或否的替代方案。如果你掷出大于 5 的数字，程序会回答是。否则（如果你掷出小于或等于 5 的数字），程序会回答否。

你可以相信我这一点。我已经根据我的 AnswerYesOrNo 程序做出了很多重要决定。

## 在代码中缩进 if 语句

注意，在清单 9-2 中，if 语句内部的 println 调用是缩进的。严格来说，你不必缩进 if 语句内部的语句。对编译器来说，你可以把整个程序写在一行上，或者把所有语句放在一个艺术化的、不成形的锯齿形中。问题是，如果你不以某种合乎逻辑的方式缩进语句，那么你或其他任何人都无法理解你的代码。在清单 9-2 中，println 调用的缩进有助于你的眼睛（和大脑）快速看出这些语句从属于整体的 if/else 流程。

在小型程序中，未缩进或缩进不良的代码勉强可以忍受。但在复杂的程序中，缩进不遵循整洁、合乎逻辑的模式会成为一个大而丑陋的噩梦。

始终缩进你的代码，以便程序的流程一目了然。

![](img/6d9dcff12e52b997f3ad31445b712549_200_1.png)
