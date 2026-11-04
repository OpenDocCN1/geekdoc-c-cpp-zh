
```
{
    Person person = peopleListBox.SelectedItem as Person;
    MessageBox.Show(person.GetAddress());
}
```

这段代码将 ListBox 的选中项转换为 Person 对象。该项实际上是 Student 或 Employee，但两者都继承自 Person（它们是 Person 的一种），因此程序可以将其视为 Person。

程序调用 Person 的 GetAddress 方法并显示结果。如果对象实际上是 Student，结果是基本姓名和地址。如果对象实际上是 Employee，结果是姓名、地址加上邮件分发点。

除了 ListBox 和 ComboBox 之外，Visual Studio 的某些部分也会使用对象的 ToString 方法。例如，如果你在调试器中停止正在执行的程序并将鼠标悬停在对象上，会出现一个工具提示，显示该对象 ToString 方法的结果。同样，如果你在“即时”窗口中输入对象的名称并按 Enter，返回的结果就是该对象 ToString 方法的返回值。

## 试一试

在本“试一试”中，你将改进为练习 24-9 所构建的形状绘制程序，通过重写 Shape 类的 Draw 方法，使 Ellipse 和 Circle 对象能够适当地绘制自身。

### 课程要求

在本课中，你要：

- 复制你在练习 24-9 中编写的程序（或从书的网站上下载可用版本）。
- 在 Shape 类的 Draw 方法中添加 virtual 关键字。
- 重写 Ellipse 类中的 Draw 方法，使其绘制椭圆而不是矩形。
- 修改窗体的 Paint 事件处理程序以绘制平滑形状。

> 注意 你可以从网站 www.wrox.com/go/csharp24hourtrainer2e 下载本课的代码和资源。

### 提示

如果 gr 是 Graphics 对象，你可以使用以下技术：

- gr.SmoothingMode = SmoothingMode.AntiAlias—使对象平滑绘制形状。（SmoothingMode 在 System.Drawing.Drawing2D 命名空间中定义。）
- gr.FillEllipse(brush, rect)—使用 brush 填充由 Rectangle rect 定义的椭圆。
- gr.DrawEllipse(pen, rect)—使用 pen 勾勒由 Rectangle rect 定义的椭圆。

### 逐步操作

复制你在练习 24-9 中编写的程序（或从书的网站上下载可用版本）。

- 1. 这很直接。

在 Shape 类的 Draw 方法中添加 virtual 关键字。

- 1. 修改 Shape 类的 Draw 方法，使其声明如下所示。（virtual 关键字以粗体突出显示。）

  ```csharp
  public virtual void Draw(Graphics gr)
  ```

重写 Ellipse 类中的 Draw 方法，使其绘制椭圆而不是矩形。

- 1. 使用类似以下的代码：

  ```csharp
  // Draw the ellipse.
  public override void Draw(Graphics gr)
  {
      using (Brush brush = new SolidBrush(Background))
      {
          gr.FillEllipse(brush, Bounds);
      }
      using (Pen pen = new Pen(Foreground, Thickness))
      {
          gr.DrawEllipse(pen, Bounds);
      }
  }
  ```

- 2. 请注意，你不需要重写 Circle 类的 Draw 方法。Circle 类继承自 Ellipse，因此它将继承此处所示由 Ellipse 类定义的版本。Circle 类的构造函数确保 Circle 的宽度和高度相同，这使得椭圆绘制代码产生圆形。

修改窗体的 Paint 事件处理程序以绘制平滑形状。

- 1. 在窗体代码文件的顶部添加以下 using 指令：

  ```csharp
  using System.Drawing.Drawing2D;
  ```

- 2. 在窗体的 Paint 事件处理程序开头添加以下语句：

  ```csharp
  e.Graphics.SmoothingMode = SmoothingMode.AntiAlias;
  ```

![](img/d5be6ade75773ca6cec5c78f96a98bb1_405_0.png)

图 25-2

图 25-2 显示了我创建的对象的结果。

## 练习

- 1. [图形] 复制你在“试一试”中构建的程序并重写 `Shape` 类的 `Draw` 方法，创建一个新版本，该版本接受 `Pen` 和 `Brush` 作为参数并使用它们进行绘制。然后对 `Ellipse` 和 `Circle` 类做类似的更改。通过修改窗体代码，使其将 `Pens.Red` 和 `Brushes.Pink` 传递给对象的 `Draw` 方法来测试新方法。

