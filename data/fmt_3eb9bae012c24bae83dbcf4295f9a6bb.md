
局部变量 `n` 在参数变量 `n` 的作用域内。`cubeVolume` 方法尝试获取该变量，但它不能——`sideLength` 的作用域没有延伸到 `main` 方法之外。解决方法是将作为参数传递，正如我们在 5.2 节中讨论的那样。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_262_0.png)

考虑示例：

```java
1 class Sample {
2 x = 4;
3 mystery(x);
4 System.out.println(x);
5 static void mystery(int x) {
6 s = 0;
7 for (int i = 0; i < x; i++) {
8 s = i + 1;
9 }
10 }
11 }
12 }
17 }
18 return s;
19 }
20
```

- 31 行代码在 `i` 的作用域内？

- 32 行代码在 `x` 的作用域内？

- 有同名的变量。它们是什么？

- 方法中有一个错误。你如何修复它？

- 错误是什么？

- 现在你可以尝试章节末尾的练习题：

## 视频示例 5.1 调试

在示例中，你将学习如何使用调试器来寻找错误。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_263_0.png)

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_263_1.png)

## 5.9 递归方法（可选）

递归方法是一种调用它自身的方法。这听起来并不不寻常。假设你面临着清理房屋的艰巨任务。你可能会说：“我会先选一个房间，然后清理剩下的部分。”换句话说，该方法通过更简单的输入调用它自己。最终，房间会被清理干净。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_263_2.png)

- 可在 WileyPLUS 和 www.wiley.com/college/horstmann 获取。

## 5.9 递归方法（可选） 229

在 Java 中，递归方法使用相同的原理。这是一个典型的示例。具体来说，我们的任务是打印如下的模式：

```java
public static void printTriangle(int sideLength)
```

上面的三角形是通过调用 `printTriangle(4)` 打印的。为了理解递归有帮助，考虑如何从边长为3的三角形得到长度为4的三角形。

```
打印边长为 3 的三角形。
打印一行 []。
```

更通地说，这里是任意边长度的指令：

```java
public static void printTriangle(int sideLength)
    printTriangle(sideLength - 1);
    for (int i = 0; i < sideLength; i++)
    {
        System.out.print("");
    }
    System.out.println();
```

这个想法只有一个问题。当边长为 1 时，我们不想调用 `printTriangle(0)`、`printTriangle(-1)` 等。解决方案仅仅是将其视为一个特例，并且当边长小于 1 时不打印任何内容。

```java
public static void printTriangle(int sideLength)
    if (sideLength < 1) { return; }
    printTriangle(sideLength - 1);
    for (int i = 0; i < sideLength; i++)
    {
        System.out.print("");
    }
    System.out.println();
```

再次观察这个方法，注意它是多么的合理。如果边长为 0，不需要打印任何内容。接下来的部分同样合理。打印较小的三角形，不要去想为什么那样有效。我们打印一行 []。

为了确保递归成功的关键要求是：

- 每次递归调用必须以某种方式简化任务。

- 必须有特例来直接处理简单的任务。

## 230 第 5 章 方法

这套俄罗斯娃娃看起来和递归方法的调用模式很相似。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_265_0.png)

当我们打印一个边长为 4 的三角形时，发生了以下情况：

- `printTriangle(4)` 调用 `printTriangle(3)`。

- `printTriangle(3)` 调用 `printTriangle(2)`。

- `printTriangle(2)` 调用 `printTriangle(1)`。

- `printTriangle(1)` 调用 `printTriangle(0)`。

- `printTriangle(0)` 返回，什么都不做。

- `printTriangle(1)` 打印 []。

- `printTriangle(2)` 打印 []。

- `printTriangle(3)` 打印 [][]。

- `printTriangle(4)` 打印 [][][]。

递归方法的模式看起来很复杂，而成功设计一个方法的关键在于不要去思考它。打印三角形形状并不是真的递归。你可以使用嵌套循环：

```java
public static void printTriangle(int sideLength)
{
    for (int i = 0; i < sideLength; i++) {
        for (int j = 0; j < i; j++) {
            System.out.print(" ");
        }
    }
    System.out.println();
}
```

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_265_1.png)

在线示例 完整的 TrianglePrinter 程序。

然而，这一对循环有点棘手。许多人发现递归解决方案更容易理解。

36. 考虑这个对 `printTriangle` 方法的轻微修改：

```java
public static void printTriangle(int sideLength)
{
    if (sideLength < 1) { return; }
    for (int i = 0; i < sideLength; i++) {
        System.out.print(" ");
    }
}
```

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_265_2.png)

## 5.9 递归方法（可选） 231

```java
}
    System.out.println();
    printTriangle(sideLength - 1);
}
```

`printTriangle(4)` 的结果是什么？

- 37. 考虑这个递归方法：

```java
public static int mystery(int n)
{
    if (n <= 0) { return 0; }
    return n + mystery(n - 1);
}
```

`mystery(4)` 是什么？

- 38. 考虑这个递归方法：

```java
public static int mystery(int n)
{
    if (n <= 0) { return 0; }
    return mystery(n / 2) + 1;
}
```

`mystery(20)` 是什么？

- 39. 写一个递归方法，在一行打印 `n` 个方框 `[]`。

40. 第 5.7 节中的 `inName` 方法接受小于 1,000 的参数。使用递归调用，将其范围扩展到 99,999。例如，如果 12,345 应该返回 "twelve thousand three hundred forty five"。

现在练习 你可以尝试章节末尾的练习题：R56, P15, P18。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_266_0.png)

## 递归地思考

递归地解决问题需要与通过编程循环解决问题不同的思维方式。事实上，如果你假装得有点懒，让别人为你完成大部分工作，会有帮助的。如果你需要解决一个复杂的问题，假装“其他人”会承担重任，而你只需要解决更简单的输入。那么你只需要弄如何将复杂问题转换为几个更简单的输入。

为了说明递归思考过程，考虑第 4.2 节的问题：计算数字各位数字之和。我们想设计一个 `digitSum` 方法来计算整数 `n` 的各位数字之和。

例如，`digitSum(1729)` = 1 + 7 + 2 + 9 = 19。

将输入拆分为可以通过问题解决的部分。

在你的脑海中，针对你想要解决的任务考虑特定的输入或一组输入，以及你如何简化这些输入。

在数字问题中，我们如何简化输入 `n = 1729` 呢？减去最后一位会有帮助。之后，`digitSum(1728)` = 18。

一种更有前景的方法是移除最后一位，即计算 `n / 10`。`digitSum(1000)` 和 `digitSum(999)` 之间似乎没有明显的联系。172 的数字和与 1729 的和直接相关。

## 232 第 5 章 方法

### 步骤 1

在你的脑海中，考虑你在步骤 1 中发现的更简单输入的解决方案。不要担心那些解决方案是如何获得的。只需让这些解决方案随手可用。对自己说：这些更简单，所以别人会解决这个问题。

在你的数字任务中，问自己如何获得 `digitSum(1729)`，如果 `n = 1729`。减去最后一位会有帮助。之后，`digitSum(1728)` = 18。

一种更有前景的方法是移除最后一位，即计算 `n / 10`。`digitSum(1000)` 和 `digitSum(999)` 之间似乎没有明显的联系。172 的数字和与 1729 的和直接相关。

在你的数字任务中，问自己如何获得 `digitSum(1729)`，如果 `n = 1729`。减去最后一位会有帮助。之后，`digitSum(1728)` = 18。
