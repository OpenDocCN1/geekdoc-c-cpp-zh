
```
if (!(x < y) && !(y < x) && (!(y < z) && !(z < y)) assert (!(x < z) && !(z < x));
```

第三个条件对于构建严格弱序是必要的。没有它，`<` 被称为偏序。你可能用偏序也能过关，但仅限于受限的用途；大多数有趣的算法都需要严格弱序。如果你想定义偏序，最好放弃所有的语法糖，并定义与 `opcmp` 不同的自定义函数。

## 第 6 章。类。面向对象的风格

注意，上述条件仅关注 `<` 而不是其他排序比较，因为后者仅仅是语法糖（`x > y` 等于 `y < x`，`x <= y` 等于 `!(y > x)`，以此此类推）。

（注：原文文本后半部分存在大量重复的 OCR 错误和乱码，上述翻译已根据核心逻辑进行清理。）

## 6.9 接口 (Interfaces)

大多数类对象包含状态并定义了处理该状态的方法。因此，一个通用对象既作为外部世界的接口（通过其公共方法），又作为该接口的封装实现。

有时，将“接口”的概念与“实现”的概念分开是非常有用的。当你想要定义大型程序中各个部分之间的通信时，这种做法特别有用。一个试图操作 Widget 的函数只关注 Widget 的实现——这与封装的定义本身无关。这引出了一个完全抽象的接口，它只包含类必须实现的方法，但不包含任何实现代码。这种实体被称为接口。

D 语言的接口定义看起来像受限制的类定义。除了将 `class` 关键字替换为 `interface` 之外，接口定义还需要服从严格的限制。你不能在接口中定义任何非静态数据，也不能为任何可重写的函数指定实现。在接口内部定义静态数据和带有实现的 `final` 函数是合法的。例如：

```
interface Transmifier {

  void transmogrify();

  void untransogrify();

  final void thereBack() {

    transmogrify();

    untransogrify();

  }

}
```

这就是函数使用 `Transmifier` 编译所需的全部内容。例如：

```
void aDayInLife(Transmifier device, string mood) {

  if (mood == "play") {

    device.transmogrify();

    device.untransogrify();

  } else if (mood == "experiment") {

    device.thereBack();

  }

}
```

当然，鉴于目前还没有 `Transmifier` 原生类型的定义，还没有合理的方法来调用 `aDayInLife`。所以让我们为该接口创建一个实现：

```
class CardboardBox : Transmifier {

  override void transmogrify() {

    // 进入箱子
    ...
  }

  override void untransogrify() {

    // 离开箱子
    ...
  }

}
```

接口的实现使用与普通继承相同的语法。现在有了 `CardboardBox`，我们现在可以发出如下调用：

`aDayInLife(new CardboardBox, "play");`

接口的任何实现都是该接口的子类型，因此它可以自动转换为该接口。我们只需通过传递一个 `CardboardBox` 对象来代替 `aDayInLife` 预期的 `Transmifier` 类型。

### 6.9.1 非虚拟接口 (NVI) 惯用

一个可能并不熟悉的是 `Transmifier` 接口中的 `final` 函数。当诗意地描述抽象的、未实现的功能时发生了什么？如果接口是抽象的，它就不应该定义任何实现。

2001 年，Herb Sutter 写了一篇文章 [52]，提出了了一个有趣的观察，他后来在书书中 [55, Item 39] 中提到了这一观点。接口定义的可重写方法（例如示例中的 `transmogrify` 和 `untransogrify`）承担着双重角色。首先，它们是接口本身的元素，即调用代码为了完成任务而使用的内容。其次，这些方法也是自定义点，因为继承类是直接定义了它们。这可能很有用。Sutter 认为，在这两个类别之间：接口可以定义稍后实现的低级抽象方法，加上客户端代码可能使用的高层级、可见且不可重写的方法。这两组方法可能不会重叠，但将它们视为理想状态将得不偿失。

区分“客户端看到的”和“实现者定义的”有许多好处。这种方法允许你设计既对实现友好又对客户端友好的接口。混淆了实现需求和客户端需求的接口必须在两种需求之间进行折中。过度关注实现会导致接口过于平庸、冗长且低级，从而在客户端代码中引发代码重复；而过度关注客户端代码则会导致接口庞大、松散且冗余，这些接口在指定基本原语之外还指定了便利函数。通过非虚拟接口 (NVI) 惯用，你可以让双方的生活都变得更轻松。例如，`Transmifier.thereBack` 为调用者提供了一个根据原生操作定义的便利函数。

