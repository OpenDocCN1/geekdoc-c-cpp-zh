

# MEDIACOMMANDS

MediaCommands 类定义了适用于音频和视频等不同媒体类型的命令。这些命令中没有预定义的手势。表 K-4 显示了这些命令。

**表 K-4:** MediaCommands 命令

| 命令 |
| --- |
| BoostBass 增强低音 |
| ChannelDown 频道向下切换 |
| ChannelUp 频道向上切换 |
| DecreaseBass 降低低音 |
| DecreaseMicrophoneVolume 减小麦克风音量 |
| DecreaseTreble 降低高音 |
| DecreaseVolume 减小音量 |
| FastForward 快进 |
| IncreaseBass 增大低音 |
| IncreaseMicrophoneVolume 增大麦克风音量 |
| IncreaseTreble 增大高音 |
| IncreaseVolume 增大音量 |
| MuteMicrophoneVolume 静音麦克风音量 |
| MuteVolume 静音音量 |
| NextTrack 下一首曲目 |
| Pause 暂停 |
| Play 播放 |
| PreviousTrack 上一曲目 |
| Record 录制 |
| Rewind 回退 |
| Select 选择 |
| Stop 停止 |
| ToggleMicrophoneOnOff 切换麦克风开关状态 |
| TogglePlayPause 切换播放/暂停 |

# NAVIGATIONCOMMANDS

NavigationCommands 类定义了适用于遵循 Web 导航模型的应用程序的命令。表 K-5 显示了这些命令及其键盘手势。

表 K-5：

| 命令 | 手势 |
| --- | --- |
| BrowseBack 向后浏览 | [Alt]+Left |
| BrowseForward 向前浏览 | [Alt]+Right |
| BrowseHome 回首页 | [Alt]+[Home] |
| BrowseStop 停止浏览 | [Alt]+[Escape] |
| DecreaseZoom 缩小 | N/A |
| Favorites 收藏 | [Ctrl]+I |
| FirstPage 第一页 | N/A |
| GoTabPage 转到页页 | N/A |
| IncreaseZoom 放大 | N/A |
| LastPage 最后一页 | N/A |
| NavigateJournal 导航日志 | N/A |
| NextPage 下一页 | N/A |
| PreviousPage 上一页 | N/A |
| Refresh 刷新 | [F5] |
| Search 搜索 | [F3] |
| Zoom 缩放 | N/A |

# COMMANDS IN XAML

要在 XAML 中使用命令，只需将控件的 Command 属性设置为适当的对象。例如，以下代码定义了编辑（Edit）菜单中的若干项，并设置了它们的 Command 属性：

```
<MenuItem Header="Edit">
<!-- 调用默认命令的菜单项。 -->
  <MenuItem Command="ApplicationCommands.Copy"/>
  <MenuItem Command="ApplicationCommands.Cut"/>
  <MenuItem Command="ApplicationCommands.Paste"/>
  <Separator/>
  <MenuItem Command="ApplicationCommands.Undo"/>
  <MenuItem Command="ApplicationCommands.Redo"/>
</MenuItem>
```

使用 CommandTarget 属性使命令适用于特定的代码。以下代码创建了一个按钮，该按钮对名为 txtTop 的 TextBox 应用 ApplicationCommands.Cut 命令：

```
<Button Row="0" Column="1" Margin="2"
Content="Binding RelativeSource={RelativeSource}, Command=Text}"
Command="ApplicationCommands.Cut"
CommandTarget="{Binding ElementName=txtTop}"/>
```

# COMMANDS IN-BEHIND

某些命令（例如 Edit 命令）具有预定义的行为。对于其他命令，你需要定义行为。

以下代码显示了程序如何定义命令绑定（command bindings）。这些绑定将 New 等命令与代码事件处理程序绑定，以便命令在需要确定何时可用以及应该执行什么操作。

```
<Window.CommandBindings>
<CommandBinding Command="New"
CanExecute="DocumentNewAllowed" Exec="DocumentNew"/>
<CommandBinding Command="Open"
CanExecute="DocumentOpenAllowed" Exec="DocumentOpen"/>
<CommandBinding Command="Save"
CanExecute="DocumentSaveAllowed" Exec="DocumentSave"/>
<CommandBinding Command="SaveAs"
CanExecute="DocumentSaveAsAllowed" Exec="DocumentSaveAs"/>
<!-- Close 绑定定义在代码中
    仅为了如何操作。 -->
<CommandBinding Command="Close"
CanExecute="DocumentCloseAllowed" Exec="DocumentClose"/>
-->
</Window.CommandBindings>
```

