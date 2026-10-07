
# CHAPTER 5 CONTENT CONTROLS

```
<Separator/>
<MenuItem Header="Exit"/>
</MenuItem>
...
</Menu>
```

## UseSeparator

This program also has two ToolBar on the bottom. The upper ToolBar directly contains a series of Buttons with a Separator between the second and third Buttons. The result is the light vertical line in Figure 5-19.

The bottom ToolBar contains a ToolPanel that holds the Buttons. Normally the ToolBar changes the appearance of the Buttons so the Separator is invisible. To make the Separator visible again, using the following code to give the Separator some width and remove to its usual vertical line:

```
<Separator Width="10" Margin="0,0,0,0" Background="x:Null"/>
```

Note that you can use any block object as a Separator in a Toolbar. For example, the following Label also makes a horizontal gap in the Toolbar:

```
<Label Width="10"/>
```

# TreeView

The TreeView displays hierarchical data. For example, the UseTreeView example program in Figure 5-20 displays the organizational chart for a fictitious company. The dark triangles beside the Board of Directors, President/CEO, and other items indicate that those items are expanded to show the subitems they contain. The light grey, to show the next triangle to the CFO item indicates that the CFO item is collapsed to hide its subitems.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_135_0.png)

The TreeView object holds the values shown on the control. TreeItem can contain other objects, but if you just want to display text as in Figure 5-20, you can set the TreeView's Header property to the text you want to display.

You give the TreeView its hierarchical structure by placing TreeItems inside other TreeViews.

The following XAML code shows how the UseTreeView program builds its TreeView control:

```
<TreeView Margin="5">
<TreeView.Background>
<RadialGradientBrush>
<GradientStop Color="#FFFFFF" Offset="0"/>
<GradientStop Color="#FFFF3030" Offset="1"/>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_135_1.png)

```
</RadialGradientBrush>
<TreeView.Background>
  <TreeView Header="Board of Directors" IsExpanded="True">
    <TreeView Header="President/CEO" IsExpanded="True">
      <TreeView Header="CIO" IsExpanded="True">
        <TreeView Header="VP Information Systems"/>
        <TreeView Header="VP Digital Assets and Paranoia"/>
        <TreeView Header="VP Networks and Grosswalks"/>
      </TreeView>
      <TreeView Header="VP Administration" IsExpanded="True">
        <TreeView Header="Human Resources"/>
        <TreeView Header="Inhuman Resources"/>
      </TreeView>
      <TreeView Header="Advertising
```

Like ListView control, the TreeView control has advanced data-binding capabilities. Chapter 18 explains some TreeView data-binding techniques.

# SUMMARY

This chapter covers WPF's most useful content controls. These are the controls that a program uses to display content for the user but not to modify or manipulate.

This chapter provides a brief overview of the controls and gives enough detail for you to get started them. However, some of the controls are incredibly complex. For example, the ListView and TreeView controls provide all sorts of features that let customize the ways in which they bind and display. With enough work, you can customize these controls they are hardly recognizable.

Unfortunately, isn't enough to cover all of these advanced techniques in a single book. For more information on specific controls, start looking at Microsoft’s documentation at mdn.microsoft.com/ms752324.aspx.

The following chapter describes another group of controls: layout controls. These are controls such as Grid and StackPanel that help you by arranging the controls that they contain.

# 6

# Layout Controls

Layout controls are primarily intended to contain and arrange other controls. They position the controls they contain in different ways to make it easier to design various kinds of interfaces.

Layout controls are not quite the same as container controls. While all layout controls contain other controls, the converse is not true: Not all controls that contain other controls arrange those controls in a nontrivial way.

For example, the GroupBox control draws a header and a border around a single child. Because its main purpose is to draw the header and border and because it contains only a single child control, it doesn't really do much arranging.

These non-arranging container controls are described elsewhere. For example, the GroupBox is described in the previous chapter.

# CONTROL Overview

The following table briefly lists the controls described in this chapter together with their purposes. You can use this table to decide which control you need in a particular situation.

| CONTROL | PURPOSE |
| --- | --- |
| Canvas | Lets you position controls explicitly by specifying the distances between their left, top, right, and bottom edges and those of the Canvas. |
| DockPanel | Docks its children to its edges. |
| Expander | Displays a header and an icon that the user can click on to show or hide a rows single control. |
| Grid | Displays children in rows and columns. You can also align the rows columns and position children somewhat as you can in a Canvas. |

(continued)

| CONTROL | PURPOSE |
| --- | --- |
| Scroll | Displays a scrollable region. |
| StackPanel | Displays children in a row or column. |
| StatusBar | Creates an area at the bottom of the window. |
| TabControl | Displays tabs that the user can select. |
| ToolBar | Displays a vertical or horizontal area. |
| ToolTray | Handles sizing, dragging. |
| UniformGrid | Displays all have the same size. |
| Viewbox | Stretches its contents. |
| WindowsHost | Contains Windows controls. |
| WrapPanel | Displays children in a row/column. |

# CANVAS

The Canvas lets you explicitly position controls by defining the distances between their left, top, right, and bottom edges.

For example, the following code creates a Canvas containing four buttons that are 20 pixels from the edges. Figure 6-1 shows the result.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_139_0.png)

```
<Canvas>
  <Button Content="TopLeft" Width="85" Height="30"
    Canvas.Top="20" Canvas.Left="20"/>
  <Button Content="TopRight" Width="85" Height="30"
    Canvas.Top="20" Canvas.Right="20"/>
  <Button Content="BottomLeft" Width="85" Height="30"
    Canvas.Bottom="20" Canvas.Left="20"/>
  <Button Content="BottomRight" Width="85" Height="30"
    Canvas.Bottom="20" Canvas.Right="20"/>
</Canvas>
```

UseCanvas

The Canvas always gives its children as much space as they want.

If a child chooses the Left and Right or the Top and Bottom attached properties, the Left or Top values take precedence and the Right or Bottom values are ignored.

# EFFECTS

Because of the attached properties work, the Canvas children stick to its edges and keep their original sizes when the Canvas resizes. If you want the children to stretch when their parent resizes, consider a different container such as a Grid.

# DOCKPAN

The DockPanel docks its children to its edges. This control defines the attached property Dock, which can take the values Left, Right, Top, and Bottom.

During layout, the DockPanel loops through its child controls and checks their Dock values. It attaches each child to the edge of whatever space is currently unclaimed in the DockPanel.

If the DockPanel's LastChildFill property is True, then it makes the last child fill whatever remains.

For example, the following code creates a series of Border controls docked to the DockPanel's

```
<DockPanel LastChildFill="True">
<Border DockPanel.Dock="Top" Background="LightGreen">
<Label Content="1, Top"/>
</Border>
<Border DockPanel.Dock="Left" Background="#FFF00FF">
<Label Content="2, Left">
<RotateTransform Angle="-90"/>
</RotateTransform>
</Label>
</Border>
<Border DockPanel.Dock="Right" Background="#FFFFB400">
<Label Content="3, Right" />
</Border>
</DockPanel>
```
