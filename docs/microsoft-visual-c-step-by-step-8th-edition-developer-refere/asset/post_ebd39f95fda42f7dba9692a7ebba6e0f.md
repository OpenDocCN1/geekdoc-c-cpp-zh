
the Segoe Print font is bigger than the default font.

13. Switch back to the MainPage.xaml file and find the XAML markup for the TextBlock control for the Adventure Works Customers label in the customersTabularView Grid control:

Click here to view code image

```
<TextBlock Grid.Row="0" HorizontalAlignment="Center"
TextWrapping="Wrap"
Text="Adventure Works Customers" VerticalAlignment="Center"
FontSize="50"/>
```

14. Change the properties of this control to reference the TabularHeaderStyle style, as shown in bold in the following code:

Click here to view code image

```
<TextBlock Grid.Row="0" Style="{StaticResource TabularHeaderStyle}"
Text="Adventure Works Customers"/>
```

The heading displayed in the Design View window should change color, size, and font and look like this:

![](img/16f6e3fe08f01ddadb2741a92c392b0e_753_0.png)

15. Find the XAML markup for the TextBlock control for the Customers label in the customers-ColumnarView Grid control:

Click here to view code image

```
<TextBlock Grid.Row="0" HorizontalAlignment="Center"
TextWrapping="Wrap"
Text="Customers" VerticalAlignment="Center" FontSize="30"/>
```

Modify the markup of this control to reference the ColumnarHeaderStyle style, as shown here in bold:

Click here to view code image

```
<TextBlock Grid.Row="0" Style="{StaticResource ColumnarHeaderStyle}"
Text="Customers"/>
```

Be aware that you won’t see this change in the Design View window because the customers-ColumnarView Grid control is collapsed by default. However, you will see the effects of this change when you run the app later in this exercise.

16. Return to the AppStyles.xaml file in the Code and Text Editor window. Modify the HeaderStyle style with the additional property Setter elements shown in bold in the following example:

Click here to view code image

```
<Style x:Key="HeaderStyle" TargetType="TextBlock" BasedOn="{StaticResource FontStyle}">
    <Setter Property="HorizontalAlignment" Value="Center"/>
    <Setter Property="TextWrapping" Value="Wrap"/>
    <Setter Property="VerticalAlignment" Value="Center"/>
    <Setter Property="Foreground" Value="SteelBlue"/>
    <Setter Property="RenderTransformOrigin" Value="0.5,0.5"/>
    <Setter Property="RenderTransform">
        <Setter.Value>
            <CompositeTransform Rotation="-5"/>
        </Setter.Value>
    </Setter>
</Style>
```

These elements rotate the text displayed in the header about its midpoint by an angle of 5 degrees by using a transformation.

### Note

This example shows a simple transformation. Using the RenderTransform property, you can perform a variety of other transformations to an item, and you can combine multiple transformations. For example, you can translate (move) an item on the x- and y-axes, skew the item (make it lean), and scale an element.

You should also notice that the value of the RenderTransform property is itself another property/value pair (the property is Rotation, and the value is −5). In cases such as this, you specify the value by using the <Setter.Value> tag.

17. Switch to the MainPage.xaml file. In the Design View window, the title should now be displayed at a jaunty angle:

![](img/16f6e3fe08f01ddadb2741a92c392b0e_754_0.png)

18. In the AppStyles.xaml file, add the following style:

Click here to view code image

```
<Style x:Key="LabelStyle" TargetType="TextBlock" BasedOn="{StaticResource FontStyle}">
    <Setter Property="FontSize" Value="30"/>
    <Setter Property="HorizontalAlignment" Value="Center"/>
    <Setter Property="TextWrapping" Value="Wrap"/>
    <Setter Property="VerticalAlignment" Value="Center"/>
    <Setter Property="Foreground" Value="AntiqueWhite"/>
</Style>
```

You will apply this style to the TextBlock elements that provide the labels for the various TextBox and ComboBox controls that the user employs to enter customer information. The style references the same font style as the headings but sets the other properties to values more appropriate for the labels.

19. Go back to the MainPage.xaml file. In the XAML pane, modify the markup for the TextBlock controls for each of the labels in the customersTabularView and customersColumnarView Grid controls. Remove the HorizontalAlignment, TextWrapping, VerticalAlignment, and FontSize properties, and reference the LabelStyle style, as shown here in bold:

Click here to view code image

