
列表 7.13 显示的 `PigLatin` 程序读取一个或多个句子并翻译为猪丁语。背后的 `PigTranslator` 类提供了一个基础服务：一个静态方法，它可以接收一个字符串并将其翻译为猪丁语。注意 `PigTranslator` 类不包含构造函数，因为不需要。

> 核心概念
> 对象提供的复杂服务可以分解为私有辅助方法。

### 列表 7.13

```java
****************************************************************
// PigLatin.java      Author: Lewis/Loftus
// 展示方法分解的概念。
****************************************************************

import java.util.Scanner;
```

### 列表 7.13 继续

```java
public class PigLatin {
    // 读取句子并翻译为猪丁语。
    public static void main(String[] args) {
        String sentence, result, another;
        Scanner scan = new Scanner(System.in);
        do {
            System.out.println();
            System.out.println("输入句子（不带标点符号）：");
            sentence = scan.nextLine();

            System.out.println();
            result = PigTranslator.translate(sentence);
            System.out.println("翻译成猪丁语后是:");
            System.out.println(result);

            System.out.println();
            System.out.print("翻译另一个句子吗 (y/n)? ");
            another = scan.nextLine();
        } while (another.equalsIgnoreCase("y"));
    }
}
```

```text
OUTPUT
输入句子（不带标点符号）：
Do you speak Pig Latin
翻译成猪丁语后是：
oday ouyay eakspay igpay atinlay

翻译另一个句子吗 (y/n)? y
输入句子（不带标点符号）：
Play it again Sam

翻译成猪丁语后是：
ayplay itay ayagainay amsay

翻译另一个句子吗 (y/n)? n
```

# 列表 7.14

```java
// *****************************************************************
// PigLatinTranslator.java      作者: Lewis/Loftus
// 表示一个从英语到皮丁语的翻译器。演示了
// 方法分解。
// *****************************************************************

import java.util.Scanner;
public class PigLatinTranslator {
    // 将一个单词句子翻译皮丁语。
    public static String translate(String sentence) {
        String result = "";

        sentence = sentence.toLowerCase();

        Scanner scan = new Scanner(sentence);

        while (scan.hasNext()) {
            result += translateWord(scan.next()) + " ";
        }

        return result;
    }

    // 将单个单词翻译为皮丁语。如果单词以元音开头，
    // 则在单词后添加后缀 "yay"。否则，
    // 将第一个或两个字母移动到单词末尾，
    // 并添加 "ay"。
    private static String translateWord(String word) {
        String result = "";

        if (beginsWithVowel(word)) {
            result = word + "yay";
        } else {
            if (beginsWithBlend(word)) {
                result = word.substring(2) + word.substring(0,2) + "ay";
            } else
                result = word.substring(1) + word.charAt(0) + "ay";
        }
        return result;
    }

    //-
    // 判断指定的单词是否以元音开头
    //-
    private static boolean beginsWithVowel (String word)
    {
        String vowels = "aeiou";
        char letter = word.charAt(0);
        return (vowels.indexOf(letter) != -1);
    }

    //-
    // 判断指定的单词是否以特定的
    // 字母辅音组合开头。
    //-
    private static boolean beginsWithBlend (String word)
    {
        return (word.startsWith("bl") || word.startsWith("sc") ||
                word.startsWith("br") || word.startsWith("sh") ||
                word.startsWith("ch") || word.startsWith("sk") ||
                word.startsWith("cl") || word.startsWith("sl") ||
                word.startsWith("cr") || word.startsWith("sn") ||
                word.startsWith("gr") || word.startsWith("sm") ||
                word.startsWith("cp") || word.startsWith("sp") ||
                word.startsWith("fl") || word.startsWith("sq") ||
                word.startsWith("fr") || word.startsWith("st") ||
                word.startsWith("gl") || word.startsWith("sw") ||
                word.startsWith("gr") || word.startsWith("th") ||
                word.startsWith("kl") || word.startsWith("tr") ||
                word.startsWith("ph") || word.startsWith("tw") ||
                word.startsWith("pl") || word.startsWith("wh") ||
                word.startsWith("pr") || word.startsWith("wr"));
    }
}
```

# 7.7 方法设计 337

将整个句子翻译成皮丁语并不是易事。如果写在一个巨大的方法中，它的代码将变得非常长且难以追踪。更好的解决方案（如 `PigLatinTranslator` 类实现的那样）是分解 `translate` 方法并使用其他几个方法来协助完成任务。

`translate` 方法使用 `Scanner` 对象将字符串拆分为单词。记住，`Scanner` 类（在第 3 章讨论过）的作用之一是将字符串拆分为称为标记（tokens）的较小元素。在这种情况下，标记是通过空格字符分隔的，因此我们可以使用默认的空格分隔符。皮丁语程序假设输入中不包含标点符号。

`translate` 方法将每个单词传递给私有辅助方法 `translateWord`。翻译单个单词的工作相当复杂，因此 `translate` 方法利用了另外两个方法：`beginsWithVowel` 和 `beginsWithBlend`。

