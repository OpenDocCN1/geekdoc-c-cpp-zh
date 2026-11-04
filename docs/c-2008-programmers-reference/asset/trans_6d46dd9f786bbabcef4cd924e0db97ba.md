

## 第二部分：使用C#进行应用程序开发

![](img/a977a875c7c627b45d939729705a252e_679_0.png)

图19-51

按F5测试页面。页面加载完成后，视频会自动开始播放（见图19-52）。

![](img/a977a875c7c627b45d939729705a252e_679_1.png)

图19-52

### 禁用自动播放

虽然自动播放视频是一个有用的功能，但有时您可能希望禁用此功能。例如，如果页面中嵌入了多个视频，此功能实际上更多是困扰而非帮助。要禁用自动播放功能，只需将<MediaElement>元素中的AutoPlay属性设置为False，如下所示：

```xml
<Canvas
    xmlns="http://schemas.microsoft.com/client/2007"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Width="640" Height="480"
    Background="White"
    x:Name="Page">
    <MediaElement x:Name="WindowsMedia_wmv"
        Width="320" Height="240"
        Source="WindowsMedia.wmv"
        Stretch="Fill"
        Canvas.Top="8" Canvas.Left="8"
        AutoPlay="False"
    />
</Canvas>
```

那么如何以及何时让它播放呢？您可以在用户鼠标进入视频时以编程方式播放视频，并在鼠标离开视频时暂停视频。此外，如果用户单击视频，视频可以停止并返回到开头。为此，设置以下突出显示的属性：

```xml
<Canvas
    xmlns="http://schemas.microsoft.com/client/2007"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Width="640" Height="480"
    Background="White"
    x:Name="Page">
    <MediaElement x:Name="WindowsMedia_wmv"
        Width="320" Height="240"
        Source="WindowsMedia.wmv"
        Stretch="Fill"
        Canvas.Top="8" Canvas.Left="8"
        AutoPlay="False"
        MouseEnter="MouseEnter"
        MouseLeave="MouseLeave"
        MouseLeftButtonDown="MouseClick"
    />
</Canvas>
```

基本上，您是在为<MediaElement>元素处理的各种事件设置事件处理程序。要编写事件处理程序，请转到“项目”窗口并双击Page.xaml.cs文件。

## 第二部分：使用C#进行应用程序开发

将以下代码追加到Page.xaml.js文件中：

```javascript
function MouseEnter (sender, eventArgs)
{
    var obj = sender.findName("WindowsMedia_wmv");
    obj.play();
}
function MouseLeave (sender, eventArgs)
{
    var obj = sender.findName("WindowsMedia_wmv");
    obj.pause();
}
function MouseClick (sender, eventArgs)
{
    var obj = sender.findName("WindowsMedia_wmv");
    obj.stop();
}
```

findName()方法允许您以编程方式获取Silverlight页面上指定元素（通过其x:Name属性）的引用。在本例中，您引用的是MediaElement元素的一个实例。该对象支持play、pause和stop方法。

再次按F5测试应用程序。这一次，当鼠标悬停在视频上时，视频将开始播放；当鼠标离开时，视频将暂停。要重新从开头播放视频，只需单击视频。

### 创建镜像效果

您可以利用视频做的一件有趣的事情是创建镜像效果。例如，图19-53显示了一个视频在播放，其底部有一个镜像图像。

![](img/a977a875c7c627b45d939729705a252e_681_0.png)

图19-53

## 第19章：开发Silverlight应用程序

通过将页面切换到XAML视图并添加以下突出显示的代码来修改原始Canvas控件：

```xml
<Canvas
    xmlns="http://schemas.microsoft.com/client/2007"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Width="640" Height="480"
    Background="White"
    x:Name="Page">
    <MediaElement x:Name="WindowsMedia_wmv"
        Width="238" Height="156"
        Source="WindowsMedia.wmv"
        Stretch="Fill"
        Canvas.Top="124" Canvas.Left="8"
        AutoPlay="False"
        MouseEnter="MouseEnter"
        MouseLeave="MouseLeave"
        MouseLeftButtonDown="MouseClick">
        <MediaElement.RenderTransform>
            <TransformGroup>
                <ScaleTransform ScaleX="1" ScaleY="1"/>
                <SkewTransform AngleX="0" AngleY="-25"/>
                <RotateTransform Angle="0"/>
                <TranslateTransform X="0" Y="0"/>
            </TransformGroup>
        </MediaElement.RenderTransform>
    </MediaElement>
</Canvas>
```

