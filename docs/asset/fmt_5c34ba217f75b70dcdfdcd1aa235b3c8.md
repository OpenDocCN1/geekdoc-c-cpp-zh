
This method sets the appropriate bytes in the data array that corresponds to x- and y-coordinates passed in as parameters. Each point plotted corresponds to a pixel, and each pixel consists of 4 bytes, as described earlier. Any pixels left unset are displayed as black. The value `0xBF` for the alpha blend byte indicates that the corresponding pixel should be displayed with a moderate intensity; if you decrease this value, the pixel will become fainter, while setting the value to `0xFF` (the maximum value for a byte) will display the pixel at its brightest intensity.

## 9. On the Debug menu, click Start Debugging to build and run the application.

## 10. When the Graph Demo window appears, click Plot Graph, and then wait.

Please be patient. The application takes several seconds to generate and display the graph, and the application is unresponsive while this occurs. (Chapter 24 explains why this is, and also instructs you how to avoid this behavior.) The following image shows the graph. Note the value in the Duration (ms) label in the following figure. In this case, the application took 4,907 milliseconds (ms) to plot the graph. Note that this duration does not include the time to actually render the graph, which might be another few seconds.

### Note

The application was run on a computer with 8 GB of memory and a quad-core processor running at 2.40 GHz. Your times might vary if you are using a slower or faster processor with a different number of cores, or a computer with a greater or lesser amount of memory.

## Graph Demo

Plot Graph

Duration (ms):
4907

![](img/16f6e3fe08f01ddadb2741a92c392b0e_616_0.png)

11. Click Plot Graph again, and take note of the time required to redraw the graph. Repeat this action several times to obtain an average value.

### Note

You might find that occasionally the graph takes an extended time to appear (more than 30 seconds). This tends to occur if you are running close to the memory capacity of your computer and Windows has to page data between memory and disk. If you encounter this phenomenon, discard this time and do not include it when calculating your average.

12. Leave the application running and right-click an empty area of the taskbar. On the shortcut menu that appears, click Task Manager.

13. In the Task Manager window, click the Performance tab and display the CPU utilization. If the Performance tab is not visible, click More Details. Right-click the CPU Utilization graph, point to Change Graph To, and then click Overall Utilization. This action causes Task Manager to display the utilization of all the processor cores running on your computer in a single graph. The following image shows the Performance tab of Task Manager configured in this way:

![](img/16f6e3fe08f01ddadb2741a92c392b0e_617_0.png)

- 14. Return to the Graph Demo application and adjust the size and position of the application window and the Task Manager window so that both are visible.
- 15. Wait for the CPU utilization to level off, and then, in the Graph Demo window, click Plot Graph.
- 16. Wait for the CPU utilization to level off again, and then click Plot Graph again.
- 17. Repeat step 16 several times, waiting for the CPU utilization to level off between clicks.
- 18. In the Task Manager window, observe the CPU utilization. Your results will vary, but on a dual-core processor, the CPU utilization will probably be somewhere around 50–55 percent while the graph was being generated. On a quad-core machine, the CPU utilization will likely be somewhere between 25 and 30 percent, as shown in the image that follows. Note that other factors, such as the type of graphics card in your computer, can also impact the performance:

![](img/16f6e3fe08f01ddadb2741a92c392b0e_618_0.png)

19. Return to Visual Studio 2015 and stop debugging.

You now have a baseline for the time the application takes to perform its calculations. However, it is clear from the CPU usage displayed by Task Manager that the application is not making full use of the processing resources available. On a dual-core machine, it is using just over half of the CPU power, and on a quad-core machine, it is employing a little more than a quarter of the CPU. This phenomenon occurs because the application is single-threaded, and in a Windows application, a single thread can provide work only to a single core on a multicore processor. To spread the load over all the available cores, you need to divide the application into tasks and arrange for each task to be executed by a separate thread, each running on a different core. This is what you will do next.

## Using Performance Explorer to identity CPU bottlenecks

The GraphDemo application was specifically designed to create a CPU bottleneck at a known point (in the `generateGraphData` method). In the real world you might be aware that something is causing your application to run slowly and become unresponsive, but you might not know where the offending code is located. This is where the Visual Studio Performance Explorer and Profiler can prove invaluable.

