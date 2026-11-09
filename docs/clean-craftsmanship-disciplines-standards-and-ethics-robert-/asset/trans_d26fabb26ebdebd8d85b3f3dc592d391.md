

![](img/7b01f9dd5d5d33f16ee27a44427cd56e_148_0.png)

**图 3.6 模拟对象**

*模拟对象*是一个间谍对象。它会返回测试专用的值，以便驱动被测系统沿着期望的路径运行，并且它会记住对它执行过的操作。然而，模拟对象还知道应该预期什么，并会基于这些预期让测试通过或失败。

![](img/7b01f9dd5d5d33f16ee27a44427cd56e_151_0.png)

**图 3.7 假对象**

很久以前，在 20 世纪 70 年代末，我曾为一家公司工作，这家公司构建了一套安装到电话公司设施中的系统。这个系统用于测试电话线路。服务中心有一台中央计算机，它通过调制解调器链路与我们安装在交换局中的计算机通信。服务中心的那台计算机被称为 SAC（服务区

```
    dialog.show();
    boolean success = dialog.submit("user", "good password");
    assertTrue(success);
}
```

这两个测试使用同一个 `FakeAuthenticator`，但向它传入不同的密码。测试预期*错误密码*会使登录尝试失败，而*正确密码*会成功。

`FakeAuthenticator` 的代码应该很容易想象：

