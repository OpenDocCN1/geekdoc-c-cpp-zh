

peg上有若干个大小不同的盘子，盘子上都有孔可以套在peg上。你在游戏中要遵循两条规则将盘子从一个peg移到另一个peg：

- 1. 一次只能移动一个盘子。
- 2. 不能把一个盘子放在比它小的盘子上。

我们想写一个程序来解决这个问题。为此，我们需要先对问题进行更深入的分析。

如果你先想象一个peg上堆着7个盘子，从底部最大到顶部最小，然后试图想象解法，你可能会觉得很困难。第一步显然是把顶部的盘子移到另一个peg上，但移到哪一个呢？之后会变得更复杂。与其试图解决一个难题，我们应该从一个简单问题开始，然后逐步构建。

最容易解决的设置是只有一个盘子时。只需将盘子从起始位置移到你想要它结束的peg上。这有点太 trivial 了，那么两个盘子呢？首先你必须把上面的盘子移到你不想结束的peg上，然后把第二个盘子移到目标peg，再把较小的盘子移到它上面。到目前为止可能还不明显，但这指向了一个通用解法。为了看清这一点，想想三个盘子的情况。我们可以逐一列出每一步的移动，但我们刚刚看到了如何移动两个盘子，所以我们可以假设我们知道怎么做。利用这一点，我们把两个盘子移到中间peg。注意，我们并不是字面意义上一次移动两个盘子，因为那样会违反规则。相反，我们使用刚刚开发的方法，用三次单盘移动来移动两个盘子。然后把最大盘子移到目标peg，再把两个盘子移到它上面。

这指向了一个通用解法。如果我们假设我们知道如何移动 N-1 个盘子，我们就可以通过先把上面的 N-1 个盘子移到备用peg，然后把最大盘子移到目的地，最后把 N-1 个盘子移回最大盘子顶部来移动 N 个盘子。注意这是一个递归定义。N 个盘子的解法依赖于 N-1 个盘子的解法。基本情况是平凡的，即移动单个盘子。

我们现在有了解决这个问题的思路。接下来需要弄清楚如何在计算机内存中表示这个问题。我们需要想出一种表示盘子和peg的方法。对于盘子，我们真正关心的只是盘子的大小。这可以用一个 Int 很好地表示。一个peg本质上只是一个盘子堆，所以我们需要类似 Array 或 List of Ints 的东西。为了决定用哪一个，我们应该考虑它们的使用方式。peg上的盘子数量会随时间变化，但它们总是从一个位置添加或移除，即堆的顶部。这指向使用一个 List，其中 List 的 head 是顶部的盘子。我们可以用 :: 把一个盘子添加到peg上，tail 就是移除盘子后剩下的部分。下面的脚本展示了代码如何将三个peg实现为 Array[List[Int]]。有一个移动一个盘子的函数，其中包含检查以确保我们没有违反第二条规则。

```
val num = if(args.length>0) args(0).toInt else 7
val pegs = Array(List.tabulate(num)(i => i+2), List[Int](), List[Int]())
```

```
def moveDisk(from:Int,to:Int) {
  require(pegs(to).isEmpty || pegs(from).head < pegs(to).head)
  pegs(to) = pegs(from).head :: pegs(to)
  pegs(from) = pegs(from).tail
}
```

```
def moveNDisks(n:Int,from:Int,to:Int) {
```

```
val other = 3-from-to
if(n==1) {
    moveDisk(from, to)
} else {
    moveNDisks(n-1, from, other)
    moveDisk(from, to)
    moveNDisks(n-1, other, to)
}
}

moveNDisks(pegs(0).size, 0, 2)
```

```
println(pegs.map(a => a.mkString(" ")).mkString("\n"))
```

函数 moveNDisks 是递归的并且依赖于 moveDisk 函数，所以我们可以确信程序没有作弊。行 val other = 3-from-to 最初看起来可能有点奇怪。该函数只传入要移动的peg编号和要移动到的peg编号，但函数中必须引用第三个peg，因为那是上面 n-1 个盘子要先去的地方。那一行使用简单的观察计算出其他peg的编号，即所有peg的索引相加为 3。脚本以调用 moveNDisks 函数结束，然后打印最后剩下的内容。这使得验证拼图是否真正被解决变得简单。

鉴于汉诺塔的物理和视觉特性，文本打印有点不令人满意。这是一个真正值得图形显示的问题。下面的脚本添加了一个 BufferedImage、一个 Panel 和一个 Frame，这样你就可以在递归解决拼图时观看盘子的移动。

```
import scala.swing._
import java.awt.image.BufferedImage
import java.awt.{Graphics2D,Color}

val num = if(args.length>0) args(0).toInt else 7
val pegs = Array(List.tabulate(num)(i => i+2), List[Int](), List[Int]())

val img = new BufferedImage(600, 300, BufferedImage.TYPE_INT_ARGB)
val g = img.createGraphics

val panel = new Panel {
    preferredSize = new Dimension(img.getWidth, img.getHeight)
    override def paint(g:Graphics2D) {
        g.drawImage(img, 0, 0, null)
    }
}
```

```
def renderPegs {
    g.clearRect(0, 0, img.getWidth, img.getHeight)
    g.setPaint(Color.red)
    for(i <- 0 until pegs.length) {
        for(j <- 0 until pegs(i).length) {
            val s=pegs(i)(j)*10
            g.fillRect(100+i*200-s/2,
                       img.getHeight-(pegs(i).length-j)*30, s, 20)
        }
    }
    panel.repaint()
```

