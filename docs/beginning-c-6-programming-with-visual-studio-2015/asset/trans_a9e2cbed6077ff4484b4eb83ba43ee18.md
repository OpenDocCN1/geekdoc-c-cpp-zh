
- 13. 选择“功能”选项卡并确保已勾选“图片库”功能。
- 14. 运行应用程序。

## 工作原理

代码使用三个 RelativePanel 来移动其内容。这些面板本身没有任何定位指令；相反，整个布局都在视觉状态管理器中定义。在本例中，我们使用两个自适应触发器，一个在视图宽度大于 720 像素时激活，另一个在视图宽度大于 0 像素时激活。

FlipView 本身在示例中几乎是最少的代码。

```
<FlipView x:Name="flipView" VerticalAlignment="Stretch"
HorizontalAlignment="Stretch" >
<FlipView.ItemTemplate>
<DataTemplate>
<Image x:Name="image" Source="{Binding}" Stretch="Uniform"/>
</DataTemplate>
</FlipView.ItemTemplate>
</FlipView>
```

在此代码中，我们告诉 FlipView 应使用此处定义的 ItemTemplate，而该模板仅包含一个 Image 控件。由此可见，你可以使用 FlipView 显示任何内容，而不仅仅是图像。

GetFiles 方法中的代码演示了可在应用中用于访问文件和资源的多个接口。本章后面我们将讨论沙盒应用的概念以及它们对代码的限制，但你已在此示例中看到了其中的一些实际应用。以下代码在应用有权访问时获取 StorageFolder 对象，如果没有访问权限则抛出 UnauthorizedAccessException 异常。

```
StorageFolder picturesFolder = KnownFolders.PicturesLibrary;
```

在普通的 .NET 中你没有这个类，并且是否授予访问权限的判定基于用户在文件系统中的权限。对于应用来说，这完全不同。在这里，你必须提前声明应用需要访问哪些资源，并且用户必须接受这些资源才能运行应用程序。在步骤 13 中，你声明了应用将包含访问图片库的功能。如果你没有这样做，运行应用时会收到异常。

接下来你使用 StorageFolder 的 GetFilesAsync 方法按日期顺序检索文件。

一旦获得文件，我们通过在 StorageFile 对象上调用 OpenAsync 来打开它们

```
using (Windows.Storage.Streams.IRandomAccessStream fileStream = await file.
OpenAsync(FileAccessMode.Read))
```

这会返回一个可用于访问文件内容的文件流。在本例中，我们不想写入它，因此仅指定只读访问。

最后，我们将 FlipView 的 ItemsSource 设置为从图片库加载的图像列表。

## 序列化、流和异步编程

在第 14 章中，你使用 `[Serializable]` 属性允许类被序列化。.NET for Universal 应用不包含此属性，但你可以使用类似的 `[DataContract]` 属性代替。`DataContract` 属性与 `DataContractSerializer` 类配合使用以序列化类的内容。为了将序列化内容写入或读取磁盘，你需要使用一些文件访问类型，但与普通 .NET 不同，你不能直接创建这些类型。相反，你使用文件选择器创建流对象，然后可将其与 `DataContractSerializer` 一起使用以保存和加载文件。

> 注意 本章可在 www.wrox.com/go/beginningvisualc#2015programming 下载的项目包含一个证书文件，你可能无法使用，但可以自行生成。请按以下步骤操作：
> 
> 1. 在项目打开的情况下，双击文件 Package.appxmanifest。
> 2. 选择 Packaging 选项卡。
> 3. 单击 Choose Certificate。
> 4. 从 Configure Certificate 中选择 Create test certificate。
> 5. 单击 OK。

下一个“试一试”演示使用 `DataContractSerializer` 与 `FileOpenPicker` 和 `FileSavePicker` 创建的流配合，以加载和保存数据模型的 XML 表示形式。

## 试一试 磁盘访问：Ch23Ex03

- 1. 在 Visual Studio 中通过选择 Blank App (Universal Windows) 创建一个新项目，并将其命名为 DataSerialization。
- 2. 在项目中创建一个名为 AppData 的新类。
- 3. 使用 `[DataContract]` 属性标记该类，并在该部分添加 `System.Runtime.Serialization` 命名空间：
- 4. 向类添加一个类型为 `int` 的属性，并使用 `[DataMember]` 属性标记它：

```
using System.Runtime.Serialization;

namespace DataSerialization
{
    [DataContract]
    class AppData
    {
    }
}
```

```
[DataMember]
public int TheAnswer { get; set; }
```