以下 C# 代码显示了 New 命令的后台代码（code-behind）：

```sharp
// 如果我们可以执行 New 操作，则返回 true。
private void DocumentNewAllowed(Object sender, ExecuteRoutedEventArgs e)
{
    e.CanExecute = (!m_IsDirty);
}
// 执行 New 操作。
private void DocumentNew(Object sender, ExecutedRoutedEventArgs e)
{
    // 清除 Canvas 上任何现有控件。
    canvasDrawing.Children.Clear();
    // 显示画布。
    drawing.Visibility = Visibility.Visible;
    m_FileName = null;
}
```

# Bitmap L-1 Effects

表 L-1 汇总了 WPF 的位图效果。

| 效果类 | 结果 |
|---|---|
| BevelBitmapEffect | 斜角外观 |
| BlurBitmapEffect | 模糊外观 |
| DropShadowBitmapEffect | 对象后的阴影 |
| EmbossBitmapEffect | 浮雕外观 |
| OuterGlowBitmapEffect | 对象后的发光 |

图 L-1 显示的 BitmapEffects 程序演示了位图效果类。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_570_0.png)

图 L-1

以下 XAML 代码显示了程序 BitmapEffects 如何显示阴影。其他位图效果类也类似。

```xml
<stackPanel>
  <Image Source="Volleyball.png" Stretch="Uniform" Height="90">
    <Image.BitmapEffect>
      <DropShadowBitmapEffect/>
    </Image.BitmapEffect>
  </Image>
  <Label Content="Drop Shadow">
    <Label.BitmapEffect>
      <DropShadowBitmapEffect/>
    </Label.BitmapEffect>
  </Label>
</stackPanel>
```

# Styles

Style（样式）允许你定义一组属性，并在多个控件之间共享。通常，Style 包含定义特定值的 Setter 对象。你可以创建两种样式：命名的非命名的。

# 命名的样式

要创建一个命名的样式，请给它一个 x:Name 属性。之后你可以通过 StaticResource 引用样式。以下 XAML 代码定义并使用了名为 stubButton 的样式：

```xml
<StackPanel Orientation="Horizontal">
  <StackPanel.Resources>
    <Style Key="stubButton" TargetType="Button">
      <Setter Property="Width" Value="100"/>
      <Setter Property="Height" Value="30"/>
      <Setter Property="Margin" Value="5"/>
      <Setter Property="FontSize" Value="14"/>
      <Setter Property="FontWeight" Value="Bold"/>
      <EventSetter Event="Click" Handler="Button_Clicked"/>
    </Style>
  </StackPanel.Resources>
  <Button Content="Customers" Style="{StaticResource stubButton}" Width="150"/>
  <Button Content="Orders" Style="{StaticResource stubButton}"/>
  <Button Content="Inventory" Style="{StaticResource stubButton}"/>
</StackPanel>
```

# 非命名的样式

要创建一个非命名的样式，简化 x:Name 属性。非命名样式适用于范围内的所有相应对象。例如，如果你在 StackPanel 的资源部分定义了 Button 样式，那么 StackPanel 内的任何 Button 都会使用它。

以下代码定义了一个与上一节描述类似的非命名样式：

```xml
<StackPanel Orientation="Horizontal">
  <StackPanel.Resources>
    <Style TargetType="Button">
      <Setter Property="Width" Value="100"/>
      <Setter Property="Height" Value="30"/>
      <Setter Property="Margin" Value="5"/>
      <Setter Property="FontSize" Value="14"/>
      <Setter Property="FontWeight" Value="Bold"/>
      <EventSetter Event="Click" Handler="Button_Clicked"/>
    </Style>
  </StackPanel.Resources>
  <Button Content="Customers" Width="150"/>
  <Button Content="Orders"/>
  <Button Content="Inventory"/>
  <Button Content="Maintenance" Style="(x:Null)" Width="75" Height="25" Click="Maintenance_Clicked"/>
</StackPanel>
```

