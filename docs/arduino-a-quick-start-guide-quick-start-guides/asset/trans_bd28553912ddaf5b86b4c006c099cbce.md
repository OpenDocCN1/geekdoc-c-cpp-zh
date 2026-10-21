

![](img/dcfd13a1bf99c4d3f9996627012a6526_70_0.png)

Figure 3.7: A first working version of our binary die

## More LEDs, Dice, and Cubes

制作二进制骰子很有趣，而且即使对初学者来说也是一个容易的项目。但反过来呢——读取真正的骰子？Steve Hoefer* 使用 Arduino 制作了一个骰子读取器，效果非常令人印象深刻。他使用五对红外发射器和接收器来“扫描”骰子的表面。这是一个相当高级的项目，你可以从中学到很多东西。

另一个有趣的项目是 LED 立方体：由 LED 组成的立方体。† 控制超过几个 LED 看起来出乎意料地困难，但你可以产生惊人的效果。

这就是实现二进制骰子第一版所需的所有代码。像往常一样，我们为 LED 连接的输出引脚定义了一些常量。在 setup() 函数中，我们将所有引脚设置为 OUTPUT 模式。对于骰子，我们需要在 1 到 6 之间需要随机数。random() 函数使用伪随机数生成器在指定范围内返回随机数。在第 10 行，我们使用从模拟输入引脚 A0 读取的一些噪声来初始化生成器（请参阅下一页的边栏，了解我们为什么必须这样做）。你可能会想知道常量 A0 从何而来。自版本 19 以来，Arduino IDE 为所有模拟引脚定义了名为 A0、A1 等的常量。

然后我们实际生成 1 到 6 之间的新随机数，并使用 output_result() 函数输出它。 （对 random() 的调用中的 7 是正确的，因为它期望上限加一）。

函数 output_result() 接收一个数字并通过相应地打开或关闭我们的三个 LED 输出其低三位。这里我们使用 & 运算符和二进制字面量。& 运算符接收两个数字并按位组合它们。当两个对应的位都是 1 时，& 运算符的结果也是 1。否则为 0。B 前缀允许你直接将二进制数字放入源代码中。例如，B11 与 3 相同。

你可能已经注意到 loop() 函数被留空了，你可能会想知道这样的骰子是如何工作的。很简单：每当你重新启动 Arduino 时，它就会输出一个新数字，要再次掷骰子，你必须按下复位按钮。

## Generating Random Numbers

一些计算问题出乎意料地困难，创建良好的随机数就是其中之一。毕竟，计算机最重要的属性之一是确定性行为。尽管如此，我们经常需要——至少看似——为各种目的提供随机行为，从游戏到加密算法。

最流行的方法（例如 Arduino 的 random() 函数使用的方法）是创建伪随机数。* 它们看起来是随机的，但实际上是公式的结果。存在不同种类的算法，但通常每个新的伪随机数都是从其前驱计算得出的。这意味着你需要一个初始化值来创建序列中的第一个随机数。这个初始化值称为随机种子，为了创建伪随机数的不同序列，你必须使用不同的随机种子。

创建伪随机数很便宜，但如果你知道算法和随机种子，你可以轻松预测它们。所以，你不应该将它们用于加密目的。

在现实世界中，你可以找到无数个随机过程，并且使用 Arduino 很容易测量它们以创建真正的随机数。通常，读取模拟引脚 0 上的一些随机噪声并将其作为随机种子传递给 randomSeed() 函数就足够了。你也可以使用这种噪声来创建真正的随机数；甚至有一个用于此目的的库。†

如果需要强随机数，Arduino 是创建它们的完美设备。你可以找到许多仅为创建随机数而观察自然过程的项目。其中一个例如使用 Arduino 观察沙漏。‡

* http://en.wikipedia.org/wiki/Pseudo-random_numbers
† http://code.google.com/p/tinkerit/wiki/TrueRandom
‡ http://www.circuitlake.com/usb-hourglass-sand-timer.html

编译代码，将其上传到 Arduino，并用你的二进制骰子玩一会儿。你已经掌握了你的第一个高级电子项目！好好享受一下！

所以，每当你想看到新结果时，你都必须重置 Arduino。这可能是你可以构建的最实用的用户界面，对于第一个原型来说，这是可以的。但通常你需要不止一个按钮，而且无论如何添加自己的按钮也更优雅。所以，我们将在下一节中这样做。

