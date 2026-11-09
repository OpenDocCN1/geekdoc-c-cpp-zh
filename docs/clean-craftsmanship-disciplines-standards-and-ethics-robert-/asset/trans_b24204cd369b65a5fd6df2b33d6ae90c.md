

```java
        factors.add(n);
    }
    return factors;
}
```

在这一点上，你完全有理由指责我只是随手塞了几个 `if` 语句来让测试通过。这离事实并不远。你也可能指责我违反了规则 5，因为这段时间的代码谈不上什么通用性。但另一方面，我确实看不到其他的选择。

不过，这其中有通用化即将到来的蛛丝马迹。请注意，这两个 `if` 语句的谓词完全相同。它们几乎就像是某个被展开的循环的一部分。事实上，第二个 `if` 语句完全没理由非得放在第一个 `if` 里面。

点击此处查看代码图片

```java
private List<Integer> factorsOf(int n) {
    ArrayList<Integer> factors = new ArrayList<>();
    if (n > 1) {
        if (n % 2 == 0) {
            factors.add(2);
            n /= 2;
        }
    }
    if (n > 1)
        factors.add(n);
    return factors;
}
```

这段代码能通过测试，而且看起来*非常*像是被展开的循环。

接下来的三个测试无需任何修改即可通过：

点击此处查看代码图片

```java
assertThat(factorsOf(5), contains(5));
assertThat(factorsOf(6), contains(2, 3));
assertThat(factorsOf(7), contains(7));
```

这很好地表明我们走在了正确的方向上，也让我对那些丑陋的 `if` 语句感觉好了不少。

下一个最退化的测试是 8，它必然会失败，因为我们的解决方案代码根本不可能把三个数字放进列表里：

```java
n /= 3;
}
}
if (n > 1)
    factors.add(n);
return factors;
}
```

但这太可怕了。它不仅严重违反了规则 5，而且造成了大量的代码重复。我甚至不确定哪种违规更糟糕！

而正是在这里，通用化的咒语开始发挥作用：

> 随着测试变得越来越具体，代码变得越来越通用。

我们写的每一个新测试都让测试套件变得更具体。每当我们调用规则 5，解决方案代码就变得更通用。我们稍后会回到这条咒语。事实证明，它对测试设计以及防止脆弱测试至关重要。

我们可以通过把原始的因式分解代码放进一个循环中来消除重复和规则 5 的违反：

点击此处查看代码图片

```java
private List<Integer> factorsOf(int n) {
    ArrayList<Integer> factors = new ArrayList<>();
    int divisor = 2;
    while (n > 1) {
        while (n % divisor == 0) {
            factors.add(divisor);
            n /= divisor;
        }
        divisor++;
    }
    if (n > 1)
        factors.add(n);
    return factors;
}
```

再说一次，如果你看了视频，你会发现这一步是通过好几个步骤完成的。第一步是把三个 2 提取到 `divisor` 变量中。下一步是引入 `divisor++` 语句。然后把 `divisor` 变量的初始化移到 `if` 语句之上。最后，把 `if` 改成了 `while`。

这种从 `if` 到 `while` 的转变又出现了。你注意到原 `if` 语句的谓词恰好变成了外层 `while` 循环的谓词吗？我觉得这非常令人吃惊。这里面似乎有某种遗传性的东西。就好像我一直试图创造的那个生物，是从一颗简单的种子开始，通过一系列微小的突变逐渐进化而来的。

注意，底部的 `if` 语句已经变得多余了。循环唯一能终止的方式就是 n 等于 1。那个 `if` 语句实际上就是一个被展开的循环的终止条件！

点击此处查看代码图片

```java
private List<Integer> factorsOf(int n) {
    ArrayList<Integer> factors = new ArrayList<>();
    int divisor = 2;
    while (n > 1) {
        while (n % divisor == 0) {
            factors.add(divisor);
            n /= divisor;
        }
        divisor++;
    }
    return factors;
}
```

只需要一点点重构，我们就得到这样的代码：

点击此处查看代码图片

```java
private List<Integer> factorsOf(int n) {
    ArrayList<Integer> factors = new ArrayList<>();

    for (int divisor = 2; n > 1; divisor++)
        for (; n % divisor == 0; n /= divisor)
            factors.add(divisor);

    return factors;
}
```