这种当时初生的惯用与模板方法模式（Template Method pattern）保持一致，该模式通过自定义的中间步骤编写高层操作，但它变得足够独特，以至于有了自己的名字，即非虚拟接口 (NVI)。遗憾的是，尽管 NVI 已成为一种广泛使用的模式，但它更多是优秀设计师之间的一种契俗，而不是一种语言辅助的强制设计一致性的手段。语言对 NVI 的支持一直缺乏，主要是因为一些流行的 OOP 语言的定义早于（并影响了）导致 NVI 产生的对 OOP 设计的更好理解。因此，Java 完全不支持 NVI，C# 支持但目前仅将其作为设计准则，而 C++ 虽然允许良好的便利助手支持，但对调用者或实现者没有强力的保证。

D 语言通过在接口使用访问修饰符时提供特定的保证来支持 NVI。例如，`Transmifier` 的作者担心使用不当——如果人们调用了 `transmogrify` 却忘记调用 `untransogrify` 呢？让我们只向客户端暴露 `thereBack`，同时要求实现类定义 `transmogrify` 和 `untransogrify`：

```
interface Transmifier {

  // 客户端接口
  final void thereBack() {
    transmogrify();
    untransogrify();
  }

  // 实现接口
  private:
  void transmogrify();
  void untransogrify();
}
```

`Transmifier` 接口将这两个私有化。这种设置了一个非常有趣的设计：实现 `Transmifier` 的类必须定义 `transmogrify` 和 `untransogrify`，但在外部无法访问它们。调用它们的唯一方法是间接的，即使用高层的 `thereBack`，这正是设计的精髓。语言阻止了破坏这种尝试。例如，实现类不能降低 `transmogrify` 的权限级别：

```
class CardboardBox : Transmifier {
  override private void transmogrify() { ... } // 允许
  override void transmogrify() { ... } // 错误！无法将 transmogrify 从 private 改为 public！
```

当然，归根底这是你的实现，如果你想要可以创建一个原生方法，但你必须给它一个不同的名称：

```
class CardboardBox : Transmifier {
  override private void transmogrify() { ... } // 允许
  override void transmogrify() { // 允许
    doTransmogrify();
  }
  override void doTransmogrify() { ... } // 允许
}
```

现在 `CardboardBox` 的用户可以调用 `doTransmogrify()`，它的功能与 `transmogrify` 相同。点在于，具有特定名称和签名的 `void transmogrify()` 不能由实现类直接暴露。如果实现想要定义并记录一个替代函数，那是它的决定。

D 语言通过禁用劫持 `final` 方法的另一种方式强制 NVI：`Transmifier` 的任何实现都不能定义有效劫持 `thereBack` 的方法。例如：

```
class Broken : Transmifier {
  void thereBack() {
    // 为什么不做两次？
    this.Transmogrifier.thereBack();
    this.Transmogrifier.thereBack();
  }
  // 错误！无法劫持 final 方法 Transmifier.thereBack
}
```

如果允许这种隐藏，知道 `Broken` 实现了 `Transmifier` 的客户端无法确保对类型为 `Broken` 的对象调用 `obj.thereBack()`；无法确认 `thereBack` 会按照 `Transmifier` 规定和记录的那样执行。当然，客户端代码可以调用 `obj.Transmogrifier.thereBack()` 来确保调用正确路由，但这种注意力驱动的设计永远不会那么吸引人。毕竟，一个良好的设计并不

## 第 6 章 类。面向对象的风格

它会在你降低防备时用令人困惑的行为出击。底线是——如果一个接口定义了一个公共函数，该函数在所有实现中都将保持可见。如果该实现也是 `final` 的，那么实现类就没有方法拦截对它的调用。然而，实现类可以定义一个同名的函数，只要没有潜在的冲突即可。例如：

```
class Good : Transmogrifier {
  void thereAndBack(uint times) {
    // 为什么不执行多次呢？
    foreach (i; 0 ... times) {
      thereAndBack();
    }
  }
}
...
```

上述情况是允许的，因为不存在混淆的风险：调用写为 `obj.thereAndBack(n)` 并指向 `Transmogrifier.thereAndBack`，或者写为 `obj.thereAndBack(n)` 并指向 `Good.thereAndBack`。`Good.thereAndBack` 的实现不需要对同名函数的调用进行限定。

### 6.9.2 受保护的原始类型

在接口中将一个可重写函数设为 `private` 有时比需要的更具限制性。例如：

```
class CardboardBox : Transmifier {
  private:
  override void transmogrify() { ... }
  override void untransogrify() { ... }
}
class FlippableCardboardBox : CardboardBox {
  private:
  bool flipped;
  override void transmogrify() {
    enforce(!flipped, "无法翻转");
    super.transmogrify(); // 错误！无法调用私有方法
  }
}
```

