descendants of Button, Checkbox, and ScrollViewer. You used the Content property of the Button earlier in the HelloWorld sample. But what if you want to place more than one element within the Button?

The trick is that you can place a Panel as the Content of a ContentControl. Panels can have more than one child the Children property. The Grid (which is a default panel when you create a new UserControl in Visual Studio) is an example of such a Panel. So, how do you place text next to the video in the HelloWorld application?

```
<Button HorizontalAlignment="Center" VerticalAlignment="Center">
<Button.Content>
<StackPanel>
<TextBlock Text="I am a button!" HorizontalAlignment="Center" Margin="5" />
<MediaElement Width="100" Height="75" Source="http://msdnchnline.llnw.net/d1/ch9/0/8/7/7/7/4/SL3Expressionlaunch_ch9.vm" />
</StackPanel>
</Button.Content>
</Button>
```

The Content of Button is now a StackPanel. The StackPanel arranges its children — a centered TextBlock, and the MediaElement that plays the video. By default, the StackPanel arranges its children so that they are below each other. So, the Button described with the previous XAML looks like Figure 8-9.

![](bbox=[0.095, 0.51, 0.43, 0.766])

**FIGURE 8-9:** Button with text and video

If you want to change the layout so that the text is to the left of the video, you must change the StackPanel itself, and add an Orientation attribute, as shown here:

```
<Button HorizontalAlignment="Center" VerticalAlignment="Center">
<Button.Content>
<StackPanel Orientation="Horizontal">
<TextBlock Text="I am a button!" HorizontalAlignment="Center" VerticalAlignment="Center" Margin="5" />
```