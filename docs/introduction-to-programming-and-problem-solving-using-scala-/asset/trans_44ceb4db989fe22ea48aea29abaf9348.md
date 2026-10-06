

# 面向对象

```scala
branch.addAccount(account1)
val account2 = Account(customer, Account.Savings)
branch.addAccount(account2)
}
```

这段代码目的是说明如何使用其他类和对象。

为了运行这些代码，我们必须首先使用 `scalac` 进行编译。如果当前目录中只有这些 Scala 文件，你可以使用 `scalac *.scala` 来编译它们。如果你当前目录下有其他 Scala 文件，特别是如果你有无法用 `scalac` 正常编译的脚本文件，则必须单独指定文件。可以通过类似 `scalac Account.scala Customer.scala BankBranch.scala` 的命令来实现。一旦编译了这些文件，你就可以 `scalac BankBranch` 来运行主程序。注意，这个命令没有 `.scala` 后缀，这与我们在运行脚本时采用的方法不同。

# 16.5 实现 Pac-Man™ 示例

与示例类似，我们的 Pac-Man 版本是作为一个应用程序编写，并分布在多个文件中。并不是所有内容都完全遵循章节开头规划的设计。这是预料之中的。当你去实现自己的设计时，通常会发现遗漏的内容，或者意识到某些部分无法以你预期的方式组合。在这种情况下，我们在设计演示和本节之间还引入了一些 Scala 概念，这些概念改变了我们构建构建。

我们首先查看 `Game`，它被实现为一个单例对象（singleton object），并有一个用于运行程序的 `main` 方法。`main` 方法包含了 GUI 的 ScalaFX 代码、一个让代码运行的定时器，以及处理键盘输入的处理器。

> 列表 16.5: Game.scala

```scala
import scalafx.Includes.
import scalafx.animation.
import scalafx.application.
import scalafx.scene.
import scalafx.scene.canvas.
import scalafx.scene.input.
import scalafx.scene.paint.

object Game {
    var Width = 760
    var Height = 840

    private var _lives = 3
    private var _score = 0

    def lives = _lives
    def score = _score
    def newLife():Unit = {
        _lives -= 1
    }
```

```scala
val maze = new Maze
```

```scala
def main(args:Array[String]):Unit = {
  val app = new JFXApp
  stage = new JFXApp.PrimaryStage
    title = "PacMan"
    scene = new Scene(Width, Height)
    var canvas = new Canvas(Width, Height)
    var gc = canvas.graphicsContext2D

  onKeyPressed = (e:KeyEvent) => {
    case Code.Left => maze.player.goLeft
    case Code.Right => maze.player.goRight
    case Code.Up => maze.player.goUp
    case Code.Down => maze.player.goDown
    case _ =>
  }
}

var lastTime = 0
var delay = (t-lastTime)/1e9
if (lastTime < 0 && delay > 0.1) {
  score += maze.updateAll()
  Renderer.render(gc, maze)
  lastTime = t-(delay-0.1)*1000000000.toInt
  if (lastTime == 0) lastTime = t
  if (lives < 0 || maze.pelletCount==0) timer.stop
}

timer.start
}
  
app.main(args)
```

第 10-22 行是基础声明，即该类型的实例。在第 24-61 行的 `main` 方法中，我们使用了 `JFXApp` 和标准的设置。大部分内容在第 11 章和第 12 章应该很熟悉。看起来奇怪的逻辑是第 50 行。在早期的示例中，我们会直接设置 `lastTime = t`。在这个示例中，我们让“游戏跳动”在发布后 0.1 秒左右发生。定时器会在达到 0.1 秒之前触发多次，并且经常会达到 0.115 左右的值。在那种情况下，简单的形式会导致时间“漂移” 0.015 秒。这看起来可能不多，但对于我们期望的 0.1 秒来说这是一个很大的比例。第 50 行的额外数学计算将 `lastTime` 设置为 0.1 秒时，而不是我们可能超出的多少，这样整个游戏就能保持接近同步。第 53 行显示了当玩家耗尽生命时停止定时器的条件，值得注意的是，虽然我们一次展示一个文件，但并不是这样编写的。开发是在一个文件之间移动的，并且随着功能的添加再次移动。这种方法不仅有助于逻辑，也有助于完成工作。你应该经常运行程序以确保它工作正常。在拥有当前状态之前，不要继续下一个功能。专注于单一任务可能具有挑战性，但对流程非常有帮助。接下来是 `Maze`，它被声明为类（class）。该类不接受任何参数，因为它设置了默认配置。第 4-9 行声明了一些私有变量，并将它们设置为默认值，但第 11-12 行声明了 `initMap` 和 `initContents` 方法来获取这些值。代码早期的迭代在声明处设置了这些值，但能够单独指定它们是有帮助的。

```scala
import scalafx.paint.Color
class Maze {
  private var cells:Array[Int] = null
  private var _player:PacMan = null
  private var _ghosts:List[Ghost] = Nil
  private var _fruit:Option[Fruit] = None
  private var count = 0
  private var nextFruitType = 0

  initMap()
  initContents()

  private def initMap():Unit = {
    cells = Array(0,0,0,0,0,0,0,0,0,0,0),
    Array(0,1,1,1,1,1,1,1,1,1,0),
    Array(0,2,0,0,1,0,1,0,0,2,0),
    Array(0,1,1,1,1,1,1,1,1,1,0),
    Array(0,1,0,1,1,1,1,0,1,1,0),
    Array(0,1,1,1,1,1,1,1,1,1,0),
    Array(0,0,0,0,1,0,1,0,3,0,0),
    Array(0,0,0,0,1,0,3,3,3,1,0),
    Array(0,0,0,0,3,3,0,-1,0,3,0),
    Array(3,3,3,3,3,3,3,0,3,3,3),
    Array(0,0,0,0,3,3,0,0,0,3,0),
    Array(0,0,0,1,0,3,3,3,3,1,0),
    Array(0,1,1,1,1,1,1,1,1,1,0),
    Array(0,1,0,1,1,0,0,0,1,1,0),
    Array(0,2,1,1,1,1,1,1,1,2,0),
    Array(0,1,0,1,1,0,0,0,1,1,0),
    Array(0,1,1,1,1,1,1,1,1,1,0),
    Array(0,0,0,0,0,0,0,0,0,0,0))
  }

private def initContents():Unit = {
  _player = new PacMan(9, 15, -1)
  _ghosts = List(new Ghost(9, 7, 1, 0, Color.Red),
    new Ghost(8, 9, 1, -50, Color.Cyan),
    new Ghost(9, 9, 0, -25, Color.Pink),
    new Ghost(10, 9, 3, -75, Color.Orange))

  _fruit = None
  count = 0
  nextFruitType = 0
}

def player = _player
def ghosts = _ghosts
def fruit = _fruit

def rows = cells.length
def columns = cells(0).length

def cell(x:Int, y:Int):Int = {
  if (y < 0 || y >= cells.length || x < 0 || x >= cells(y).length) 
    -1
  else cells(y)(x)
}

def updateAll():Int = {
  // Logic goes here
  0
}
```

