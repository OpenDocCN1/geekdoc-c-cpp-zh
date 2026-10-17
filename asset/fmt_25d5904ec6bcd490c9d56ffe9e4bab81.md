
我们使用 `Ctrl+F5` 在不带调试的情况下运行程序。结果是错误的——牌没有被洗牌。Initial deck: (7 HEART)(A SPADE)(10 DIAMOND)(2 CLUB)(6 DIAMOND)(J CLUB)

我们再次通过 `F5` 进度以调试模式运行程序。调试器再次在断点处停止，程序运行依然没有问题。(7 HEART)(A SPADE)(10 DIAMOND)(2 CLUB)(6 DIAMOND)(J CLUB) (A SPADE)(7 HEART)(10 DIAMOND)(2 CLUB)(6 DIAMOND)(J CLUB) (6 DIAMOND)(7 HEART)(10 DIAMOND)(2 CLUB)(A SPADE)(J CLUB) (2 CLUB)(7 HEART)(10 DIAMOND)(A SPADE)(J CLUB)(6 DIAMOND)

After shuffle: (7 HEART)(A SPADE)(10 DIAMOND)(2 CLUB)(6 DIAMOND)(J CLUB)

Initial deck: (7 HEART)(A SPADE)(10 DIAMOND)(2 CLUB)(6 DIAMOND) (10 DIAMOND)(7 HEART)(A SPADE)(J CLUB)

After shuffle: (10 DIAMOND)(7 HEART)(A SPADE)(J CLUB)

Initial deck: (7 HEART)(A SPADE)(10 DIAMOND)(2 CLUB)(6 DIAMOND)(J CLUB)

After shuffle: (7 HEART)(A SPADE)(10 DIAMOND)(2 CLUB)(6 DIAMOND)(J CLUB)

Initial deck: (7 HEART)(A SPADE)(10 DIAMOND)(2 CLUB)(6 DIAMOND)(J CLUB)

After shuffle: (7 HEART)(A SPADE)(10 DIAMOND)(2 CLUB)(6 DIAMOND)(J CLUB)

Initial deck: (7 HEART)(A SPADE)(10 DIAMOND)(2 CLUB)(6 DIAMOND)(J CLUB)

After shuffle: (7 HEART)(A SPADE)(10 DIAMOND)(2 CLUB)(6 DIAMOND)(J CLUB)

Initial deck: (7 HEART)(A SPADE)(10 DIAMOND)(2 CLUB)(6 DIAMOND)(J CLUB)

After shuffle: (7 HEART)(A SPADE)(10 DIAMOND)(2 CLUB)(6 DIAMOND)(J CLUB)

Initial deck: (7 HEART)(A SPADE)(10 DIAMOND)(2 CLUB)(6 DIAMOND)(J CLUB)

After shuffle: (7 HEART)(A SPADE)(10 DIAMOND)(2 CLUB)(6 DIAMOND)(J CLUB)

Initial deck: (7 HEART)(A SPADE)(10 DIAMOND)(2 CLUB)(6 DIAMOND)(J CLUB)

After shuffle: (7 HEART)(A SPADE)(10 DIAMOND)(2 CLUB)(6 DIAMOND)(J CLUB)

Initial deck: (7 HEART)(A SPADE)(10 DIAMOND)(2 CLUB)(6 DIAMOND)(J CLUB)

After shuffle: (7 HEART)(A SPADE)(10 DIAMOND)(2 CLUB)(6 DIAMOND)(J CLUB)

Initial deck: (7 HEART)(A SPADE)(10 DIAMOND)(2 CLUB)(6 DIAMOND)(J CLUB)

After shuffle: (7 HEART)(A SPADE)(10 DIAMOND)(2 CLUB)(6 DIAMOND)(J CLUB)

Initial deck: (7 HEART)(A SPADE)(10 DIAMOND)(2 CLUB)(6 DIAMOND)(J CLUB)

After shuffle: (7 HEART)(A SPADE)(10 DIAMOND)(2 CLUB)(6 DIAMOND)(J CLUB)

Initial deck: (7 HEART)(A SPADE)(10 DIAMOND)(2 CLUB)(6 DIAMOND)(J CLUB)

After shuffle: (7 HEART)(A SPADE)(10 DIAMOND)(2 CLUB)(6 DIAMOND)(J CLUB)

Initial deck: (7 HEART)(A SPADE)(10 DIAMOND)(2 CLUB)(6 DIAMOND)(J CLUB)

After shuffle: (7 HEART)(A SPADE)(10 DIAMOND)(2 CLUB)(6 DIAMOND)(J CLUB)

We clearly see that at every step, which we expect to be done a swap. The only way for this to happen is if every time the random number is the same. The conclusion is that we have a problem with the generation of random numbers. **The random generator does not work.**

