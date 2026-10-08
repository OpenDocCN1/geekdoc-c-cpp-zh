```
}
private void Window_Loaded(object sender, RoutedEventArgs e)
{
    ChartHost.Child = new SimpleChart();
}
```

Code file [MainWindow.xaml.cs] available for download at Wrox.com

Your chart is hosted in the WPF MainWindow, and your application is ready to run. Figure 14-15 shows that it works as expected.

![](bbox=[0.147, 0.343, 0.577, 0.574])

FIGURE 14-15: Chart hosted in a WPF window

> Although the chart is hosted in a WPF window, it uses GDI+ technology to render the chart. Right now, Microsoft does not ship a WPF chart with Visual Studio 2010. When you need to use one, you can buy one from your preferred control vendor or examine free WPF chart solutions.

# USING CHART CONTROLS

Earlier in this chapter, you read an overview of chart creation, and you became familiar with a few chart elements (such as chart areas, series, data points, titles and so on). Now, let's dive deeper into the use of chart controls.