

## 善用字符串变量

清单 18-1 中的程序获取用户输入并将其回显到屏幕上。这是一个很棒的程序，但（就像我认识的许多大学管理者一样）它似乎并不是特别有用。

所以，让我们来看看 Java 的 `String` 类型一个更有用的应用。清单 18-2 中就是一个很好的例子。

## 清单 18-2：把名字放入字符串变量

```java
import java.util.Scanner;
import static java.lang.System.out;

class ProcessMoreData {
    public static void main(String args[]) {
        Scanner keyboard = new Scanner(System.in);
        String fullName;
        double amount;
        boolean taxable;
        double total;

        out.print("Customer's full name: ");
        fullName = keyboard.nextLine();
        out.print("Amount: ");
        amount = keyboard.nextDouble();
        out.print("Taxable? (true/false) ");
        taxable = keyboard.nextBoolean();

        if (taxable) {
            total = amount * 1.05;
        } else {
            total = amount;
        }

        out.println();
        out.print("The total for ");
        out.print(fullName);
        out.print(" is ");
        out.print(total);
        out.println(".");

        keyboard.close();
    }
}
```

清单 18-2 中代码的一次运行结果如图 18-2 所示。这段代码将 Barry A. Burd 存储在名为 `fullName` 的变量中，并将 `fullName` 变量的内容作为输出的一部分显示出来。要让这个程序正常运行，你必须把 Barry A. Burd 存储在某处。毕竟，程序遵循着一定的步骤：

```
获取名字。
获取其他一些信息。
计算总额。
显示名字（以及其他一些信息）。
```

![](img/6d9dcff12e52b997f3ad31445b712549_365_0.png)

**图 18-2**：进行一次购买。

如果程序没有把名字存储在某处，那么当它完成获取其他信息和计算总额时，它就会忘记这个名字（所以程序无法显示名字）。

## 读取和写入字符串

要从键盘读取一个 `String` 值，你可以调用 `next` 或 `nextLine`：

- 方法 `next` 读取到下一个空白字符为止。例如，对于输入 Barry A. Burd，下面的语句

  ```java
  String firstName = keyboard.next();
  String middleInit = keyboard.next();
  String lastName = keyboard.next();
  ```

  会将 Barry 赋给 `firstName`，将 A. 赋给 `middleInit`，将 Burd 赋给 `lastName`。

- 方法 `nextLine` 读取到当前行末尾为止。例如，对于输入 Barry A. Burd，下面的语句

  ```java
  String fullName = keyboard.nextLine();
  ```

  会将 Barry A. Burd 赋给变量 `fullName`。（嘿，作为作者，确实有一些隐藏的好处。）

## 清单 18-3 *（续）*

```java
public static void main(String args[]) {
    Scanner keyboard = new Scanner(System.in);
    String password = "swordfish";
    String userInput;

    out.print("What's the password? ");
    userInput = keyboard.next();

    if (password == userInput) {
        out.println("You're okay!");
    } else {
        out.println("You're a menace.");
    }

    keyboard.close();
}
```

**图 18-3**：但我输入了正确的密码啊！

![](img/6d9dcff12e52b997f3ad31445b712549_367_0.png)

下面是这个例子中出现的事实：

- 根据清单 18-3 中的代码，`password` 的值是 `"swordfish"`。
- 在图 18-3 中，作为对程序提示的响应，用户输入了 `swordfish`。因此，在代码中，`userInput` 的值是 `"swordfish"`。
- `if` 语句检查条件 `password == userInput`。因为两个变量都有值 `"swordfish"`，所以这个条件*应该*为真，但是……

- 这个条件*不*为真，因为程序的输出是 `You're a menace.`

这到底是怎么回事？我尝试加强代码，看看能否找到一些线索。清单 18-4 中是一个增强版的密码检查程序，新版本的一次运行结果如图 18-4 所示。

## 清单 18-4：尝试调试清单 18-3 中的代码

```java
import java.util.Scanner;
import static java.lang.System.out;

class DebugCheckPassword {
    public static void main(String args[]) {
        Scanner keyboard = new Scanner(System.in);
        String password = "swordfish";
        String userInput;

        out.print("What's the password? ");
        userInput = keyboard.next();

        out.println();
        out.println("You typed           ");
        out.println(userInput);
        out.print("But the password is ");
        out.println(password);
        out.println();

        if (password == userInput) {
            out.println("You're okay!");
        } else {
            out.println("You're a menace.");
        }

        keyboard.close();
    }
}
```

