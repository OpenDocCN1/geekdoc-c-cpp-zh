

```java
private void checkSin(double radians, double sin) {
    assertEquals(sin, sin(radians), EPSILON);
}
```

```java
@Test
public void sines() throws Exception {
    checkSin(0, 0);
    checkSin(PI, 0);
    checkSin(PI/2, 1);
    checkSin(PI/3, 0.8660254038);
    checkSin(PI/4, 0.7071067812);
    checkSin(PI/5, 0.5877852523);
    checkSin(3*PI/2, -1);
}
```

好，这通过了。我们再试几个：

```java
checkSin(2*PI, 0);
checkSin(3*PI, 0);
```

啊，2π 可行，但 3π 不行。不过它很接近：4.6130E-9。我们或许可以通过提高 `close()` 函数中比较的限值来修正这个问题，但那看起来像作弊，而且对 100π 或 1,000π 可能也不管用。更好的方案是把角度缩减到 0 到 2π 之间。

```java
double sin(double radians) {
    radians %= 2*PI;
    double result = radians;
```

是的。这样可行。那么负数呢？

```java
checkSin(-PI, 0);
checkSin(-PI/2, -1);
checkSin(-3*PI/2, 1);
checkSin(-1000*PI, 0);
```

是的，它们都可行。好，那么不是 2π 的整数倍的大数呢？

点击此处查看代码图像

```java
checkSin(1000*PI + PI/3, sin(PI/3));
```

唉。那也可行。还有什么可试的吗？有没有可能失败的值？

哎哟！我不知道。

## TDD 不确定性原理

欢迎来到 TDD 不确定性原理的前半部分。无论我们尝试多少个值，都会留下这种挥之不去的不确定性：我们漏掉了某些东西——某个输入值不会产生正确的输出值。

大多数函数不会让你这样悬着心。大多数函数都有一个很好的性质：当你写完最后一个测试时，你*知道*它们能工作。但随后又有这些烦人的函数，让你怀疑是否存在某个会失败的值。

用我们已经写出的这类测试来解决这个问题的唯一方法，就是尝试每一个可能的值。而由于 `double` 数有 64 位，这意味着我们需要编写略少于 2 × 10^19 个测试。这比我愿意写的多得多。

那么，关于这个函数，我们*到底*信任什么？我们信任泰勒级数能计算给定弧度角的正弦吗？是的，我们看到了它的数学证明，所以我们相当确定泰勒级数会收敛到正确的值。

我们如何把对泰勒级数的信任转化为一组测试，以证明我们正在正确地执行那个泰勒级数呢？

我想我们可以检查泰勒展开的每一项。例如，在计算 sin(π) 时，泰勒级数的各项为 3.141592653589793、−2.0261201264601763、0.5240439134171688、−0.075220615903062306、0.006925270707505149、−4.4516023820919976E-4、2.114256755841263E-5、−7.727858894175775E-7、2.2419510729973346E-8。

我不明白这种测试为什么会比我们已有的测试更好。那些值只适用于某一个特定测试，而且它们没有告诉我们这些项对其他任何值是否正确。

不，我们想要不同的东西。我们想要决定性的东西。某种能*证明*我们使用的算法确实恰当地执行了泰勒级数的东西。

好，那么那个泰勒级数是什么？它是 $x$ 的奇次幂除以奇阶乘的无限交错和：

$$\sum_{n=1}^{\infty} (-1)^{(n-1)} \frac{x^{2n-1}}{(2n-1)!}$$

或者，换句话说，

$$x - \frac{x^3}{3!} + \frac{x^5}{5!} - \frac{x^7}{7!} + \frac{x^9}{9!} - \cdots$$

这如何帮助我们？嗯，如果我们有一个间谍对象，能告诉我们泰勒级数的各项是如何被计算的，那就可以让我们写出这样的测试：

点击此处查看代码图像

```java
@Test
public void taylorTerms() throws Exception {
    SineTaylorCalculatorSpy c = new SineTaylorCalculatorSpy();
    double r = Math.random() * PI;
    for (int n = 1; n <= 10; n++) {
        c.calculateTerm(r, n);
        assertEquals(n - 1, c.getSignPower());
        assertEquals(r, c.getR(), EPSILON);
        assertEquals(2 * n - 1, c.getRPower());
        assertEquals(2 * n - 1, c.getFac());
    }
}
```

对 $x$ 使用随机数，并对 `n` 使用所有合理的值，可以让我们避免使用特定值。我们在这里关心的是：给定某个 $x$ 和某个 `n`，正确的数字被送入正确的函数。如果这个测试通过，我们就会*知道*`sign`、`power` 和 `factorial` 计算器都收到了正确的输入。

