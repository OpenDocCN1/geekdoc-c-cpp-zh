![](bbox=[0.012, 0.008, 0.273, 0.158])

![](bbox=[0.318, 0.008, 0.579, 0.158])

Still in the constructor, we create two QToolButton, each with an icon. These buttons allow the user to zoom in and out. The buttons' icons are stored in a resource file, so any application that uses the Plotter widget will need this entry in its .pro file.

```
RESOURCES = plotter.qrc
```

The resource file is similar to the one we have used for the Spreadsheet application:

```
<RCC>
<resource>
  <file>images/zoomin.png</file>
  <file>images/zoomout.png</file>
</resource>
</RCC>
```

The adjustSize() calls on the buttons set their sizes to be that of their size hints. The buttons are not put in a layout; instead, we will position them manually in the Plotter's resize event. Since we are not using any layouts, we must specify the buttons' parent explicitly by passing this to the QToolButton constructor.

The call to setPlotSettings() at the end completes the initialization.

```
void Plotter::setPlotSettings(const PlotSettings &settings)
{
  zoomStack.clear();
  zoomStack.append(settings);
  curZoom = 0;
  zoomInButton->hide();
  zoomOutButton->hide();
  refreshPixmap();
}
```