We instantly think about taking a look at the documentation of `System.Random()`. On MSD we can read, by creating the constructor `Random()`, a new instance of the generator of pseudo-random numbers with a value, equal to the current system. The documentation we can further read that by creating two or more instances of the class `Random` in relatively short span time, there is a great chance the numbers to the same. It turns out the problem consists in the misuse of the class.

Now being more familiar with the current problem, we could correct it by creating an instance of the class `Random` only at the beginning of the program. After that, if we need a random number, we are going to use the already created generator of pseudo-random numbers. After the correction, the code looks like this:

```csharp
class CardsShuffle
{
    static Random rand = new Random();
```

# 第 23 章 问题解决的方法论

```csharp
static void PerformSingleSwap(List<Card> cards) {
    int randomIndex = rand.Next(1, cards.Count);
    Card firstCard = cards[0];
    Card randomCard = cards[randomIndex];
    cards[0] = randomCard;
    cards[randomIndex] = firstCard;
}
...
```

It seems that the program finally works correctly. At every run the order of the cards is different and looks randomly.

Initial deck: (7 HEART)(A SPADE)(10 DIAMOND)(2 CLUB)(6 DIAMOND)(J CLUB)

After shuffle: (2 CLUB)(A SPADE)(J CLUB)(10 DIAMOND)(7 HEART)(6 DIAMOND)

Initial deck: (7 HEART)(A SPADE)(10 DIAMOND)(2 CLUB)(6 DIAMOND)(J CLUB)

After shuffle: (6 DIAMOND)(10 DIAMOND)(J CLUB)(2 CLUB)(A SPADE)(7 HEART)

We try some other tests and the final result is still correct. Now we can say that we have a correct implementation of our algorithm, which we have designed earlier.

# 第 5 – 控制输入

Now we only need to be able to read the deck from the console so that the user can enter the cards, which need to be shuffled. Notice that we left this step as last. Why? The answer is simple: we do not want to enter the same data at the start of our program just to check whether a piece of code works correctly.

> If the problem involves entering data from the console, leave this as last step and be sure that everything works before implementing the reading of the input. While writing the source code, do your tests with hard-coded examples so that you don’t have to enter any data.

# 使用 C# 的计算机编程基础

一个或同时；是同时或单独输入的面部和颜色。没有什么困难的，把这留给我们的读者吧。

# 数字排序 – 逐步进行

到目前为止，我们已经向你展示了按步骤编写程序是多么重要，在进入下一步之前，你必须确保上一步运行正常。

让我们来看一下数字进行排序的问题。解决这个问题的步骤是相同的。再次强调，解决此任务的正确方法是分步进行。让我们简要看看我们处于哪一个步骤。我们不会编写任何代码，而是将考虑解决方案的主要部分。假设我们使用 `List<int>`，其中我们连续找到最小数字，打印它并从数字列表中删除它。这些是步骤：

- 步骤 1. 构想一个良好的测试数据（示例）。例如数字：7, 2, 4, 1, 8 和 2。我们创建一个 `List<int>` 并用示例中的数字填充它。我们创建一个输出这些数字的方法。

我们编译并测试刚刚编写的代码段。

- 步骤 2. 我们创建一个方法来找到数组中的最小数字并返回其位置。

我们测试负责查找最小数字的方法。我们尝试不同的数字集合以确保搜索工作正常（我们还将最小元素设置在开头、结尾、中间；我们还考虑了最小数字出现多次的情况）。

- 步骤 3. 我们创建一个方法找到最小数字，打印它，然后将其删除。

我们用我们的示例测试该方法是否运行正常。我们还必须用其他示例进行测试。

- 步骤 4. 我们创建一个排序数字的方法。该方法执行 N 次上一个方法（其中 N 是数字的数量）。

我们必须测试一切是否都运行正常。

- 步骤 5. 如果需要输入数据，我们在将主问题分解为更小的问题后实现它。

你看到，这种方法适用于所有任务。我们只需要从一个大问题中找出哪些是较小的问题，并实现它们。每实现一个较小的问题，我们都需要对其进行测试。每一步之后，我们都需要启动程序，以确保到目前为止一切运行完美无缺。通过这种方式，我们能够快速发现错误并进行调试。这比在我们写了大量代码后再尝试调试它们要快得多。

# 测试你的解决方案！

以下内容听起来你熟悉吗：“我已经准备好第一个任务，所以我必须开始下一个。”每个人在考试时都想过这一点。但在编程中，准备好一个任务意味着：

- 1. 我很好地理解了任务描述。
- 2. 我想出了解决该问题的算法。
- 3. 我在纸上测试了我的算法，并确定它是正确的。
- 4. 我对我们需要的数据结构以及我的算法的复杂度进行了思考。
- 5. 我写了一个程序，正确地实现了我的算法。
- 6. 我用合适的示例测试了我的程序，以便我确定一切运行完美无缺，即使在异常情况下也是如此。