这会将视频变换为图19-54所示的形状。

![](img/a977a875c7c627b45d939729705a252e_682_0.png)

图19-54

## 第二部分：使用C#进行应用程序开发

添加另一个<MediaElement>元素（突出显示的代码）以模拟镜像效果：

```xml
<Canvas
    xmlns="http://schemas.microsoft.com/client/2007"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Width="640" Height="480"
    Background="White"
    x:Name="Page">
    <MediaElement x:Name="WindowsMedia_wmv"
    Width="238" Height="156"
    Source="WindowsMedia.wmv"
    Stretch="Fill"
    Canvas.Top="124" Canvas.Left="8"
    AutoPlay="False"
    MouseEnter="MouseEnter"
    MouseLeave="MouseLeave"
    MouseLeftButtonDown="MouseClick">
    <MediaElement.RenderTransform>
        <TransformGroup>
            <ScaleTransform ScaleX="1" ScaleY="1"/>
            <SkewTransform AngleX="0" AngleY="-25"/>
            <RotateTransform Angle="0"/>
            <TranslateTransform X="0" Y="0"/>
        </TransformGroup>
    </MediaElement.RenderTransform>
    </MediaElement>
```

```xml
<MediaElement x:Name="WindowsMedia_wmv1"
    AutoPlay="False"
    MouseEnter="MouseEnter"
    MouseLeave="MouseLeave"
    MouseLeftButtonDown="MouseClick"
    Width="238.955" Height="99.454"
    Source="WindowsMedia.wmv"
    Stretch="Fill" Canvas.Left="149.319" Canvas.Top="379.884">
    <MediaElement.RenderTransform>
        <TransformGroup>
            <ScaleTransform ScaleX="1" ScaleY="-1"/>
            <SkewTransform AngleX="55" AngleY="-25"/>
            <TranslateTransform X="0" Y="0"/>
        </TransformGroup>
    </MediaElement.RenderTransform>
</MediaElement>
```

```xml
</Canvas>
```

## 第19章：开发Silverlight应用程序

现在您有两个视频，第二个视频镜像第一个视频（见图19-55）。

![](img/a977a875c7c627b45d939729705a252e_684_0.png)

图19-55

要为镜像图像创建半透明效果，请将opacity属性设置为0到1之间的值（此处设置为0.3）：

```xml
<MediaElement x:Name="WindowsMedia_wmv1"
AutoPlay="False"
MouseEnter="MouseEnter"
MouseLeave="MouseLeave"
MouseLeftButtonDown="MouseLeftButtonDown"
Width="238.955" Height="99.454"
Source="WindowsMedia.wmv"
Stretch="Fill" Canvas.Left="149.319" Canvas.Top="179.884"
Opacity="0.3">
```

## 第二部分：使用C#进行应用程序开发

修改Page.xaml.js中如下突出显示的代码块：

```javascript
//---make these variables global---
var obj, obj1;

if (!window.Media)
    Media = {};

Media.Page = function()
{
}

Media.Page.prototype =
{
    handleLoad: function(control, userContext, rootElement)
    {
        this.control = control;

        // Sample event hookup:
        rootElement.addEventListener("MouseLeftButtonDown", Silverlight.createDelegate(this, this.handleMouseDown));

        //--- the original video---
        obj = this.control.content.findName("WindowsMedia_wmv");
        //--- the reflected video---
        obj1 = this.control.content.findName("WindowsMedia_wmv1");

    },

    // Sample event handler
    handleMouseDown: function(sender, eventArgs)
    {
        // The following line of code shows how to find an element by name and
        call a method on it.
        // this.control.content.findName("Storyboard1").Begin();
    }
}

function MouseEnter (sender, eventArgs)
{
    //---mute the reflected video---
    obj1.volume=0;

    //---play the 2 videos---
    obj.play();
    obj1.play();
}
function MouseLeave (sender, eventArgs)
{
    //---pause the 2 videos---
}
```

