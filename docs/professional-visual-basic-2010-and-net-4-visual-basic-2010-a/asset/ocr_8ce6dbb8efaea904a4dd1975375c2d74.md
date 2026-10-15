```
HorizontalAlignment="Right" Width="75"
Clip="{StaticResource RoundPanel}">
    <Button HorizontalAlignment="Stretch"
VerticalAlignment="Stretch" Name="ButtonNext"
Height="75" Width="75" Visibility="Hidden">
        <Image Margin="0,0,0,0" Stretch="Fill"
Source="/Resources/RightArrow.jpg"/></Image>
    </Button>
    </StackPanel>
    <StackPanel Background="Transparent" VerticalAlignment="Center"
Margin="25,0,0,0" Height="75" Name="StackPanelPrev"
HorizontalAlignment="Left" Width="75"
Clip="{StaticResource RoundPanel}">
    <Button HorizontalAlignment="Left"
VerticalAlignment="Center" Name="ButtonPrev"
Height="75" Width="75" Visibility="Hidden">
        <Image Margin="0,0,0,0" Stretch="Fill"
Source="/Resources/LeftArrow.jpg"/></Image>
    </Button>
    </StackPanel>
</Grid>
</UserControl>
```

Code snippet from ImageRotator.xaml

The preceding XAML should look familiar. The main differences from the last time we looked at this code as part of the MainWindow class are the changes related to the user control declaration and to ButtonBrowse.

In terms of the UserControl, it has several attributes that should be very familiar in terms of class and namespace definitions. One which may not be familiar is the one labeled mc and associated with markup compatibility. This library is also used within the attributes of the user control declaration. mc:Ignorable="d" indicates that attribute values which are namespaced within the "d" namespace can be ignored when processing this XAML.

DesignHeight and DesignWidth are the two attributes prefaced with d:. In this context it should be relatively clear what is occurring; We are introducing the idea that when designing this user control, it is useful to have a visible design surface. However, at deployment, this user control should be sized to the needs of the containing object. Since the design surface has no containing object, this could cause an issue because the height and width would default to 0. The only way to prevent that would be to introduce an element to force a size on the user control, and of course that would carry forward into the deployment and affect use of the control.

What mc:Ignorable provides is a way within XAML to describe aspects of the UI that are specific to design time. That way, at runtime it isn’t necessary to remember to remove these attributes; instead they are ignored.

In addition to the elements used to define the new user control class, the other change of interest involves ButtonBrowse. As noted, ButtonBrowse is now included in the same display area as the image. You’ll note that the button’s height and width are now data bound, as explained in more detail shortly.

Before discussing data binding and leaving the majority of this XAML behind, notice how the image has been placed as the content of the button. Placing the image into the button’s content allows the code to leverage the built-in command routing of WPF. When someone clicks on the image, the image doesn’t handle the click event. It is therefore passed to the UI element layered below the image, the button. The button, of course, handles the click event. Thus, unlike the days of Windows Forms, when you would attach the image to the button which had some knowledge about using an image as its surface, in WPF the button is blissfully unaware that an image is acting as its content. However, this decoupling of the image from the button leaves a gap in relation to the sizing of the button, and that’s where data binding the button’s height and width to those of the image comes in.