`beginsWithVowel` 方法返回一个布尔值，表示作为参数传递的单词是否包含元音。该方法的代码没有检查每个元音，而是声明了一个包含所有元音的字符串，并调用 `String` 方法 `indexOf` 来确定单词的第一个字符是否在元音字符串中。如果没有找到指定的字符，`indexOf` 方法将返回 -1。

`beginsWithBlend` 方法也返回一个布尔值。该方法体只包含一个返回语句，其中包含一个表达式调用了 `String` 类的 `startsWith`。如果这些调用中任何一个返回 `true`，那么 `beginsWithBlend` 方法也会返回 `true`。

注意 `translateWord`、`beginsWithVowel` 和 `beginsWithBlend` 都被声明为 `private` 可见。它们的目的不是直接为类外的客户端提供服务。相反，它们的存在是为了帮助 `translate` 方法（这是该类中唯一的服务方法）完成工作。通过将它们声明为 `private`，无法从类外部调用它们。例如，如果 `PigLatin` 类的 `main` 方法尝试调用 `translateWord`，编译器将发出错误信息。

7.4 显示了皮丁程序的 UML 类图。注意显示各种方法可见性的符号。

每当一个方法变得巨大或复杂时，我们应该考虑将其分解为多个方法，以创建一个更易理解的类设计。然而，首先必须考虑如何定义其他类和对象以创建更好的整体设计。在面向对象的设计中，方法分解必须从于对象分解。

# 第 7 章 面向对象的设计

| PigLatin | PigLatinTranslator |

| --- | --- |

| + main (args : String[]) : void | + translate (sentence : String) : String |

| - translateWord (word : String) : String |

| - beginsWithVowel (word : String) : boolean |

| - beginsWithBlend (word : String) : boolean |

图 7.4 皮丁程序的 UML 类图

# 重新回顾方法参数

与设计相关的另一个重要问题涉及参数如何传递。在 Java 中，所有参数都是按值传递的。也就是说，实际参数（在调用处）的值被复制到方法头部的形式参数中。我们在第 4 章中提到过这一点，让我们详细检查一下。

本质上，参数传递类似于赋值，为形式参数赋值实际参数所存储的值副本。在方法内部修改形式参数时，必须考虑这个问题。形式参数是传入值的的独立副本，因此对其进行的任何更改对实际参数都没有影响。当控制返回到调用方法时，实际参数的值将与调用之前相同。

然而，当我们将对象传递给方法时，我们实际上传递的是该对象的引用。复制的值是对象的地址。形式参数和实际参数彼此引用（alias）。如果我们通过形式引用更改对象的状态，我们就更改了实际参数所引的对象。另一方面，如果我们更改了形式引用本身（使其指向新对象），我们并没有改变实际参数指向原始对象的事实。

> 核心概念
> 当将对象传递给方法时，实际参数和形式参数彼此引用（alias）。

列表 7.15 中的程序说明了参数传递的微妙之处。仔细跟踪该程序的处理过程并注意输出的值。`Tester` 类包含一个 `main` 方法，用于更改 `ParameterModifier` 对象中的 `changeValues`。`changeValues` 的两个参数是 `Num` 对象，每个对象存储一个整数值。另一个参数是基本整数值。

# 第 7 章 对象面向设计

列表 7.15 继续

在更改值之后：

f1 f2 f3

999 888 777

在调用 changeValues 后：

a1 a2 a3

111 888 333

列表 7.16 显示了 ParameterModifier 类，列表 7.17 显示了 Num 类。在 changeValues 方法内部，对三个形式参数中的每一个都进行了修改：整数参数被设置了不同的值，第一个 Num 参数中存储的值通过其 `setValue` 方法被更改，并且创建了一个新的

```java
LISTING 7.16
*******************************************************************************************************************
// ParameterModifier.java Author: Lewis/Loftus
// 展示了更改参数值的影响。
****************************************************************************************************

public class ParameterModifier {
    // 修改参数，并在修改之前和
    //之后打印它们的值。

    public void changeValues(int f1, int f2, int f3) {
        System.out.println("Before changing the values:");
        System.out.println("f1\tf2\tf3");
        System.out.println("f1 \t" + f2 + "\t" + f3 + "\n");

        f1 = 999;
        f2.setValue(888);
        f3 = new Num(777);

        System.out.println("After changing the values:");
        System.out.println("f1\tf2\tf3");
        System.out.println(f1 + "\t" + f2 + "\t" + f3 + "\n");
    }
}
```

## 7.7 方法设计

### 列表 7.17

```java
************************************************************************************
// Num.java      Author: Lewis/Loftus
// 将单个整数表示为对象。
//************************************************************************************
public class Num {
    private int value;

    --------------------------------------------------------------------------------
    // 初始化 Num 对象，存储初始值。
    --------------------------------------------------------------------------------
    public Num(int update) {
        value = update;
    }

    --------------------------------------------------------------------------------
    // 将存储的值设置为新指定的值。
    --------------------------------------------------------------------------------
    public void setValue(int update) {
        value = update;
    }

    --------------------------------------------------------------------------------
    // 将存储的整数值作为字符串返回。
    ------------------------------------------------------------------
    public String toString() {
        return value + "";
    }
}
```

了 Num 对象并将其赋值给第二个 Num 参数。这些更改反映在 changeValues 方法结束时打印的输出中。