推导那些能够解决*可以*解决的问题的算法的一般过程。

- 3. 这就是希尔伯特的“判定问题”。他问的是，是否存在一种通用的方法，能够证明任何给定的丢番图方程都是可解的。丢番图方程是一种输入和输出都是整数的数学函数。计算机程序也是一种输入和输出都是整数的数学函数。因此，希尔伯特的问题可以被描述为与计算机程序相关的问题。

## 保龄球游戏

1999 年，鲍勃·科斯和我在一次 C++ 会议上相遇。我们有一些空闲时间，于是决定练习一下 TDD 这个新想法。我们选择了计算保龄球比赛得分这个简单问题。

一场保龄球比赛由十轮组成。在每一轮中，球员有两次机会将球滚向十个木瓶，试图将它们击倒。一个球击倒的木瓶数就是该球的得分。如果第一个球就击倒了全部十个木瓶，这被称为*全中*。如果击倒全部十个木瓶需要用两个球，则被称为*补中*。可怕的滚沟球（图 2.3）则一分不得。

![](img/7b01f9dd5d5d33f16ee27a44427cd56e_93_0.png)

**图 2.3** 臭名昭著的滚沟球

计分规则可以简洁地表述如下：

- 如果一轮是全中，得分为 10 分加上接下来两次投球的得分。
- 如果一轮是补中，得分为 10 分加上下一次投球的得分。
- 否则，得分为这一轮两次投球的得分之和。

图 2.4 中的计分表是一场典型（如果说有点古怪的话）的比赛。

| 轮次 | 第一次投球 | 第二次投球 | 第三次投球 | 累计得分 |
|---|---|---|---|---|
| 1 | 1 | 4 | — | 5 |
| 2 | 4 | 5 | — | 14 |
| 3 | 6 | / | — | 29 |
| 4 | 5 | / | — | 49 |
| 5 | X | — | — | 60 |
| 6 | 0 | 1 | — | 61 |
| 7 | 7 | / | — | 77 |
| 8 | 6 | / | — | 97 |
| 9 | X | — | — | 117 |
| 10 | 2 | / | 6 | 133 |

![](img/7b01f9dd5d5d33f16ee27a44427cd56e_95_0.png)

**图 2.5 保龄球计分的 UML 图**

`Game` 有十个 `Frame`。除 `TenthFrame` 子类外，每个 `Frame` 都有一到两次 `Roll`，而 `TenthFrame` 继承 `1..2` 并添加一次投球，使其变为 `2..3`。每个 `Frame` 对象都指向下一个 `Frame`，这样 `score` 函数就可以在需要计算补中或全中时向前查看。

`Game` 有两个函数。`roll` 函数在球员每次投球时被调用，并传入球员击倒的木瓶数。`score` 函数在所有球都投完后被调用，返回整场比赛的得分。

这是一个漂亮而简单的面向对象模型。编写代码应该相当容易。事实上，如果有一个四人团队，我们可以把工作分成四个类，然后大约一天后汇合，集成并让它们工作起来。

或者，我们也可以使用 TDD。如果你能观看视频，现在就应该去看。无论如何，请仔细阅读下面的文字。

观看相关视频：保龄球游戏

在 [informit.com/register](http://informit.com/register) 注册以访问视频

我们一如既往地从一个什么都不做的测试开始，只是为了证明我们能编译和运行。这个测试运行通过后，我们把它删掉：

点击此处查看代码图片

```java
public class BowlingTest {
  @Test
  public void nothing() throws Exception {
  }
}
```

接下来，我们断言可以创建 `Game` 类的实例：

点击此处查看代码图片

```java
@Test
public void canCreateGame() throws Exception {
  Game g = new Game();

}
```

然后我们通过让 IDE 创建缺失的类来使它编译并通过：

```java
public class Game {
}
```

接下来，我们看看能否投一个球：

点击此处查看代码图片

```java
@Test
public void canRoll() throws Exception {
  Game g = new Game();
  g.roll(0);
}
```

然后我们通过让 IDE 创建 `roll` 函数来使它编译并通过，并给参数起一个合理的名字：

点击此处查看代码图片

```java
public class Game {
  public void roll(int pins) {
  }
}
```

