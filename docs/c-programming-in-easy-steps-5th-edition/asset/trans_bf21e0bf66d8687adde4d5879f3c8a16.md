

![](img/bf8dbdfb89042fadbaa73b4160c74bac_180_0.png)

在 UWP 应用中没有 **Enabled** 属性，而是使用 **IsEnabled**。

- 8. 在 **BtnReset_Click** 事件处理程序块中，插入语句将字符串赋值给 **<TextBlock>** 组件。

```
textBlock1->Text = "...";
textBlock2->Text = "...";
textBlock3->Text = "...";
textBlock4->Text = "...";
textBlock5->Text = "...";
textBlock6->Text = "...";
// Statements to be inserted here (Step 9).
```

- 9. 最后，插入语句设置 **<Button>** 状态。

```
BtnPick->IsEnabled = true;
BtnReset->IsEnabled = false;
```

![](img/bf8dbdfb89042fadbaa73b4160c74bac_180_1.png)

**BtnReset** 按钮仅将 **<TextBox>** 和 **<Button>** 组件恢复到其原始状态。

**MainPage.xaml.cpp** 代码隐藏页现在应如下图所示：

![](img/bf8dbdfb89042fadbaa73b4160c74bac_180_2.png)

- 10. 返回到 **MainPage.xaml** 文件，然后在 **XAML** 视图中，可以看到属性已自动添加到 **<Button>** 元素以调用事件处理程序代码。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_180_3.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_180_4.png)

请注意，第一个 for 循环在每次迭代中只包含一条要执行的语句，因此不需要大括号。

## 测试程序

通过上面的 C++ 代码添加了功能后，你现在可以针对两种设备测试该程序：

![](img/bf8dbdfb89042fadbaa73b4160c74bac_181_0.png)

- 1. 在 Visual Studio 标准工具栏上，选择 **x64** 体系结构的 **Debug** 和 **Local Machine** 选项，然后单击 **Start** 按钮为 PC 设备运行该应用。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_181_1.png)

- 2. 等待应用程序生成并加载，然后点击按钮测试其功能。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_181_2.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_181_3.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_181_4.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_181_5.png)

你必须将 PC 设置为 **开发人员模式**，路径为 **设置、更新和安全、开发人员**。

该应用在 PC 设备上看起来不错——数字正在随机化，按钮状态按需变化。

- 3. 现在，在 Visual Studio 标准工具栏上，选择 **Debug**，**Stop Debugging** 退出正在运行的程序。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_182_0.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_182_1.png)

你可以安全地忽略黑色框中出现的 DEBUG 数字，但如果不想看到它们，请选择 **Project**、**ProjectName Properties**、**Build**，然后取消选中 **Define DEBUG** 常量选项。

- 4. 在 Visual Studio 标准工具栏上，选择 **x86** 体系结构的 **Debug** 和大型 **Mobile Emulator** 选项，然后单击 **Start** 按钮为移动设备运行该应用。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_182_2.png)

- 5. 等待模拟器启动——这需要一些时间。

- 6. 当应用程序生成并加载后，你看到控件不可见——所以你无法测试其功能！

- 7. 这是怎么回事？单击模拟器的 **Rotate**（旋转）按钮之一，将其翻转为横向，然后寻找线索。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_182_3.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_182_4.png)

- 8. 啊哈！现在可以看到一些控件了，但这并不令人满意——需要对界面布局进行调整，以使应用在移动设备上看起来很好。

- 9. 再次在 Visual Studio 标准工具栏上，选择 **Debug**、**Stop Debugging** 退出正在运行的程序。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_182_5.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_183_0.png)

在内存最低、屏幕最小的模拟器上进行测试，在具有更好功能的模拟器上运行应该没问题。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_183_1.png)

不要单击模拟器窗口上的 X 按钮来停止正在运行的程序，因为那也会关闭模拟器。

## 调整界面

上面针对移动设备的应用测试未能令人满意地呈现控件，因为对于小屏幕设备来说界面太宽。幸运的是，可以使界面适应不同的屏幕尺寸，使其在移动设备上看起来也很不错。这种适应依赖于识别屏幕尺寸，并为窄屏设备更改 **XAML** 中 **<StackPanel>** 元素的方向：

![](img/bf8dbdfb89042fadbaa73b4160c74bac_184_0.png)

- 1. 打开 **MainPage.xaml**，然后在 XAML 视图中，将这些元素紧接在开始 **<Grid>** 元素下方、组件元素之前添加。

```xml
<VisualStateManager.VisualStateGroups>
    <VisualStateGroup>
        <!-- Elements to be inserted here (Steps 2-3) -->
    </VisualStateGroup>
</VisualStateManager.VisualStateGroups>
```

- 2. 接下来，插入用于识别宽屏的元素。

```xml
<VisualState x:Name="wideState">
    <VisualState.StateTriggers>
        <AdaptiveTrigger MinWindowWidth="641" />
    </VisualState.StateTriggers>
</VisualState>
```

- 3. 现在，插入用于识别窄屏并更改外部 **<StackPanel>** 的 **Orientation** 的元素。

```xml
<VisualState x:Name="narrowState">
    <VisualState.StateTriggers>
        <AdaptiveTrigger MinWindowWidth="0" />
    </VisualState.StateTriggers>

    <VisualState.Setters>
        <Setter
            Target="MainStack.Orientation" Value="Vertical" />
    </VisualState.Setters>
</VisualState>
```

**MainPage.xaml** 文件的开头现在应类似于下面的截图：

![](img/bf8dbdfb89042fadbaa73b4160c74bac_184_1.png)

XAML 代码识别与 HTML 代码中使用的相同的 `<!-- -->` 注释标记。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_184_2.png)

请记住，此应用中的外部 **<StackPanel>** 包含一个 **<Image>** 和一个嵌套的 **<StackPanel>**，它们以水平并排方式显示。如果垂直显示，它们应该一个在另一个上方。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_185_0.png)

- 4. 选择 **x64** 和 **Local Machine**，再次为 PC 设备运行该应用——它看起来和运行起来仍然很好。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_185_1.png)

- 5. 现在选择 **x86** 和 **Mobile Emulator**，为移动设备运行该应用——它现在看起来和运行起来也很好。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_185_2.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_185_3.png)

你可以通过按 Ctrl + K、Ctrl + D 让 Visual Studio 很好地格式化 XAML 代码。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_185_4.png)

虽然应用可能在模拟器上运行良好，但建议在部署前始终在真实设备上进行测试。

## 部署应用程序

上文已在 **Mobile Emulator**（移动模拟器）中测试了该应用，现在可以在部署之前在真实设备上进行测试：

![](img/bf8dbdfb89042fadbaa73b4160c74bac_186_0.png)

- 1. 在 Windows 10 设备上，从“**设置、更新和安全、开发人员**”菜单中选择“**开发人员模式**”。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_186_1.png)

- 2. 接下来，通过 USB 插口将设备连接到你的 PC。

- 3. 在 Visual Studio 工具栏上，选择 **ARM** 体系结构的 **Debug** 和 **Device** 选项，然后单击 **Start** 按钮，在连接的设备上运行该应用。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_186_2.png)

- 4. 等待应用程序生成并加载，然后点击按钮测试其功能。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_186_3.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_186_4.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_186_5.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_186_6.png)

你可以选择 **Remote Machine** 选项通过网络连接进行测试。

该应用看起来不错，数字在随机化，按钮状态按需变化——该应用可以部署了。