- 4. 重复步骤 3 两次，使项目中共有三个页面，分别命名为 BlankPage2 和 BlankPage3。
- 5. 打开 App.xaml.cs 代码隐藏文件并找到 OnLaunched 方法。此方法使用了你刚刚删除的 MainPage，因此将其引用改为 BlankPage1。
- 6. 在 BlankPage1 中，向网格中插入一个堆栈面板、一个 TextBlock 和三个按钮：

```
<Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
<TextBlock x:Name="textBlockCaption" Text="Page 1" HorizontalAlignment="Center" Margin="10" VerticalAlignment="Top"/>
<StackPanel Orientation="Horizontal" Grid.Row="1" HorizontalAlignment="Center">
<Button Content="Page 2" Click="buttonGoto2_Click" />
<Button Content="Page 3" Click="buttonGoto3_Click" />
<Button Content="Back" Click="buttonGoBack_Click" />
</StackPanel>
</Grid>
```

- 7. 按如下方式添加单击事件的处理程序：

```
private void buttonGoto2_Click(object sender, RoutedEventArgs e)
{
    Frame.Navigate(typeof(BlankPage2));
}
private void buttonGoto3_Click(object sender, RoutedEventArgs e)
{
    Frame.Navigate(typeof(BlankPage3));
}
private void buttonGoBack_Click(object sender, RoutedEventArgs e)
{
    if (Frame.CanGoBack) this.Frame.GoBack();
}
```

- 8. 打开第二个页面（BlankPage2）并向其添加一个类似的堆栈面板：

```
<TextBlock x:Name="textBlockCaption" Text="Page 2" HorizontalAlignment="Center" Margin="10" VerticalAlignment="Top"/>
<StackPanel Orientation="Horizontal" Grid.Row="1" HorizontalAlignment="Center">
<Button Content="Page 1" Click="buttonGoto1_Click" />
<Button Content="Page 3" Click="buttonGoto3_Click" />
<Button Content="Back" Click="buttonGoBack_Click" />
</StackPanel>
```

- 9. 向事件处理程序添加导航：

```
private void buttonGoto1_Click(object sender, RoutedEventArgs e)
{
    Frame.Navigate(typeof(BlankPage1));
}
private void buttonGoto3_Click(object sender, RoutedEventArgs e)
{
    Frame.Navigate(typeof(BlankPage3));
}
private void buttonGoBack_Click(object sender, RoutedEventArgs e)
{
    if (Frame.CanGoBack) this.Frame.GoBack();
}
```

## 工作原理

运行应用时，你现在可以使用命令栏按钮在已访问的页面列表中前后移动。命令栏本身非常易于使用。

命令栏使用三种类型构建。第一种是 AppBarToggleButton。

```
<AppBarToggleButton x:Name="toggleButtonBold" Icon="Bold" Label="Bold" Click="AppBarToggleButtonBold_Click" />
```

这种类型的按钮可用于显示可打开或关闭的状态。

第二种类型是 AppBarButton，它的工作方式与其他按钮一样，事实上你可以看到 AppBarButtonBack 按钮的单击事件由与前一个示例中的 ButtonBack 相同的事件处理程序处理。

```
<AppBarButton Icon="Back" Label="Back" Click="buttonGoBack_Click"/>
```

命令栏中使用的第三种类型是 AppBarSeparator。此控件仅在栏上显示分隔符。

最后，两个按钮位于 CommandBar.SecondaryCommands 标签内：

```
<CommandBar.SecondaryCommands>
<AppBarButton Icon="Camera" Label="Take picture" />
<AppBarButton Icon="Help" Label="Help" />
</CommandBar.SecondaryCommands>
</CommandBar>
```

这些命令不会直接显示在命令栏上。相反，当你单击显示的三个点时，它们会作为下拉菜单显示。

## 管理状态

与桌面应用程序不同，应用必须随时准备被挂起。这发生在用户切换到另一个应用或桌面时，因此这是所有应用都必须处理的非常常见的情况。当应用被挂起时，Windows 会保存你的变量和数据结构的值，并在应用恢复时将其还原。但是，你的应用可能已被挂起很长时间，因此如果有随时间变化的数据，例如新闻源，则应在应用恢复时刷新它。

当应用被挂起时，你还应考虑保存应在应用的不同调用之间保持持久的数据，因为如果随后 Windows 或用户终止应用，你将没有机会这样做。

当你的应用即将被挂起时，会发送一个 Suspending 事件，你应处理它。当应用恢复运行时，它会收到 Resuming 事件。通过处理这两个事件并保存应用程序的状态，你可以将应用恢复到挂起前的状态，用户不应察觉到任何变化。
