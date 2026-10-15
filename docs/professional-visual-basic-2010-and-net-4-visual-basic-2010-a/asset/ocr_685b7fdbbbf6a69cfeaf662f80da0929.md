```
TrafficLight1.Status = TrafficLightStatus.statusYellow
End Sub
Private Sub btnGreen_Click(ByVal sender As System.Object,
    ByVal e As System.EventArgs) Handles btnGreen.Click
    TrafficLight1.Status = TrafficLightStatus.statusGreen
End Sub
```

In the Solution Explorer, right-click your test Windows Application project and select Set as Startup Project. Then press F5 to run. When your test form appears, you can change the "signal" on the traffic light by pressing the buttons. Figure 15-8 shows a sample screen.

Of course, you can’t see the color in a black-and-white screenshot; but as you can tell from its position, the circle is red. The "yellow light" displays in the middle of the control, and the "green light" displays at the bottom. These positions are all calculated in the Paint event logic, depending on the value of the Status property.

For a complete example, it would be desirable for the control to allow the user to change the Status by clicking on a different part of the "traffic light." That means including logic to examine mouse clicks, calculate whether they are in a given area, and change the Status property if appropriate. In the code available for download for this book, the TrafficLight example includes such functionality.

# ATTACHING AN ICON FOR THE TOOLBOX

By default, the icon that appears in the Toolbox next to your control's name is a gear-shaped icon. However, you can attach an icon to a control for the Toolbox to display. There are two ways to do that.

Windows Forms includes a ToolboxBitmap attribute that can specify an icon for a class. It can be used in several ways, and you can see examples in the help file for the ToolboxBitmap attribute.

The easy way to attach an icon to your control is to let Visual Studio do it for you. Simply locate or draw the icon you want to use and add it to the project containing your control. Then rename the icon so that it has the same name as your control but an extension of .ico instead of .vb.

For example, to attach an icon to the TrafficLight control in the preceding example, find an icon you like, place it in your project, and name it TrafficLight.ico. Then Visual Studio will attach the icon to your control during the compilation process; and when your control is added to the Toolbox, your icon will be used instead of the gear-shaped one.

> Custom icons are displayed for a control in the Toolbox only when the control is added with the Toolbox's Choose Items option. Controls that appear in the Toolbox at the top because their project is currently loaded do not exhibit custom icons. They always have a blue, gear-shaped icon.

# EMBEDDING CONTROLS IN OTHER CONTROLS

Another valuable technique for creating custom controls is to embed other controls. In a sense, the UserControl does this; but when a UserControl is used as the base class, by default it only exposes the properties of the UserControl class. Instead, you may want to use a control such as TextBox or Grid as the starting point, but embed a Button in the TextBox or Grid to obtain some new functionality.

The embedding technique relies on the fact that in Windows Forms, all controls can be containers for other controls. Visual Basic developers are familiar with the idea that Panels and GroupBoxes can be containers, but in fact a TextBox or a Grid can also be a container of other controls.

Code snippet from TrafficLight

![](bbox=[0.75, 0.2, 0.92, 0.3])

FIGURE 15-8