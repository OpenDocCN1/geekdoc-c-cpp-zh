# CHAPTER 4 COMMON PROPERTIES

The Width and Height properties are self-explanatory. They determine the control's size directly.
Often, you don't really want to set a control size explicitly. Instead, it would be better for the control to resize itself in some space to fit its contents or the area that contains. It lets the control use as much space as possible or take best advantage of the space available.

That's where the HorizontalAlignment and VerticalAlignment properties come into play. HorizontalAlignment can take the values Left, Right, Center, and Stretch. VerticalAlignment can take the values Left, Top, Bottom, Center, and Stretch.

The Left, Right, Top, and Center values determine the control's position in a fairly obvious way. For example, if a control has properties set to Left/Top, then it is placed in the upper-left corner of its container.

The Stretch value is a bit less intuitive. In general, this value means that the control should expand to fill its contents, but the exact result depends on the type of control's container.
For example, if the container is a Grid, the control stretches to fill its Grid as expected. In contrast, if the container is a StackPanel oriented vertically, then setting HorizontalAlignment = Stretch makes the expand to fill the width of the StackPanel, but if you do explicitly set the Height property, then the control will be as short as still displaying its contents.

The SizeInContainers example show in Figure 4-1 displays controls inside various types of containers. The Labels tell what kind of containers they are, and the containers have yellow backgrounds where you can see them. The Buttons in each container are the same, and all have HorizontalAlignment and VerticalAlignment set to Stretch.

![](bbox=[0.095, 0.548, 0.57, 0.783])

FIGURE 4-1

The following XAML code shows how the program creates its Grid container together with its Label and Buttons. Notice that the Grid's size is explicitly set with its Width and Height properties. The code for the other containers is similar except they use other controls in place of the Grid.

```
<StackPanel Margin="10">
  <Label Content="Grid" HorizontalAlignment="Center"/>
  <Grid Background="Yellow" Width="175" Height="100">
    <Button Content="Button1"/>
```