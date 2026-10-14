
window, expand the Common property category if it is not already expanded. Then, click the ellipsis button that appears alongside the Items property.
The Object Collection Editor window opens.
9. In the list toward the lower left of the window, select ComboBoxItem, and then click Add. In the right pane displaying the properties for the item, expand the Common section if it is not already expanded, and then type Mr in the Content property.

![](img/16f6e3fe08f01ddadb2741a92c392b0e_718_0.png)

10. Click OK.

The Object Collection Editor closes. If you examine the XAML markup for the title ComboBox, it should now look like this:

Click here to view code image

```
<ComboBox x:Name="title" HorizontalAlignment="Left"
Margin="420,240,0,0"
    VerticalAlignment="Top" Width="100" FontSize="20"/>
    <ComboBoxItem Content="Mr"/>
</ComboBox>
```

There are two things to notice here. The first is that the ComboBox markup has been split into an opening <ComboBox> tag and a closing </ComboBox> tag. The second is that between these tags, Visual Studio has added a ComboBoxItem element with the Content property set to Mr. This
item will be displayed in a drop-down list when the app runs.

11. Add the values *Mrs*, *Ms*, and *Miss* to the *title* ComboBox. You can use the Object Collection Editor or type the XAML markup by hand. The resulting markup should look like this:

Click here to view code image

```
<ComboBox x:Name="title" HorizontalAlignment="Left"
    Margin="420,240,0,0"
    VerticalAlignment="Top" Width="75" FontSize="20">
    <ComboBoxItem Content="Mr"/>
    <ComboBoxItem Content="Mrs"/>
    <ComboBoxItem Content="Ms"/>
    <ComboBoxItem Content="Miss"/>
</ComboBox>
```

## Note

A *ComboBox* control can display simple elements such as a set of *ComboBoxItem* controls that display text, but it can also contain more complex elements such as buttons, check boxes, and radio buttons. If you are adding simple *ComboBoxItem* controls, it is probably easier to type the XAML markup by hand, but if you are adding more complex controls, the Object Collection Editor can prove very useful. However, you should avoid trying to be too clever in a combo box; the best apps are those that provide the most intuitive UIs, and embedding complex controls in a combo box can be confusing to a user.

12. Add two more *TextBox* controls and two more *TextBlock* controls to the form. With the *TextBox* controls, the user will be able to enter an email address and telephone number for the customer, and the *TextBlock* controls provide the labels for the text boxes. Use the values in the following table to set the properties of the controls.

| Control | Property | Value |
|---|---|---|
| First TextBlock | HorizontalAlignment | Left |
|  | Margin | 300,390,0,0 |
|  | TextWrapping | Wrap |
|  | Text | Email |
|  | VerticalAlignment | Top |
|  | FontSize | 20 |
| First TextBox | x:Name | email |
|  | HorizontalAlignment | Left |
|  | Margin | 450,390,0,0 |
|  | TextWrapping | Wrap |
|  | Text | Leave Empty |
|  | VerticalAlignment | Top |
|  | Width | 400 |
|  | FontSize | 20 |
| Second TextBlock | HorizontalAlignment | Left |
|  | Margin | 300,540,0,0 |
|  | TextWrapping | Wrap |
|  | Text | Phone |
|  | VerticalAlignment | Top |
|  | FontSize | 20 |
| Second TextBox | x:Name | phone |
|  | HorizontalAlignment | Left |
|  | Margin | 450,540,0,0 |
|  | TextWrapping | Wrap |
|  | Text | Leave Empty |
|  | VerticalAlignment | Top |
|  | Width | 200 |
|  | FontSize | 20 |

The XAML markup for these controls should look like this:

Click here to view code image

```
<TextBlock HorizontalAlignment="Left" Margin="300,390,0,0"
TextWrapping="Wrap"
Text="Email" VerticalAlignment="Top" FontSize="20"/>
<TextBox x:Name="email" HorizontalAlignment="Left"
Margin="450,390,0,0"
TextWrapping="Wrap" Text="" VerticalAlignment="Top" Width="400"
FontSize="20"/>
<TextBlock HorizontalAlignment="Left" Margin="300,540,0,0"
TextWrapping="Wrap"
Text="Phone" VerticalAlignment="Top" FontSize="20"/>
<TextBox x:Name="phone" HorizontalAlignment="Left"
Margin="450,540,0,0"
TextWrapping="Wrap" Text="" VerticalAlignment="Top" Width="200"
FontSize="20"/>
```

The completed form in the Design View window should look like this:

![](img/16f6e3fe08f01ddadb2741a92c392b0e_721_0.png)

13. On the Debug menu, click Start Debugging to build and run the app.
The app starts and displays the form. You can enter data into the form and select a title from the combo box, but you cannot do much else yet.
However, a much bigger problem is that the form looks awful. The right side of the display has been cut off, much of the text has wrapped around, and the Last Name text box has been truncated:

## Adventure Works Customers

ID

First Name

Last Nam

Email

Phone

14. Click and drag the right side of the window to expand the display so that the text and controls are displayed as they appeared in the Design View window in Visual Studio. This is the optimal size of the form as it was designed.

15. Resize the window displaying the Customer app to its minimum width. This time, much of the form disappears. Some of the TextBlock content wraps, but the form is clearly not usable in this view.

16. Return to Visual Studio, and on the Debug menu, click Stop Debugging.

That was a salutary lesson in being careful about how you lay out an app. Although the app looked fine when it ran in a window that was the same size as the Design View, as soon as you resized the window to a narrower view, it became less useful (or even completely useless). Additionally, the app assumes that the user will be viewing the screen on a device in the landscape orientation. If you temporarily switch the Design View window to the 12” Tablet form factor and click the Portrait orientation button, you can see what the form would look like if the user ran the app on a tablet that supports different orientations and rotated the device to switch to portrait mode. (Don’t forget to switch back to the 13.3” Desktop form factor afterward.)

The issue is that the layout technique shown so far does not scale and adapt to different form factors and orientations. Fortunately, you can use the properties of the Grid control and another feature called the Visual State Manager to solve these problems.

## Using the Simulator to test a Universal Windows Platform app

Even if you don’t have a tablet computer, you can still test your UWP apps and see how they behave on a mobile device by using the Simulator provided with Visual Studio 2015. The Simulator mimics a tablet device, providing you with the ability to emulate user gestures such as pinching and swiping objects, as well as rotating and changing the resolution of the device.

To run an app in the Simulator, open the Debug Target drop-down list box on the Visual Studio toolbar. By default, the debug target is set to Local Machine, which causes the app to run full-screen on your computer,
but you can select Simulator from this list, which starts the Simulator when you debug the app. Note that you can also set the debug target to a different computer if you need to perform remote debugging (you will be prompted for the network address of the remote computer when you select this option). The following image shows the Debug Target list:

![](img/16f6e3fe08f01ddadb2741a92c392b0e_724_0.png)

After you have selected the Simulator, when you run the app from the Debug menu in Visual Studio, the Simulator starts and displays your app. The toolbar down the right side of the Simulator window contains a selection of tools with which you can emulate user gestures by using the mouse. You can even simulate the location of the user if the app requires information about the geographic position of the device. However, for testing the layout of an app, the most important tools are Rotate Clockwise, Rotate Counterclockwise, and Change Resolution. The following image shows the Customers app running in the Simulator. The app has been maximized to occupy the full screen. The labels describe the function of each of the buttons for the Simulator.