**图 18-4**：这看起来更糟了。

![](img/6d9dcff12e52b997f3ad31445b712549_368_0.png)

哎哟！这次我真是被难住了。图 18-4 中的运行结果显示，`userInput` 和 `password` 变量的值都是 `swordfish`。那么，为什么程序不接受用户的输入呢？

```java
out.print("What's the password? ");
userInput = keyboard.next();

if (password.equals(userInput)) {
    out.println("You're okay!");
} else {
    out.println("You're a menace.");
}

keyboard.close();
}
```

新的密码检查代码的一次运行结果如图 18-5 所示，我可以告诉你，这真是让人大大松了一口气！清单 18-5 中的代码实际上能正常工作！当用户输入 `swordfish` 时，`if` 语句的条件为真。

![](img/6d9dcff12e52b997f3ad31445b712549_370_0.png)

## 关于类和方法的真相

清单 18-5 中的神奇之处在于使用了一个名为 `equals` 的方法。我有两种方式来解释 `equals` 方法——一种简单的方式，一种更详细的方式。首先，这里是一种简单的方式：`equals` 方法将一个字符串中的字符与另一个字符串中的字符进行比较。如果这些字符相同，那么 `if` 语句中的条件就为真。仅此而已。

![](img/6d9dcff12e52b997f3ad31445b712549_370_1.png)

不要使用双等号来比较两个 `String` 对象。相反，要使用其中一个对象的 `equals` 方法。

为了更详细地理解 `equals` 方法，请翻到第 17 章，看看图 17-7 和图 17-8。这些图说明了类、对象和表格的各个部分之间的相似性。在这些图中，每一行代表一次购买，每一列代表购买行为所具备的一个特征。

你可以对任何类观察到同样的相似性，包括 Java 的 `String` 类。事实上，图 17-7 对购买行为所做的说明，图 18-6 也对字符串做了同样的说明。

**图 18-6**：将 `String` 类和 `String` 对象视为表格的各个部分。

**String**

| value | count | equals |
|---|---|---|
| swordfish | 9 | （一个将 swordfish 与任何字符串进行比较的方法） |
| catfish | 7 | （一个将 catfish 与任何字符串进行比较的方法） |

图 18-6 中展示的内容比真实的 `String` 类故事简单得多。但图 18-6 说明了一个很好的观点。就像图 17-7 中的购买行为一样，每个字符串都有自己的特征。例如，每个字符串都有一个值（存储在字符串中的实际字符），每个字符串都有一个计数（存储在字符串中的字符数量）。你实际上不能编写下面这行代码，因为图 18-6 中的内容省略了一些微妙的细节。

```java
//This code does NOT work:
System.out.println(password.count);
```

无论如何，图 18-6 中的每一行都有三个项目——一个值、一个计数和一个 `equals` 方法。所以表中的每一行不仅仅包含数据。每一行都包含一个 `equals` 方法，这是一种利用数据来做一些有用事情的方式。就好像每个对象（`String` 类的每个实例）都有三样东西：

- 一串字符（对象的值）
- 一个数字（对象的计数）
- 一种与其他字符串进行比较的方式（对象的 `equals` 方法）

这就是面向对象编程的精髓。每个字符串都有自己的 `equals` 方法副本。例如，在清单 18-5 中，`password` 字符串有自己的 `equals` 方法。当你调用 `password` 字符串的 `equals` 方法，并将 `userInput` 字符串放入该方法的括号中时，该方法会比较这两个字符串，看看它们是否包含相同的字符。

清单 18-5 中的 `userInput` 字符串也有一个 `equals` 方法。我可以使用 `userInput` 字符串的 `equals` 方法将这个字符串与 `password` 字符串进行比较。但我没有这么做。事实上，在清单 18-5 中，我根本没有使用 `userInput` 字符串的 `equals` 方法。（要将 `userInput` 与 `password` 进行比较，我必须要么使用 `password` 字符串的 `equals` 方法，要么使用 `userInput` 字符串的 `equals` 方法。所以我做了一个随意的选择：我选择了 `password` 字符串的方法。）