缺乏经验的软件开发者经常忘记最后一步。他们认为测试不是他们的工作，这是他们最大的错误。这就像是认为微软不应该测试 Windows 并让它每分钟崩溃一次。

> 测试是程序员职责的重要部分。不测试就编写代码就像不看屏幕在键盘上打字——你认为你写的文本是正确的，但它可能充满了漏洞。

经验丰富的程序员知道，未经测试的代码不是完成的。在大多数软件公司中，不测试你的工作是完全不可接受的。

在软件行业中，广泛流传着观点：对每个代码单元（方法、类和模块）进行单元测试的自动测试。单元测试意味着对于每个程序，我们都创建另一个程序来测试我们的工作。在某些公司中，你首先思考测试场景，构建测试，然后才编写程序。关于单元你需要了解的知识非常多，但随着你深入“软件工程”，你将对它们更加熟悉。现在，我们将关注每个程序员都必须进行的手动测试。单元测试框架和测试自动化可以简化这一过程。

# 如何测试？

如果一个程序可以处理每种输入数据，那么它就能正常工作。测试是一个发现任何类型漏洞的过程。它无法检测程序是否运行完美无缺，但它可以帮助你发现大多数导致错误结果和其他类型错误的漏洞。

遗憾的是，你无法预测所有情况并对它们进行测试。因此，你必须构想涵盖可能发生的大多数情况的示例。

# 计算机编程基础（即最少数量简单测试）

这种方法可以用最小的努力（即最少数量简单测试）来检查程序的所有常见用法情况。如果测试后没有发现漏洞，这并不意味着程序 100% 正确，通过这种方式我们减少了程序在以后阶段崩溃的概率。

> 测试只能发现漏洞的存在。它可以证明一个程序运行完美无缺！经过仔细测试的程序比未测试或未仔细测试的程序漏洞更少。

从我们程序的典型案例开始测试是好的。这通常是我们在纸上测试过的同一个示例，我们的算法可以正确处理该示例。

# 使用良好的示例进行测试

正如已经提到的，从我们程序的典型案例开始测试是好的。这通常是我们在纸上测试过的同一个示例，我们的算法可以正确处理该示例。

# 还要测试什么？

测试纸上画的案例只是第一步。接下来你需要进行一些额外的测试，以确保你的程序运行正常。

# 一个困难的常见情况测试

我们已经对我们的程序测试了一个案例，即我们在纸上写下的案例。我们的程序运行正常。这涵盖了我们程序的一个典型使用场景。

```csharp
foreach (Suit suit in allSuits) {
  Card card = new Card() { Face = face, Suit = suit };
  cards.Add(card);
}
ShuffleCards(cards);
PrintCards(cards);
```

如果我们执行它，返回的结果是：

```
(4 DIAMOND)(2 DIAMOND)(6 HEART)(2 SPADE)(A SPADE)(7 SPADE)(3
DIAMOND)(3 SPADE)(4 SPADE)(4 HEART)(6 CLUB)(K HEART)(5 CLUB)
DIAMOND)(5 SPADE)(A HEART)(9 CLUB)(10 CLUB)(A CLUB)(6 SPADE)(7
CLUB)(7 DIAMOND)(3 CLUB)(9 HEART)(8 CLUB)(3 HEART)(9 SPADE)(4
CLUB)(8 HEART)(9 DIAMOND)(5 SPADE)(8 DIAMOND)(J HEART)(10
DIAMOND)(10 HEART)(10 SPADE)(Q HEART)(2 CLUB)(J CLUB)(J SPADE)(Q
CLUB)(7 HEART)(2 HEART)(Q CLUB)(J DIAMOND)(6 DIAMOND)(K
SPADE)(8 SPADE)(8 SPADE)(A DIAMOND)(Q DIAMOND)(K DIAMOND)
```

如果我们仔细注意，大多数牌仍然在相同的位置。在前 4 张牌之后，洗牌后有一半的牌没有改变位置：2♦ 和 2♠。

在程序中发现 bug 永远都不为晚，我们唯一的方法就是用一副真正的 52 张扑牌进行测试，不是吗？在实际情况下进行测试是有用的。我们发现了一个无法修复的严重 bug。

如何修复这个问题？我们想到的第一个想法是进行单次交换（显然 N 次是不够的）。另一个想法是在第 N 次单次交换时，将牌中的第 N 张牌与一张随机牌进行交换，而不是与第一张牌交换。这样我们就能保证每张牌都会被交换。第二个主意更好。让我们来实现它。我们在代码中添加了以下 Swap 更改：
