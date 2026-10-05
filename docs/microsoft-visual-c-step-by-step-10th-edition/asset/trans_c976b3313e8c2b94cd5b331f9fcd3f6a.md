
该方法继续执行，并在时长 `TextBlock` 中显示完成这些任务所需的时间。请注意，等待一个已经完成的任务并不是错误；`await` 运算符将直接返回并将控制权交给后续语句。

> > **更多信息**
> 第 24 章详细详细讨论了 `async` 修饰符和 `await` 运算符。

+   12. 找到 `cancelButton_Click` 方法。然后将此处加粗的代码添加到此方法中：

点击此处查看代码图像

```
private void cancelButton_Click(object sender, RoutedEventArgs e)
{
    if (tokenSource is not null)
    {
        tokenSource.Cancel();
    }
}
```

此代码检查 `tokenSource` 变量是否已实例化。如果是，代码将调用该变量的 `Cancel` 方法。

+   13. 在“调试”菜单上，选择“转调试启动”以编译并运行应用程序。

+   14. 在 `GraphDemo` 窗口中，选择“Plot Graph”，并验证图表是否像以前一样出现。注意到生成图表所需更长时间。这是因为 `generateGraphData` 方法执行的迭代次数在增加。

+   15. 再次选择“Plot Graph”，然后快速选择“Cancel”。

如果你动作足够快，在图表数据生成之前选择了“Cancel”，此操作将导致正在运行的任务方法返回。数据是不完整的，因此图表会出现空洞，如图所示。空洞的大小取决于你选择“Cancel” 的速度。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_870_0.png)

16. 关闭 `GraphDemo` 应用程序并返回 Visual Studio。

你可以通过检查 `Task` 对象的 `Status` 属性来确定任务是否已完成或被取消。`Status` 属性包含来自 `System.Threading.Tasks.TaskStatus` 举的值。以下列表描述了你可能会遇到的一些状态值（还有其他值）：

- *Created*：这是任务的初始状态。它已被创建，但尚未调度运行。
- *WaitingToRun*：任务已就绪，但尚未开始运行。
- *Running*：任务当前正在由线程执行。
- *RanToCompletion*：任务成功完成，没有任何任何未处理的异常。
- *Canceled*：任务在开始运行之前被取消，或者确认了已取消并在不抛出异常的情况下完成。
- *Faulted*：任务由于发生异常而终止。

在下一个练习中，你将报告每个任务的状态，这样你就可以看到它们何时完成或被取消。

# 取消并行 For 或 Each 循环

`Parallel.For` 和 `Parallel.ForEach` 方法没有提供直接访问已创建的 `Task` 对象的方法。.NET 运行时使用其自己的启发式算法，根据可用资源和计算机的当前负载来确定使用的最佳数量。

如果你想提前停止 `Parallel.For` 或 `Parallel.ForEach` 方法，必须使用 `ParallelLoopState` 对象。你指定的指定循环体的方法包含一个额外的 `ParallelLoopState` 参数。`Parallel` 类会创建一个 `ParallelLoopState` 对象并将其传递给方法。`Parallel` 类使用此对象来存储有关每次调用的信息。方法可以调用该对象的 `Stop` 方法，以指示 `Parallel` 类不要尝试执行任何已经开始并结束的迭代。

后续示例显示了 `Parallel.For` 方法在每次迭代时调用 `doLoopWork` 方法。`doLoopWork` 方法检查迭代变量。如果它大于 `600`，方法调用 `ParallelLoopState` 参数的 `Stop` 方法。这会导致 `Parallel.For` 方法停止运行循环的后续迭代。（当前的迭代可能会继续执行完毕。）

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_871_0.png)

记住 `Parallel.For` 循环中的迭代并不是按照特定顺序运行的。因此，当迭代变量值为 `600` 时取消循环，并保证之前的 599 次迭代已经运行。同样，某些大于 600 的迭代可能已经完成。

点击此处查看代码图像

```
Parallel.For(0, 1000, doLoopWork);
...
private void doLoopWork(int i, ParallelLoopState p)
{
    if (i > 600)
    {
        p.Stop();
    }
}
```

# 显示每个任务的状态

+   1. 在 Visual Studio 中，在设计视图窗口中显示 `MainPage.xaml` 文件。
2. 在 XAML 格中，在最后的结束标记 `</Grid>` 之前向 `MainPage` 表单的定义添加以下标记，如下代码加粗所示：

点击此处查看代码图像

```
<Image x:Name="graphImage" Grid.Column="1" Stretch="Fill" />
</Grid>
<TextBlock x:Name="messages" Grid.Row="4" FontSize="18" HorizontalAlignment="Left"/>
</Page>
```

此标记在表单底部添加了一个名为 `messages` 的 `TextBlock` 控件。

+   3. 在代码文本编辑器中显示 `MainPage.xaml.cs` 文件并找到 `plotButton_Click` 方法。
4. 在 `plotButton_Click` 方法中，添加以下代码来处理任务状态。

点击此处查看代码图像

```csharp
private void plotButton_Click(object sender, RoutedEventArgs e)
{
    try
    {
        // ... 其他代码
    }
    catch (OperationCanceledException)
    {
        messages.Text = "任务已取消。";
    }
}
```
