
# 592 Exploring Common XAML Controls

- Display-only controls
- Basic input controls
- List-based controls

All the controls in this section are bindable to data (see Chapter 3 in this minibook) and modifiable through code.

## Display-only controls

Four main controls focus on displaying information to the user:

- Image: The Image control displays images (of type .bmp, .gif, .ico, .jpg, .png, .wdp, .tiff). To preserve the image's aspect ratio, set the Width or Height, but not both. Additionally, the DecodePixelWidth should be set to the same size as the Width. This will cause the rendering engine to scale the image appropriately, saving a significant amount of memory.

Note, by the way, that you can put images almost anywhere in WPF — for example, how about an image on a button, in a label, or inline in a paragraph of text. And it's quite easy. I don't get so fancy here, but I want you know about this possibility.

Listing 2-13 shows the XAML to load an image that shows a color wheel. Only the Width and DecodePixelWidth are set. The resulting window is shown in Figure 2-15.

### Listing 2-13: Image Control

```xml
<Image Grid.Row="0" Grid.Column="0" Width="256" >
  <Image.Source>
    <Bitmap DecodePixelWidth="256" UriSource="/Images/1460_PaintPalette_256x256.png" />
  </Image.Source>
</Image>
```

![](img/6df7bb88e9302e98442acc219cfbd7fc_617_0.png)

Figure 2-15: Image control.

TextBlock and Label: Both the TextBlock and the Label controls are designed to provide text or other content to the user with a few distinctions. The TextBlock control is designed to be the lightweight "little brother" to the label, deriving directly from UIElement.

The Label control provides access modifier and also derives from ContentControl, which opens up additional possibilities. Placing an underscore (_) before a letter enables the access modifiers. To provide an underscore in the Label, use a double underscore. In XAML, because it is essential XAML, the underscore is used because an ampersand would break the XAML. The Target attribute specifies the control to receive focus when the access modifier is key. You may use a Binding expression, which is covered in Chapter 3 of this minibook.

TextBlock and Label controls are illustrated in Listing 2-14 and Figure 2-16.

### Listing 2-14: TextBlock and Label

```xml
<TextBlock Grid.Row="0" Grid.Column="0" Margin="5,0" HorizontalAlignment="Right"
           Text="TextBlock"/>
<Grid Grid.Row="1" Grid.Column="1" Margin="5,0"
      HorizontalAlignment="Stretch">
  <Label Grid.Row="0" Grid.Column="0" Margin="5,0" HorizontalAlignment="Stretch"
         Content="_Label__"
         Target="Binding ElementName=TextBox"/>
  <TextBox Name="SampleTextBox" Grid.Row="1" Grid.Column="1" Margin="5,0"
             HorizontalAlignment="Stretch" />
</Grid>
```

In the sample, the "Label" in the control is the access modifier, and the double underscore adds an underscore character to the rendered output.

### Figure 2-16:

TextBlock and Label controls.

![](img/6df7bb88e9302e98442acc219cfbd7fc_618_0.png)

ProgressBar: The final display-only control is the progress bar. Although technically descendant of the RangeBase class, it does not enable user input by the Slider (see the next section). Figure 2-17 shows a bar in perpetual motion, set the IsInd to True.

```xml
<Grid>
  <Grid.RowDefinitions>
    <RowDefinition Height="Auto"/>
    <RowDefinition Height="Auto"/>
  </Grid.RowDefinitions>
  <ProgressBar Name="ConstantProgressBar" Grid.Row="0" Grid.Column="0"
               IsIndeterminate="True"
               Height="20" Width="200" Foreground="Blue"
               Background="White"/>
  <ProgressBar Grid.Row="1" Grid.Column="0" Maximum="100" Minimum="1"
               Value="50"
               IsIndeterminate="False" Height="20" Width="200"
               Foreground="Blue" Background="White"/>
</Grid>
```

Figure 2-17.
ProgressBar bar at 50 percent.

![](img/6df7bb88e9302e98442acc219cfbd7fc_619_0.png)

## Basic input controls

The workhorses of line of business applications are the basic input controls. You find some of these on every window you create, and they are very straightforward. Figure 2-18 shows all these controls on a single Window. Here are the basic input controls:

- TextBox and Password: The TextBox and Password both allow for the input of standard text into the Window. Password obfuscates the characters typed (using either the default system password character or a developer-specified character) and is used for sensitive information. The TextBox exposes its through the Text property.
- CheckBox: CheckBoxes represent Boolean values. The IsChecked property allows for three state options.
- Radio buttons: Radio buttons allow for a single selection within a group. The choices are determined by the GroupName.
- Slider: The slider is a ranged input. Similar to the ProgressBar, the control takes Minimum, Maximum, and Value.
- DatePicker: New in Visual Studio 2012, the DatePicker control provides a method for getting (or displaying) dates.
- Calendar: Also new in Visual Studio 2012, the Calendar is in full display mode.
- Button: The Button responds to a user's click. The following code shows the Button implemented with an event handler.