The Profiler can sample the run-time state of the application periodically and capture information about which statement was running at the time. The more frequently a particular line of code is executed and the longer this line takes to run, the more frequently this statement will be observed. The Profiler uses this data to generate a run-time profile of the application and produce a report that details the hotspots in your code. These hotspots can be useful in identifying areas on which you should focus your optimizations. The following optional steps walk you through this process.

Note

Performance Explorer and the Profiler are not available in Visual Studio 2015 Community Edition.

- 1. In Visual Studio, on the Debug menu, point to Profiler, point to Performance Explorer, and then click New Performance Session. The Performance Explorer window should appear in Visual Studio:
- 2. 在 Performance Explorer 中，右键单击 Targets，然后单击 Add Target Project。GraphDemo 应用程序将被添加为目标。
- 3. 在 Performance Explorer 菜单栏中，单击 Actions，然后单击 Start Profiling。GraphDemo 应用程序开始运行。
- 4. 单击 Plot Graph 并等待图表生成。重复此过程几次，然后关闭 GraphDemo 应用程序。
- 5. 返回 Visual Studio 并等待 Profiler 分析收集的采样数据并生成报告，该报告应类似于以下内容：

# Sample Profiling Report

31,966 total samples collected

## Hot Path

| Function Name | Inclusive Samples % | Exclusive Samples % |
| dynamicClass.IL_STUB_WinRTtoCLR | 98.01 | 0.00 |
| GraphDemo.MainPage.plotButton_Click | 98.00 | 0.00 |
| GraphDemo.MainPage.generateGraphData | 91.06 | 31.59 |
| GraphDemo.MainPage.plotXY | 35.93 | 35.93 |
| [coreclr.dll] | 23.54 | 23.54 |

Related Views: Call Tree Functions

## Functions Doing Most Individual Work

| Name | Exclusive Samples % |
| GraphDemo.MainPage.plotXY | 36.84 |
| GraphDemo.MainPage.generateGraphData | 31.59 |
| [coreclr.dll] | 26.98 |

该报告显示了 CPU 利用率（应与您之前使用任务管理器观察到的情况相似，每次单击 Plot Graph 时都会出现峰值），以及应用程序的 Hot Path。该路径标识了应用程序中消耗最多处理的序列。在此情况下，应用程序在 `plotButton_Click` 方法中花费了 98% 的时间，执行 `generateGraphData` 方法花费了 91.06% 的时间，而在 `plotXY` 方法中花费了 35.93% 的时间。运行时（`coreclr.dll`）也消耗了相当多的时间（23.54%）。

请注意，您可以放大 CPU 利用率图的特定区域（使用鼠标单击并拖动），并将报告过滤为仅涵盖采样数据的放大部分。

6. 在报告的 Hot Path 部分中，单击 `GraphDemo.MainPage.generateGraphData` 方法。Report 窗口将显示该方法的详细信息，以及执行最昂贵语句所花费的 CPU 时间的比例：

![](img/16f6e3fe08f01ddadb2741a92c392b0e_622_0.png)

在此情况下，您可以看到 for 循环中的代码应该是任何优化工作的主要目标。

# Modify the GraphDemo application to use Task objects

- 1. 返回 Visual Studio 2015，并在代码和文本编辑器窗口中显示 `MainPage.xaml.cs` 文件，如果它尚未打开。
- 2. 检查 `generateGraphData` 方法。

此方法的目的是填充数据数组中的项。它使用基于 x 循环控制变量的外层 for 循环遍历数组，此处以粗体突出显示：

Click here to view code image

```
private void generateGraphData(byte[] data)
{
    int a = pixelWidth / 2;
    int b = a * a;
    int c = pixelHeight / 2;
```

```
for (int x = 0; x < a; x++)
{
    int s = x * x;
    double p = Math.Sqrt(b - s);
    for (double i = -p; i < p; i += 3)
    {
        double r = Math.Sqrt(s + i * i) / a;
        double q = (r - 1) * Math.Sin(24 * r);
```