```
<Grid x:Name="customersTabularView" Margin="10,20,10,20" Visibility="Visible">
    ...
    <Grid Grid.Row="2">
        ...
        <TextBlock Grid.Row="0" Grid.Column="1" Style="{StaticResource LabelStyle}" Text="ID"/>
        <TextBlock Grid.Row="0" Grid.Column="3" Style="{StaticResource LabelStyle}" Text="Title"/>
        <TextBlock Grid.Row="0" Grid.Column="5" Style="{StaticResource LabelStyle}" Text="First Name"/>
        <TextBlock Grid.Row="0" Grid.Column="7" Style="{StaticResource LabelStyle}" Text="Last Name"/>
        ...
        <TextBlock Grid.Row="3" Grid.Column="1" Style="{StaticResource LabelStyle}" Text="Email"/>
        ...
        <TextBlock Grid.Row="5" Grid.Column="1" Style="{StaticResource LabelStyle}" Text="Phone"/>
        ...
    </Grid>
</Grid>
<Grid x:Name="customersColumnarView" Margin="10,20,10,20" Visibility="Collapsed">
```

```
...
<Grid Grid.Row="1">
...
<TextBlock Grid.Row="0" Grid.Column="0" Style="{StaticResource LabelStyle}"
Text="ID"/>
<TextBlock Grid.Row="1" Grid.Column="0" Style="{StaticResource LabelStyle}"
Text="Title"/>
<TextBlock Grid.Row="2" Grid.Column="0" Style="{StaticResource LabelStyle}"
Text="First Name"/>
<TextBlock Grid.Row="3" Grid.Column="0" Style="{StaticResource LabelStyle}"
Text="Last Name"/>
...
<TextBlock Grid.Row="4" Grid.Column="0" Style="{StaticResource LabelStyle}"
Text="Email"/>
...
<TextBlock Grid.Row="5" Grid.Column="0" Style="{StaticResource LabelStyle}"
Text="Phone"/>
...
</Grid>
</Grid>
```

The labels on the form should change to the Segoe Print font and be displayed in white, in a font size of 30 points:

![](img/16f6e3fe08f01ddadb2741a92c392b0e_756_0.png)

20. On the Debug menu, click Start Debugging to build and run the app.

### Note

Use the Simulator if you are running on a display with a resolution less than 1366 × 768.

The Customers form should appear and be styled in the same way that it appears in the Design View window in Visual Studio. Notice that if you enter any text into the various fields on the form, they use the default font and styling for the TextBox controls.

### Note

Although the Segoe Print font is good for labels and titles, it is not recommended as a font for data-entry fields because some of the characters can be difficult to distinguish from one another. For example, the lowercase letter l is very similar to the digit 1, and the uppercase letter O is almost indistinguishable from the digit 0. For this reason, it makes sense to stick with the default font for the TextBox controls.

21. Resize the window to make it narrower and verify that the styling has been applied to the controls in the customersColumnarView grid. The form should look like this:

# Customers

ID

Title

First Name

Last Name

Email

Phone

22. Return to Visual Studio and stop debugging.

For completeness, the following image shows the Customers app running on the Windows Phone 10 Emulator:

# Customers

ID

Title

First Name

Last Name

Email

Phone

You can see that by using styles, you can easily implement a number of really cool effects. In addition, careful use of styles makes your code much more maintainable than it would be if you set properties on individual controls. For example, if you want to switch the font used by the labels and headings in the Customers app, you need to make only a single change to the *FontStyle* style. In general, you should use styles wherever possible; besides assisting maintainability, the use of styles helps to keep the XAML markup for your forms clean and uncluttered, and the XAML for a form needs to specify only the controls and layout rather than how the controls should appear on the form. You can also use Microsoft Blend for Visual Studio 2015 to define complex styles that you can integrate into an app. Professional graphics artists can use Blend to develop custom styles and provide these styles in the form of XAML markup to developers building apps. All the developer has to do is add the appropriate *Style* tags to the user interface elements to reference the corresponding styles.

## Summary

In this chapter, you learned how to use the *Grid* control to implement a user interface that can scale to different device form factors and orientations. You also learned how to use the Visual State Manager to adapt the layout of controls when the user changes the size of the window displaying the app. Finally, you learned how to create custom styles and apply them to the controls on a form. Now that you have defined the user interface, the next challenge is to add functionality to the app, enabling the user to display and update data, which is what you will do in the final chapters.

- If you want to continue to the next chapter, keep Visual Studio 2015 running and turn to Chapter 26.
- If you want to exit Visual Studio 2015 now, on the File menu, click Exit. If you see a Save dialog box, click Yes and save the project.

## Quick reference