我们可以用下面这段简单的代码让测试通过：

点击此处查看代码图像

```java
public class SineTaylorCalculator {
    public double calculateTerm(double r, int n) {
        int sign = calcSign(n-1);
        double power = calcPower(r, 2*n-1);
        double factorial = calcFactorial(2*n-1);
        return sign*power/factorial;
    }

    protected double calcFactorial(int n) {
        double fac = 1;
        for (int i=1; i<=n; i++)
            fac *= i;
        return fac;
    }

    protected double calcPower(double r, int n) {
        double power = 1;
        for (int i=0; i<n; i++)
            power *= r;
        return power;
    }

    protected int calcSign(int n) {
        int sign = 1;
        for (int i=0; i<n; i++)
            sign *= -1;
        return sign;
    }
}
```

注意，我们并没有测试实际的计算函数。它们非常简单，可能不需要测试。鉴于我们即将编写的其他测试，这一点尤其正确。

这是间谍对象：

点击此处查看代码图像

```java
package London_sine;

public class SineTaylorCalculatorSpy extends SineTaylorCalculator {
    private int fac_n;
    private double power_r;
    private int power_n;
    private int sign_n;
    public double getR() {
        return power_r;
    }

    public int getRPower() {
        return power_n;
    }

    public int getFac() {
        return fac_n;
    }

    public int getSignPower() {
        return sign_n;
    }

    protected double calcFactorial(int n) {
        fac_n = n;
        return super.calcFactorial(n);
    }

    protected double calcPower(double r, int n) {
        power_r = r;
        power_n = n;
        return super.calcPower(r, n);
    }

    protected int calcSign(int n) {
        sign_n = n;
        return super.calcSign(n);
    }
}
```

```java
public double calculateTerm(double r, int n) {
    return super.calculateTerm(r, n);
}
```

既然测试通过了，编写求和算法有多难呢？

点击此处查看代码图像

```java
public double sin(double r) {
    double sin=0;
    for (int n=1; n<10; n++)
        sin += calculateTerm(r, n);
    return sin;
}
```

你可以抱怨整个实现的效率，但你相信它能工作吗？`calculateTerm` 函数是否正确计算了正确的泰勒项？`sin` 函数是否正确地把它们加在一起？10 次迭代足够吗？我们如何在不退回那些原始值测试的情况下测试这一点？

这里有一个有趣的测试。`sin(r)` 的所有值都应该在 –1 和 1 之间（开区间）。

点击此处查看代码图像

```java
@Test
public void testSineInRange() throws Exception {
    SineTaylorCalculator c = new SineTaylorCalculator();
    for (int i=0; i<100; i++) {
        double r = (Math.random() * 4 * PI) - (2 * PI);
        double sinr = c.sin(r);
        assertTrue(sinr < 1 && sinr > -1);
    }
}
```

那个测试通过了。这个呢？给定这个恒等式，

点击此处查看代码图像

```java
public double cos(double r) {
    return (sin(r+PI/2));
}
```

让我们测试毕达哥拉斯恒等式：sin² + cos² = 1。

[点击此处查看代码图像](#)

```java
    @Test
    public void PythagoreanIdentity() throws Exception {
        SineTaylorCalculator c = new SineTaylorCalculator();
        for (int i=0; i<100; i++) {
            double r = (Math.random() * 4 * PI) - (2 * PI);
            double sinr = c.sin(r);
            double cosr = c.cos(r);
            assertEquals(1.0, sinr * sinr + cosr * cosr, 0.00001);
        }
    }
```

嗯。实际上，直到我们把项数提高到 20 它才通过，而 20 当然是一个高得离谱的数字。但是，就像我说的，这是一个极端的练习。

鉴于这些测试，我们有多大信心认为自己正确地计算了正弦？我不知道你怎么想，但我相当有信心。我知道各项被喂入了正确的数字。我可以目测那些简单的计算器，而且 `sin` 函数似乎具有正弦的性质。

哦，管他呢，我们就随便做几个值测试吧：

[点击此处查看代码图像](#)

```java
    @Test
    public void sineValues() throws Exception {
        checkSin(0, 0);
        checkSin(PI, 0);
        checkSin(PI/2, 1);
        checkSin(PI/3, 0.8660254038);
        checkSin(PI/4, 0.7071067812);
        checkSin(PI/5, 0.5877852523);
    }
```

是的，全都可行。很好。我解决了我的信心问题。我不再怀疑我们是否正确计算正弦了。谢天谢地，有那个间谍对象！

### TDD 不确定性原理（再次）

