
## 使用 SolidColorBrush

`<SolidColorBrush>` 元素使用纯色绘制区域。编辑上一节中创建的 `UI.xaml` 文件，并将其内容替换为以下内容：

```
~~~xml
<Canvas
    xmlns="http://schemas.microsoft.com/client/2007"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">

  <Ellipse
    Canvas.Left="10" Canvas.Top="10"
    Height="100" Width="100"
    Stroke="Black"
    StrokeThickness="10"
    Fill="Yellow" />

  <Ellipse
    Canvas.Left="120" Canvas.Top="10"
    Height="100" Width="100"
    Stroke="Black"
    StrokeThickness="10"
    Fill="#A3FC96" /> <!-- 6-digit hexadecimal -->

  <Ellipse
    Canvas.Left="10" Canvas.Top="120"
    Height="100" Width="100"
    Stroke="Black"
    StrokeThickness="10"
    Fill="#A3FC96FF" />
  <!-- 6-digit hexadecimal + 2-digit for alpha/opacity value -->

  <Ellipse
    Canvas.Left="120" Canvas.Top="120"
    Height="100" Width="100"
    Stroke="Black"
    StrokeThickness="10">
    <Ellipse.Fill>
      <SolidColorBrush Color="LightBlue"/>
    </Ellipse.Fill>
  </Ellipse>

</Canvas>
~~~
```

在此示例中，`Fill` 属性指定用于填充特定元素的纯色。在 Web 浏览器中重新加载 `Default.html` 文件，并在浏览器中观察输出结果（见图 19-12）。

![](img/a977a875c7c627b45d939729705a252e_654_0.png)

**图 19-12**

## 使用 LinearGradientBrush

<LinearGradientBrush> 元素使用线性渐变绘制区域。再次编辑 UI.xaml 文件，将其内容替换为以下内容。

```
<Canvas xmlns="http://schemas.microsoft.com/client/2007" xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">
  <Ellipse Canvas.Left="10" Canvas.Top="10" Height="100" Width="100" Stroke="Black" StrokeThickness="10">
    <Ellipse.Fill>
      <LinearGradientBrush><!-- fill is diagonal by default -->
        <GradientStop Color="Yellow" Offset="0.25" />
        <GradientStop Color="Red" Offset="0.5" />
        <GradientStop Color="Blue" Offset="0.75" />
      </LinearGradientBrush>
    </Ellipse.Fill>
  </Ellipse>
  <Ellipse Canvas.Left="120" Canvas.Top="10" Height="100" Width="100" Stroke="Black" StrokeThickness="10">
    <Ellipse.Fill>
      <!-- fill is horizontal -->
      <LinearGradientBrush StartPoint="0,0" EndPoint="1,0">
        <GradientStop Color="Yellow" Offset="0.25" />
        <GradientStop Color="Red" Offset="0.5" />
        <GradientStop Color="Blue" Offset="0.75" />
      </LinearGradientBrush>
    </Ellipse.Fill>
  </Ellipse>
</Canvas>
```

这里您使用 <Ellipse.Fill> 元素用 <LinearGradientBrush> 元素填充每个椭圆形。在 Web 浏览器中重新加载 Default.html 文件。图 19-13 显示了输出结果。

![](img/a977a875c7c627b45d939729705a252e_655_0.png)

图 19-13

## 使用 ImageBrush

<ImageBrush> 元素使用图像绘制区域。假设您已将图 19-15 所示的图像保存为 C:\Silverlight\USFlag.jpg，编辑已创建的 UI.xaml 文件，并将其内容替换为以下内容：

![](img/a977a875c7c627b45d939729705a252e_657_0.png)

```
<Canvas
xmlns="http://schemas.microsoft.com/client/2007"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml" >

<Ellipse
Canvas.Left="10" Canvas.Top="10"
Height="100" Width="100"
Stroke="Black"
StrokeThickness="10">
<Ellipse.Fill>
<ImageBrush ImageSource="USFlag.jpg"/>
</Ellipse.Fill>
</Ellipse>

<Ellipse
Canvas.Left="120" Canvas.Top="10"
Height="100" Width="100"
Stroke="Black"
StrokeThickness="10">
<Ellipse.Fill>
<ImageBrush ImageSource="USFlag.jpg" Stretch="Uniform"/>
</Ellipse.Fill>
</Ellipse>

</Canvas>
```

在 Web 浏览器中重新加载 Default.html 以查看输出结果（见图 19-16）。

![](img/a977a875c7c627b45d939729705a252e_657_1.png)

## 使用 Expression Blend 2 创建 XAML

虽然您可以手工编码 UI，但更简单的方法是使用设计工具以图形方式设计和创建 UI。

Microsoft Expression Blend 2 是用于为 Windows 和 Silverlight 创建引人入胜的网络连接体验的专业设计工具。目前为第 2 版，您可以从 www.microsoft.com/downloads 下载 Expression Blend 2 的 30 天试用版。