[点击此处查看代码图像](#)

```java
public class FakeAuthenticator implements Authenticator {
    public Boolean authenticate(String username, String password)
    {
        return (username.equals("user") &&
                password.equals("good password"));
    }
}
```

假对象的问题在于，随着应用程序增长，总是会有更多条件需要测试。因此，假对象往往会随着每一个新测试条件而增长。最终，它们可能变得如此庞大和复杂，以至于它们自己也需要测试。

我很少编写假对象，因为我不相信它们不会膨胀。

## TDD 不确定性原理

使用模拟还是不使用模拟，这是一个问题。其实不是。真正的问题是*何时*使用模拟。

关于这一点有两种思想学派：伦敦学派和芝加哥学派，本章末尾会讨论它们。但在深入讨论之前，我们需要先明确为什么这首先会成为问题。它之所以成为问题，是因为*TDD 不确定性原理*。

为了帮助我们理解这一点，我想请你容许我玩味地“走向极端”一下。下面的内容并不是你真正会去做的事情，但它很好地说明了我试图表达的观点。

想象一下，我们想用 TDD 编写一个函数，用来计算以弧度表示的角度的三角正弦值。第一个测试是什么？

记住，我们喜欢从最退化的情况开始。让我们测试能够计算零的正弦值：

[点击此处查看代码图像](#)

```java
public class SineTest {
    private static final double EPSILON = 0.0001;
    @Test
    public void sines() throws Exception {
        assertEquals(0, sin(0), EPSILON);
    }

    double sin(double radians) {
        return 0.0;
    }
}
```

现在，如果你提前思考，这应该已经让你感到不安了。这个测试除了 `sin(0)` 的值之外，没有约束任何东西。

我这么说是什么意思？我的意思是，我们使用 TDD 编写的大多数函数都受到不断增长的测试集的强烈约束，以至于到了某个时刻，函数会通过我们能提出的任何其他测试。我们在质因数示例和保龄球游戏示例中看到了这一点。每个测试都缩小了可能解的范围，直到最终解变得已知。

但在这里，`sin(r)` 函数看起来并不是那样运作的。`sin(0) == 0` 的测试是正确的，但它似乎并没有把解约束到那一个点之外。

当我们尝试下一个测试时，这一点会变得更加明显。那个测试应该是什么？为什么不试试 sin(π)？

[点击此处查看代码图像](#)

```java
public class SineTest {
    private static final double EPSILON = 0.0001;
    @Test
    public void sines() throws Exception {
        assertEquals(0, sin(0), EPSILON);
        assertEquals(0, sin(Math.PI), EPSILON);
    }

    double sin(double radians) {
        return 0.0;
    }
}
```

我们再次有了那种不受约束的感觉。这个测试似乎没有为解增加任何东西。它没有给我们任何如何解决问题的提示，所以让我们试试 π/2：

[点击此处查看代码图像](#)

```java
public class SineTest {
    private static final double EPSILON = 0.0001;
    @Test
    public void sines() throws Exception {
        assertEquals(0, sin(0), EPSILON);
        assertEquals(0, sin(Math.PI), EPSILON);
        assertEquals(1, sin(Math.PI/2), EPSILON);
    }
    double sin(double radians) {
        return 0.0;
    }
}
```

这个测试失败了。我们怎样才能让它通过？同样，这个测试没有给我们任何关于如何让它通过的提示。我们可以尝试加入一些糟糕的 `if` 语句，但那只会导致越来越多的 `if` 语句。

此时，你可能会认为最好的方法是查阅正弦的泰勒级数，然后直接实现它。

$$x - \frac{x^3}{3!} + \frac{x^5}{5!} - \frac{x^7}{7!} + \cdots$$

这应该不会太难：

[点击此处查看代码图像](#)

```java
public class SineTest {
    private static final double EPSILON = 0.0001;
    @Test
    public void sines() throws Exception {
        assertEquals(0, sin(0), EPSILON);
        assertEquals(0, sin(Math.PI), EPSILON);
        assertEquals(1, sin(Math.PI/2), EPSILON);
    }

    double sin(double radians) {
        double r2 = radians * radians;
        double r3 = r2 * radians;
        double r5 = r3 * r2;
        double r7 = r5 * r2;
        double r9 = r7 * r2;
        double r11 = r9 * r2;
        double r13 = r11 * r2;
        return (radians - r3/6 + r5/120 - r7/5040 + r9/362880 -
                r11/39916800.0 + r13/6227020800.0);
    }
}
```

这个测试通过了，但它相当丑陋。不过，我们仍然应该能够用这种方式计算其他几个正弦值：

[点击此处查看代码图像](#)

```java
public void sines() throws Exception {
    assertEquals(0, sin(0), EPSILON);
    assertEquals(0, sin(Math.PI), EPSILON);
    assertEquals(1, sin(Math.PI/2), EPSILON);
    assertEquals(0.8660, sin(Math.PI/3), EPSILON);
    assertEquals(0.7071, sin(Math.PI/4), EPSILON);
    assertEquals(0.5877, sin(Math.PI/5), EPSILON);
}
```

是的，这个测试通过了。但这个解决方案很丑陋，因为它的精度有限。我们应该把泰勒级数展开到足够多的项，使其收敛到我们的精度极限。（注意 EPSILON 常量的变化。）

[点击此处查看代码图像](#)

```java
public class SineTest {
    private static final double EPSILON = 0.00000001;
    @Test
    public void sines() throws Exception {
        assertEquals(0, sin(0), EPSILON);
        assertEquals(0, sin(Math.PI), EPSILON);
        assertEquals(1, sin(Math.PI/2), EPSILON);
        assertEquals(0.8660254038, sin(Math.PI/3), EPSILON);
        assertEquals(0.7071067812, sin(Math.PI/4), EPSILON);
        assertEquals(0.5877852523, sin(Math.PI/5), EPSILON);
    }

    double sin(double radians) {
        double result = radians;
        double lastResult = 2;
        double m1 = -1;
        double sign = 1;
        double power = radians;
        double fac = 1;
        double r2 = radians * radians;
        int n = 1;
        while (!close(result, lastResult)) {
            lastResult = result;
            power *= r2;
            fac *= (n+1) * (n+2);
            n += 2;
            sign *= m1;
            double term = sign * power / fac;
            result += term;
        }

        return result;
    }

    boolean close(double a, double b) {
        return Math.abs(a - b) < .0000001;
    }
}
```

好了，现在进展得很顺利。但是等等？TDD 怎么了？我们怎么知道这个算法真的正确工作？我的意思是，这是很多代码。我们怎么判断这些代码是否正确？

我想我们可以再测试几个值。而且，哎呀，这些测试变得越来越笨重了。我们也来稍微重构一下吧：

点击此处查看代码图像