```
Thread.sleep(100)
}

def moveDisk(from:Int,to:Int) {
    require(pegs(to).isEmpty || pegs(from).head < pegs(to).head)
    pegs(to) = pegs(from).head :: pegs(to)
    pegs(from) = pegs(from).tail
    renderPegs
}

def moveNDisks(n:Int,from:Int,to:Int) {
    val other = 3-from-to
    if(n==1) {
        moveDisk(from, to)
    } else {
        moveNDisks(n-1, from, other)
        moveDisk(from, to)
        moveNDisks(n-1, other, to)
    }
}

val frame=new MainFrame {
    title="Hanoi"
    contents=panel
    resizable=false
}

frame.visible=true

moveNDisks(pegs(0).size, 0, 2)

println(pegs.map(a => a.mkString(" ")).mkString("\n"))
```

如果你稍微修改一下这段代码，你会注意到高堆的盘子移动需要很长时间。这就引出了一个问题：要把 N 个盘子从一个peg移到另一个peg需要多少次移动？递归代码使得这个问题相当容易回答，如果我们对递归函数作为答案感到满意的话。

f(N) = 1                     N = 1
       1 + 2 * f(N - 1)   otherwise

这可以简化为 f(N) = 2^N - 1。所以移动次数在盘子数量上呈指数增长。20 或 30 个盘子的堆确实需要很长时间才能完成。

## 15.5 迷宫

另一个需要递归的问题类别是涉及迷宫的问题。这可能也看起来更像是娱乐，但迷宫是被称为图的一种简化情况，图在计算机科学中非常重要，并用于表示各种各样的问题。我们在这里为迷宫使用的相同方法同样适用于图。

还有许多应用，其中执行诸如在某种受限路径如迷宫中寻找最优路线之类的操作是重要的。

为了保持简单，我们将使用一种相当基础的方法来构建迷宫。与其在单元格之间有墙的网格，我们将有一个网格，其中完整的方块要么是开放的，要么被墙占据。这种表示意味着我们可以使用一个 2-D Array 的值来告诉我们是否有墙。理论上我们可以用 Array[Array[Boolean]] 来实现此目的，但在实践中我们将使用能够在“房间”中放置数值，所以 Array[Array[Int]] 会更实用。

我们将用类似以下的代码定义迷宫。

```
val maze=Array(Array( 0, 0, 0, 0, 0, 0, 0, 0, 0, 0),
    Array(-1,-1,-1, 0,-1,-1,-1,-1,-1,-1),
    Array( 0, 0, 0, 0,-1, 0, 0, 0,-1, 0),
    Array( 0,-1, 0,-1,-1,-1,-1, 0, 0, 0),
    Array( 0,-1, 0,-1, 0, 0,-1,-1,-1, 0),
    Array( 0,-1,-1,-1,-1, 0, 0, 0, 0, 0),
    Array( 0,-1, 0, 0,-1, 0,-1,-1,-1, 0),
    Array( 0, 0, 0,-1,-1, 0, 0, 0, 0, 0),
    Array( 0,-1, 0,-1,-1, 0,-1, 0,-1,-1),
    Array( 0,-1, 0, 0, 0, 0,-1, 0, 0, 0))
```

这构建了一个 Ints 的 2-D Array，使用 0 表示开放方块，使用 -1 表示墙。使用 -1 表示墙是有意为之，这样正数以后就可以用来表示其他东西。这个特定迷宫的大小只有 10x10。这对于我们的目的来说是一个很好的起点，尽管它不允许非常复杂的迷宫。

我们的第一个任务是大多数人可能想对迷宫做的事情。我们想知道如何以最少的步数穿过它。首先，我们将问一个简单的问题：最短路径有多长。这比试图实际返回一条路径有显著优势。不仅它是一个简单的数值，而且还是唯一的。可以有多条路径长度相同。如果我们要求最优路径，这会产生歧义。它也恰好是，拥有一个函数来查找最短路径的长度是足够的，因为对该函数的多次调用可以用来构建最优路径，即使这种构造效率不高。

你可以用循环写一个函数来查找最短路径的长度，但代码相当复杂。我们可以用递归写一个更简单的解法。和所有递归函数一样，我们可以将解法分解为两个主要部分，基本情况和递归情况。基本情况应该很容易解决。对于迷宫问题，有两个很好的基本情况。一个基本情况是到达出口时。如果你在出口处，出来需要零步。另一个基本情况是检查的位置在迷宫之外或在墙内。对于这种情况，我们希望返回一个不可能成为解的值。我们在讨论递归情况后会再回来讨论这个问题。

想象你站在迷宫中的某个位置，想要知道从当前位置到出口的最短路径需要多少步。递归的方法是想象你有一个神谕，它可以告诉你从任何相邻方格的答案，并弄清楚你将如何结合这些值来确定你所在位置的距离。正如我们在本章前面所说，我们通过假设有一个可工作的函数并基于该假设编写来编写递归函数。一旦完成，假设我们正确处理了情况，它就会工作。神谕就是我们假设的可工作函数。如果你身处迷宫中，并且可以询问神谕从北、南、东、西一步之遥的地方出来需要多少步，你将如何利用这些信息来确定你所在位置的最短距离？