- 2. [图形] 复制你在练习 1 中构建的程序并添加 `Rect` 和 `Square` 类。（我将其中第一个类称为 `Rect` 而不是 `Rectangle`，因为 .NET 已有 `Rectangle` 类，这样命名可能会引起混淆。）修改窗体代码以创建一个随机的 `Shape`、`Ellipse`、`Circle`、`Rect` 和 `Square`。提示：

  - 使 `Rect` 类类似于 `Ellipse` 类。
  - 使 `Square` 类有点类似于 `Circle` 类，但其构造函数接受 X 和 Y 坐标以及宽度，而不是圆心点和半径。
  - 创建一个 `GetRandomParameters` 方法来为新形状生成随机的厚度、宽度、高度和位置。
  - 删除使所有形状变为粉红色的代码，以便可以看到形状的颜色。

- 3. [图形，高级] `abstract` 关键字与 `virtual` 关键字 somewhat 相似。当你将方法标记为 `abstract` 时，你允许在派生类中重写它。事实上，抽象方法没有代码，因此在你能够创建该类的实例之前，你 *必须* 重写它。

  因为你不能创建包含 `abstract` 方法的类的实例，所以你还必须将该类标记为 `abstract`。

  为什么要这样做？想想你在“试一试”中编写的程序。你可能并不真正打算让程序创建 `Shape` 类的实例。它实际上只是作为一个基类存在，以便你可以将 `Ellipses` 和 `Circles` 等其他对象视为 `Shapes`。

  复制你在练习 2 中编写的程序并使 `Shape` 类的 `Draw` 方法抽象。然后修改窗体代码，使其不尝试创建 `Shape` 对象。提示：

  - 抽象方法不能包含任何代码。只需在方法参数列表后以分号结束即可。
  - 在 `class` 关键字前放置 `abstract` 关键字。
  - 抽象类可以包含非抽象属性和方法，并且它们会像往常一样被继承。在此示例中，`Shape` 类仍可以定义绘图参数（`Bounds`、`Foreground`、`Background` 和 `Thickness`）和构造函数。

- 4. [图形，困难] 创建一个新程序，显示一个 Cursor 属性设置为 Cross 的 PictureBox。将你在练习 3 中构建的形状类复制到其中。要将类从一个项目复制到另一个项目，你可以在新项目中创建同名类，然后将代码复制粘贴进去。或者你可以：

  - 将类的文件复制到新项目的目录中。
  - 使用项目菜单的“添加现有项”命令将类添加到项目中。
  - 编辑类的代码并更改其命名空间语句，使其使用与项目其余部分相同的命名空间。（你可以在主窗体代码的顶部查看该语句应是什么样。）

  接下来创建一个名为 Shapes 的类级 `List<Shape>`。

  编写代码以允许用户在 PictureBox 上选择一个矩形。

  - 创建两个名为 StartPoint 和 EndPoint 的类级 Point 变量。还创建一个名为 Drawing 的类级 bool 变量并将其初始化为 false。
  - 在 PictureBox 的 MouseDown 事件处理程序中，将鼠标位置保存到 StartPoint 和 EndPoint 中，并将 Drawing 设置为 true。
  - 在 PictureBox 的 MouseMove 事件处理程序中，如果 Drawing 为 false，则返回。否则，将鼠标当前位置保存到 EndPoint 并刷新 PictureBox。
  - 在 PictureBox 的 MouseUp 事件处理程序中，如果 Drawing 为 false，则返回。否则，如果 StartPoint 和 EndPoint 的 X 和 Y 坐标不同，则使用它们创建一个新的 Rect 并将其添加到 Shapes 列表中。
  - 在 PictureBox 的 Paint 事件处理程序中，遍历 Shapes 列表并使其中包含的对象自行绘制。然后如果 Drawing 为 true，则绘制一个以 StartPoint 和 EndPoint 为角的红色虚线矩形。（提示：DrawRectangle 方法无法绘制宽度或高度为负的矩形，因此你需要确定新选定矩形的左上角位置。Math.Min 和 Math.Abs 方法可能有帮助。）

  ![](img/d5be6ade75773ca6cec5c78f96a98bb1_407_0.png)

  图 25-3

- 5. [图形，困难] 复制你在练习 4 中构建的程序并添加图 25-3 中显示的包含四个下拉按钮的工具栏。

  下拉按钮代表用户选择的形状、线条粗细、前景色和背景色。当用户在 PictureBox 上完成区域选择时，将适当的形状添加到 Shapes 列表中。提示：

  - 使用菜单项的属性来存储所选值。
  - 使用菜单项的 Tag 属性来存储线条粗细值。（当你需要它们时，需要解析这些值。）

