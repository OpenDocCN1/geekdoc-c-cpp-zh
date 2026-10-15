
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

## Data Binding in WPF

WPF includes significant support for binding, whether it is between controls or to a data source. Binding to a source is a very declarative method for associating an external value with a control. Because you specify what is bound, if the bound item changes, then WPF knows to automatically reflect that change in your control. Thus, you aren’t managing state and attempting to track and update changes; that becomes part of the “plumbing” and you can just expect it to work.

In order to manage some of the complexity of data binding, this chapter looks at binding between controls, the use of dependency properties, and then binding to external data sources.

### Binding between WPF Controls

As noted in the updated XAML for the Image1 control, the size of ButtonBrowse has been bound to the size of the control Image1. Control Image1 conveniently is the contents of ButtonBrowse, which creates an interesting dependency when you think about it. However, the size of the image is constrained by the available space within the control’s display area and the scaling of the image being displayed. Thus, if the control is sized at 300×300 and an image is loaded, the control will compute its scale based on the available space. For an image which has a greater height than width, that might be 250×300. Notice how all of this is handled automatically.

In the past your next step would have been to detect that the Image control changed size, communicating this size change to the button to keep it “hidden” behind the image. The code would also need to capture when a new image was loaded, since this would result in resizing the image and another notification to the button. To this also add another notification each time the control was resized, etc. In other words, you would be attempting to ensure that your plumbing captured every change in the Image control’s size.

With WPF, you can simply associate the height of the button with the same value that the Image control is using for its height, and step back. It doesn’t matter how or when the Image control changes size; when the height changes, it changes for both controls. The same is done for the Width property and that’s it; no custom code, no custom event — nothing.

The format used in the ButtonBrowse control is what might be called an inline format for binding:

```
```xml
<Button Height="{Binding ElementName=Image1, Path=Height}"
        Width="{Binding ElementName=Image1, Path=Width}" Name="ButtonBrowse" >
```
```

Notice that the Height and Width properties remain as attributes of the Button’s XML node. This method is convenient when you have only a couple of properties to bind. A second method for binding is discussed later in the chapter.

Binding between controls is, of course, not the only form of binding; nor are you limited to binding to just another named control. In fact, in some cases it’s not realistic to bind to a named control. For example, if you are working with a data grid, you’ll want to bind to the current row, and that implies an associative binding. In that case you want to use a RelativeSource binding so that you can indicate that the row associated with your control in the data grid is the one to which you are binding. That row won’t have a name, just a direct parent relationship. Keep in mind that this example shows only one set of binding parameters; several others are available in order to support the disparate needs of different requirements.

In terms of limitations, you can bind to any object that inherits from DependencyObject. This class is in the class hierarchy for all of the controls in the System.Windows.Controls namespace. It can also be in the class hierarchy of your own custom classes. However, your property also needs to be implemented as a dependency property, the subject of the next section.

### Dependency Properties

Not all properties are dependency properties, but any property used where the design allows for data binding is typically implemented as a dependency property. For the purposes of this chapter, it’s only necessary to understand a few things about dependency properties. First, they are often used to reference resources and styles as dynamic resources, not static resources. Second, they are identified in the documentation of the WPF components. Finally, to help expand your concept of binding, keep in mind that the Style property is in fact a dependency property.

Every control can be associated with one or more styles. As part of your development, you can create a style just as you create a resource. Styles can be assigned similarly to resources — that is, either by referencing them by name when assigning a new style to an instance of a control, or by creating a style that is associated with all instances of a given type. In either case, the Style property of a control is what is known as a dependency property.

When you hear the term dependency you may initially assume this means the property has a dependency on some other item. However, in the context of WPF, a better way to think of the term dependency is that “it depends on who set that specific value in the object that defines that property.” A dependency property isn’t dependent on some external item; the property’s value varies over time depending upon the last update to the property.

Going into the details of why this occurs is beyond the scope of this chapter. However, dependency properties are coupled with change notification logic, and play a significant role in things such as animation and 3-D layout. For our purposes, the goal is to demonstrate the usefulness of dependency properties and how to create a custom dependency property.

To this end, start by assuming that you would like the ImageRotator control to notify its parent container whenever the path for images changes. The traditional way to do this, using a custom event, is illustrated in the code for the ImageRotator control:

```
Public Class ImageRotator

    Private m_imageList As String() = {}
    Private m_curIndex As Integer = 0
    Private m_curImagePath As String = ""
    Private thename As String

    Public Event ImagePathChanged(ByVal sender As Object, ByVal e As String)

    Private Sub Grid1_Loaded(ByVal sender As System.Object,
        ByVal e As System.Windows.RoutedEventArgs) Handles
    Grid1.Loaded
        m_curImagePath = Environment.GetFolderPath(Environment.SpecialFolder.MyPictures)
        RaiseEvent ImagePathChanged(Me, m_curImagePath)
        LoadImages()
    End Sub

    Private Sub ButtonBrowse_Click(ByVal sender As System.Object,
        ByVal e As System.Windows.RoutedEventArgs) Handles
    ButtonBrowse.Click
        Dim folderDialog As System.Windows.Forms.FolderBrowserDialog =
            New System.Windows.Forms.FolderBrowserDialog()
        folderDialog.Description = "Select the folder for images."
        folderDialog.SelectedPath = m_curImagePath
        Dim res As System.Windows.Forms.DialogResult = folderDialog.ShowDialog()
        If res = System.Windows.Forms.DialogResult.OK Then
            m_curImagePath = folderDialog.SelectedPath
            RaiseEvent ImagePathChanged(Me, m_curImagePath)
            LoadImages()
        End If
    End Sub

    Private Sub LoadImages()
        Image1.Source = Nothing
```