本节介绍如何使用 Expression Blend 2 构建 Silverlight 应用程序并使用 JavaScript 以编程方式与 Silverlight 应用程序的内容进行交互。

### 使用 Expression Blend 2

通过选择“开始”⇨“程序”⇨“Microsoft Expression”⇨“Microsoft Expression Blend 2”启动 Expression Blend 2。通过选择“新建项目”项创建新项目。

在“新建项目”对话框中，选择 Silverlight 1 Site 项目类型并将项目命名为 `RoundButton`（见图 19-17）。单击“确定”。

![](img/a977a875c7c627b45d939729705a252e_658_0.png)

图 19-17

在设计视图中，双击 `Canvas` 控件以将其插入页面（见图 19-18）。

## 第 II 部分：使用 C# 进行应用程序开发

![](img/a977a875c7c627b45d939729705a252e_659_0.png)

图 19-18

在工具箱中右键单击 Rectangle 控件，并选择 Ellipse（见图 19-19）。

![](img/a977a875c7c627b45d939729705a252e_659_1.png)

图 19-19

双击 Ellipse 元素将其添加到页面。将 Ellipse 对象拖到“对象和时间轴”窗口中的 Canvas 对象上，以将其移入 Canvas 控件（见图 19-20）。

![](img/a977a875c7c627b45d939729705a252e_660_0.png)

图 19-20

页面现在看起来像图 19-21。

![](img/a977a875c7c627b45d939729705a252e_660_1.png)

图 19-21

选中 Ellipse 对象后，选择“属性”检查器，并单击（见图 19-22）：

- [ ] 描边
- [ ] 纯色画刷
- [ ] 为 StrokeThickness 指定 5

![](img/a977a875c7c627b45d939729705a252e_661_0.png)

图 19-22

接下来，单击以下内容（见图 19-23）：

- [ ] 填充
- [ ] 渐变画刷
- [ ] 为 R 指定 180、为 G 指定 248、为 B 指定 8、为 A 指定 100%

![](img/a977a875c7c627b45d939729705a252e_662_0.png)

图 19-23

单击“画刷变换”工具，并观察 Ellipse 元素上的箭头（见图 19-24）。

![](img/a977a875c7c627b45d939729705a252e_662_1.png)

图 19-24

![](img/a977a875c7c627b45d939729705a252e_664_0.png)

图 19-27

双击 `TextBlock` 元素将其添加到页面。如常，将其移入 `Canvas` 控件并在 `TextBlock` 元素中键入 OK（见图 19-28）。

![](img/a977a875c7c627b45d939729705a252e_664_1.png)

图 19-28

选中 `TextBlock` 对象后，选择“属性”检查器，并单击（见图 19-29）：

- 前景色
- 纯色画刷
- 为 R 指定 251、为 G 指定 219、为 B 指定 8、为 A 指定 100%

## 第 II 部分：使用 C# 进行应用程序开发

![](img/a977a875c7c627b45d939729705a252e_665_0.png)

图 19-29

将 TextBlock 的字体大小设置为 18 并加粗（见图 19-30）。

![](img/a977a875c7c627b45d939729705a252e_665_1.png)

图 19-30

在“对象和时间轴”窗口中按住 Control 键单击以下控件，右键单击它们，然后选择“分组到”⇔“画布”（见图 19-31）；

- [ ] Ellipse
- [ ] EllipsePressed
- [ ] TextBlock

![](img/a977a875c7c627b45d939729705a252e_666_0.png)

图 19-31

所有选中的控件现在已分组为一个。命名新的复合控件为 RoundButton（见图 19-32）。

![](img/a977a875c7c627b45d939729705a252e_666_1.png)

图 19-32

切换到项目的 XAML 视图（见图 19-33）。

![](img/a977a875c7c627b45d939729705a252e_667_0.png)

图 19-33

### 使用 JavaScript 脚本化 UI

将以下突出显示的代码插入 RoundButton Canvas 控件中：

```
<Canvas
    xmlns="http://schemas.microsoft.com/client/2007"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Width="640" Height="480"
    Background="White"
    x:Name="Page">
    <Canvas Width="100" Height="100" Canvas.Top="8" Canvas.Left="8">
        <Canvas Width="100" Height="100" x:Name="RoundButton"
            MouseLeftButtonDown="ButtonClicked"
            MouseLeftButtonUp="ButtonReleased"
            MouseLeave="ButtonReleased">
        </Canvas>
    </Canvas>
</Canvas>
```

在“项目”窗口中，双击 Page.xaml.js 文件。将以下代码块追加到文件末尾：

```
function ButtonClicked(sender, eventArgs)
{
    if(sender.name == "RoundButton")
    {
        //---Get a reference to the ellipse---
        var pressedEllipse = sender.findName("EllipsePressed");
        pressedEllipse.opacity = 1;
    }
}

function ButtonReleased(sender, eventArgs)
{
    if(sender.name == "RoundButton")
    {
        //---Get a reference to the ellipse---
        var pressedEllipse = sender.findName("EllipsePressed");
        pressedEllipse.opacity = 0;
    }
}
```
