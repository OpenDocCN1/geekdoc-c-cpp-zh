

9. 在事件列表中，找到 RightTapped 事件，然后双击 RightTapped 文本框。
此事件发生在用户使用手指在画布上轻触、按住然后释放，或在画布上单击鼠标右键时发生。

10. 在 drawingCanvas_RightTapped 方法中添加下面以粗体显示的代码：

Click here to view code image

```
private void drawingCanvas_RightTapped(object sender,
RightTappedRoutedEventArgs e)
{
    Point mouseLocation = e.GetPosition(this.drawingCanvas);
    Circle myCircle = new Circle(100);

    if (myCircle is IDraw)
    {
        IDraw drawCircle = myCircle;
        drawCircle.SetLocation((int)mouseLocation.X,
(int)mouseLocation.Y);
        drawCircle.Draw(drawingCanvas);
    }

    if (myCircle is IColor)
    {
        IColor colorCircle = myCircle;
        colorCircle.SetColor(Colors.HotPink);
    }
}
```

此代码中的逻辑与 drawingCanvas_Tapped 方法中的逻辑类似，只是此代码绘制并填充的是圆形而不是正方形。

11. 在 Debug 菜单上，单击 Start Debugging 以构建并运行应用程序。

12. 当 Drawing Pad 窗口打开时，在窗口中显示的画布上任意位置轻触或单击。应出现一个紫色正方形。

13. 在画布上任意位置轻触、按住并释放，或右键单击。应出现一个粉色圆形。你可以任意多次单击鼠标左键和右键；每次单击都会在鼠标位置绘制一个正方形或圆形。以下图像显示了应用程序在 Windows 10 上的运行情况：

## Drawing Pad

![](img/16f6e3fe08f01ddadb2741a92c392b0e_361_0.png)

14. 返回 Visual Studio 并停止调试。

## 抽象类

你可以在许多不同的类中实现之前练习中讨论的 ILandBound 和 IGrazable 接口，具体取决于你在 C# 应用程序中想要建模的哺乳动物类型的数量。在这种情况下，派生类的一部分通常会共享通用实现。例如，以下两个类中的重复是显而易见的：

[Click here to view code image]()

```
class Horse : Mammal, ILandBound, IGrazable
{
    ...
    void IGrazable.ChewGrass()
    {
        Console.WriteLine("Chewing grass");
        // code for chewing grass
    }
}

class Sheep : Mammal, ILandBound, IGrazable
{
```

```
    ...
    void IGrazable.ChewGrass()
    {
        Console.WriteLine("Chewing grass");
        // same code as horse for chewing grass
    }
}
```

代码中的重复是一个警告信号。如果可能，你应该重构代码以避免重复并降低相关的维护成本。实现此重构的一种方法是把通用实现放入专门为此目的创建的新类中。实际上，你可以在类层次结构中插入一个新类，如以下代码示例所示：

Click here to view code image

```
class GrazingMammal : Mammal, IGrazable
{
    ...
    void IGrazable.ChewGrass()
    {
        // common code for chewing grass
        Console.WriteLine("Chewing grass");
    }
}

class Horse : GrazingMammal, ILandBound
{
    ...
}

class Sheep : GrazingMammal, ILandBound
{
    ...
}
```

这是一个不错的解决方案，但仍有一点不太对劲：你实际上可以创建 GrazingMammal 类的实例（同样 Mammal 类也是如此）。这并没有什么意义。GrazingMammal 类的存在是为了提供一个通用的默认实现。它的唯一目的是作为一个可继承的类。GrazingMammal 类是对通用功能的抽象，而不是自身的一个实体。

要声明不允许创建某个类的实例，你可以使用 abstract 关键字声明该类为抽象类，如以下示例所示：

Click here to view code image

```
abstract class GrazingMammal : Mammal, IGrazable
{
    ...
}
```

如果现在尝试实例化一个 *GrazingMammal* 对象，代码将无法编译：

Click here to view code image

```
GrazingMammal myGrazingMammal = new GrazingMammal(...); // illegal
```

## 抽象方法

抽象类可以包含抽象方法。抽象方法在原则上与虚拟方法类似（在第 12 章中介绍），只是它不包含方法体。派生类 *必须* 重写此方法。抽象方法不能是私有的。以下示例将 *GrazingMammal* 类中的 *DigestGrass* 方法定义为抽象方法；食草哺乳动物可能使用相同的代码来咀嚼草，但它们必须提供自己的 *DigestGrass* 方法实现。抽象方法在不适合在抽象类中提供默认实现但希望继承类提供自己的实现时很有用。

Click here to view code image

```
abstract class GrazingMammal : Mammal, IGrazable
{
    public abstract void DigestGrass();
    ...
}
```

## 密封类

使用继承并不总是容易的，并且需要深思熟虑。如果你创建一个接口或抽象类，你就是在有意识地编写将来会被继承的东西。问题在于预测未来是一件困难的事情。通过练习和经验，你可以培养出设计灵活、易于使用的接口、抽象类和类层次结构的能力，但这需要付出努力，并且你还需要对正在建模的问题有扎实的理解。换句话说，除非你有意识地设计一个类以用作基类，否则它几乎不可能作为基类良好地发挥作用。在 C# 中，如果你决定某个类不应被用作基类，可以使用 *sealed* 关键字来防止该类被用作基类。例如：

Click here to view code image

```
sealed class Horse : GrazingMammal, ILandBound
{
    ...
}
```

如果任何类尝试将 *Horse* 用作基类，将会生成编译时错误。请注意，密封类不能声明任何虚拟方法，并且抽象类不能被密封。

## 密封方法

你也可以使用 sealed 关键字声明未密封类中的单个方法为密封。这意味着派生类不能重写此方法。你只能密封使用 override 关键字声明的方法，并且将方法声明为 sealed override。你可以把 interface、virtual、override 和 sealed 关键字理解如下：

+   - 一个接口引入了方法的名称。
+   - 一个虚拟方法是方法的第一个实现。
+   - 一个重写方法是方法的另一个实现。
+   - 一个密封方法是方法的最后一个实现。

## 实现和使用抽象类

以下练习使用抽象类来合理化你在上一个练习中开发的一些代码。Square 和 Circle 类包含大量重复代码。将此代码提取到名为 DrawingShape 的抽象类中是有意义的，因为这将有助于在未来更轻松地维护 Square 和 Circle 类。

## 创建 DrawingShape 抽象类

-   1. 返回 Visual Studio 中的 Drawing 项目。

### Note

上一个练习的完整工作副本可在 Drawing 项目中找到，该项目位于你的 Documents 文件夹中的 \Microsoft Press\VCSBS\Chapter 13\Drawing Using Interfaces 文件夹中。

-   2. 在 Solution Explorer 中，单击 Drawing 解决方案中的 Drawing 项目。在 Project 菜单上，单击 Add Class。
+   Add New Item – Drawing 对话框打开。

-   3. 在 Name 框中，键入 DrawingShape.cs，然后单击 Add。
+   Visual Studio 创建该类并在 Code and Text Editor 窗口中显示它。

-   4. 在 DrawingShape.cs 文件中，在文件顶部的列表中，添加以下 using 指令：

Click here to view code image

```
using Windows.UI;
```