## 3.5 Working with Buttons

在本节中，我们将为我们的二进制骰子添加自己的按钮，这样我们就不再需要滥用 Arduino 的复位按钮来掷骰子了。我们从小处着手，构建一个使用按钮控制单个 LED 的电路。

那么，按钮到底是什么？以下是可用于 Arduino 复位按钮的典型按钮的三个视图。

![](img/dcfd13a1bf99c4d3f9996627012a6526_73_0.png)

它有四个连接器，可以完美地安装在面包板上（至少在你用钳子将其拉直之后）。当按钮被按下时，相对的两个引脚会连接；否则，它们是断开的。

在下一页的图 3.8 中，你可以看到一个使用按钮的简单电路。将引脚 7（完全任意选择）连接到按钮，并通过 10kΩ 电阻将按钮连接到地。然后将 5 伏电源连接到按钮的另一端。

总的来说，这种方法似乎很直接，但为什么我们还需要一个电阻呢？问题是我们期望按钮在未按下时返回默认值（LOW）。但当按钮未按下时，它不会直接连接到地，并且会因静电和干扰而闪烁。有一点电流流过电阻，这有助于防止随机噪声改变输入引脚看到的电压。

![](img/dcfd13a1bf99c4d3f9996627012a6526_74_0.png)

# Figure 3.8: A simple pushbutton circuit

当按钮被按下时，Arduino 的数字引脚上仍会有 5 伏电压，但当按钮未按下时，它会干净地读取到地的连接。我们称之为下拉电阻；上拉电阻则完全相反。也就是说，你必须通过按钮将 Arduino 的信号引脚连接到电源，并使用电阻将按钮的另一端连接到地。

现在我们已经消除了所有这些丑陋不稳定的现实世界行为，我们可以回到稳定而舒适的软件开发世界。下面的程序检查按钮是否被按下并相应地点亮 LED：

Download BinaryDice/SimpleButton/SimpleButton.pde

```
const unsigned int BUTTON_PIN = 7;
const unsigned int LED_PIN   = 13;

void setup() {
  pinMode(LED_PIN, OUTPUT);
  pinMode(BUTTON_PIN, INPUT);
}

void loop() {
  const int BUTTON_STATE = digitalRead(BUTTON_PIN);

  if (BUTTON_STATE == HIGH)
    digitalWrite(LED_PIN, HIGH);
  else
    digitalWrite(LED_PIN, LOW);
}
```

我们将按钮连接到引脚 7，将 LED 连接到引脚 13，并在 setup() 函数中相应地初始化引脚。在 loop() 中，我们读取连接到按钮的引脚的当前状态。如果它是 HIGH，我们打开 LED。否则，我们关闭它。

将程序上传到 Arduino，你会看到只要按下按钮，LED 就亮。松开按钮后，LED 就熄灭。这很酷，因为现在我们几乎拥有控制骰子的所有所需内容，使用我们自己的按钮。但在继续之前，我们将稍微增强我们的示例，并将按钮变成真正的电灯开关。

要构建电灯开关，我们从最简单的解决方案开始。不要更改当前电路，并将以下程序上传到你的 Arduino：

```
```
const unsigned int BUTTON_PIN = 7;

const unsigned int LED_PIN  = 13;

void setup() {
  pinMode(LED_PIN, OUTPUT);
  pinMode(BUTTON_PIN, INPUT);
}

int led_state = LOW;

void loop() {
  const int CURRENT_BUTTON_STATE = digitalRead(BUTTON_PIN);
  
  if (CURRENT_BUTTON_STATE == HIGH) {
    led_state = (led_state == LOW) ? HIGH : LOW;
    digitalWrite(LED_PIN, led_state);
  }
}
```
```

我们以通常的引脚常量开始，并在 setup() 中设置我们使用的引脚的模式。在第 9 行，我们定义了一个名为 led_state 的全局变量来存储我们 LED 的当前状态。当 LED 打开时它将为 LOW，否则为 HIGH。在 loop() 中，我们检查按钮的当前状态。当我们按下按钮时，其状态切换为 HIGH，我们切换 led_state 的内容。也就是说，如果 led_state 为 HIGH，我们将其设置为 LOW，反之亦然。最后，我们将物理 LED 的状态设置为我们当前的软件状态。

我们的解决方案非常简单，但不幸的是，它不起作用。稍微玩一下，你很快就会注意到一些令人讨厌的行为。