### 6.9 接口

当盒子翻转时，它无法作为 `transmogrifier`——众所周知，`FlippableCardboardBox` 强制了这一点，但在正常路径上无法调用父类的方法。该怎么办？

一种解决方案是使用上面类似的 `doTransmify` 重命名技巧，但如果需要对多个方法这样做，就会变得很重复。一个更简单的解决方案是将 `Transmogrifier` 中的可重写访问放为 `protected`：

```
interface Transmogrifier {
    final void thereAndBack() { ... }
protected:
    void transmogrify();
    void untransogrify();
}
```

通过 `protected` 访问，实现类现在能够调用父类的实现。注意，加强保护也是非法的。如果接口定义了一个方法，实现类不能对该方法声明更强的保护。例如，`Transmogrifier` 定义了 `transmogrify` 和 `untransogrify`，以下代码将报错：

```
class BrokenInWays {
    public void transmogrify() { ... } // 错误！
    private void untransogrify() { ... } // 错误！
}
```

在技术上，允许在实现中放宽接口的要求，但这毫无用处。接口表达了一种意图，而实现类应该完全吸收接口的定义。

### 6.9.3 选择性实现

有时会出现两个接口定义了 `final` 方法的情况：

```
interface Timer {
    final void run() { ... }
    ...
}
```

```
interface Application {
    final void run() { ... }
    ...
}
```

```
class TimedApp : Timer, Application {
... // 无法定义 run()
}
```

在这种情况下，`TimedApp` 无法定义自己的 `run()`，因为它会接管两个方法。消除 `Timer` 或 `Application` 中的其中一个 `final` 并无法解决问题，因为另一个仍然有效。如果两者都是非 `final` 的，情况就顺利——`TimedApp` 同时实现了 `Timer.run` 和 `Application.run`。

## 6.10 抽象类

通常，基类无法为其某些或所有方法提供合理的实现。一种想法是将此类类转换为接口，但有时让类定义一些状态和非 `final` 方法非常有帮助，而接口是不允许的。这里抽象类成了救星：它们几乎就像普通类，可以使用 `abstract` 关键字让函数保持未实现。

作为示例，考虑一个参与矢量图形程序的对象的层次结构。该层次结构根于 `Shape` 类。任何形状都有边界矩形，因此 `Shape` 可能需要将其定义为成员变量（接口无法实现的）。另一方面，`Shape` 必须留出某些方法（如 `draw`），因为它无法合理地实现它们。这些方法应该由 `Shape` 的后代类实现。

```
class Rectangle {
int left, right, top, bottom;
}
```

```
class Shape {
  protected Rectangle bounds;
  abstract void draw(Shape that);
  bool overlaps(Shape that) {
      return bounds.left <= that.bounds.right &&
             bounds.right >= that.bounds.left &&
             bounds.top <= that.bounds.bottom;
    }
```

### 6.10.1 抽象类（续）

至少有一个抽象方法的类本身被称为抽象类。如果重写了 `Shape` 的所有抽象方法，`RectangularShape` 也是抽象的。此外，`RectangularShape` 允许引入新的抽象方法。例如：

```
class Shape {
    // 同上
    abstract void draw();
}
class RectangularShape : Shape {
    // 继承 Shape 的一个抽象方法
    // 并引入另一个
    abstract void drawFrame();
}
class Rectangle : RectangularShape {
    override void draw() { ... }
    // Rectangle 仍然是一个抽象类
}
class SolidRectangle : Rectangle {
    override void drawFrame() { ... }
    // SolidRectangle 是具体的：
    // 没有更多抽象函数需要实现
```

最有趣的是，一个类可能决定将一个函数重新引入为抽象的，尽管它之前已经被重写并实现了！下面的代码引入了一个抽象类，从它派生出一个具体类，然后从该具体类派生出一个抽象类，这一切仅仅为了一个方法。

```
class Abstract {
    abstract void fun();
}
```

```
class Concrete : Abstract {
    override void fun() { ... };
}
```

```
class BornAgainAbstract : Concrete {
    abstract override void fun();
}
```

你可以对抽象方法的实现进行最终……

```
class UltimateShape : Shape {
    // 这是关于 draw 方法的最终决定
    override final void draw() { ... };
}
```

但由于明显的原因，不能定义一个既是 `abstract` 又是 `final` 的方法。

如果你想引入一组抽象方法，可以用类似于保护限定符的方式重用 `abstract` 关键字（第 200 页第 6.7.1 节）：
