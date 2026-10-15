
The updated property code follows, starting with the updated ImageURI property:

```
Public Property ImageURI As String
    Get
        Return m_curImagePath
    End Get
    Set(ByVal value As String)
        m_curImagePath = value
        LoadImages()
    End Set
End Property

Private Shared ImageProp As DependencyProperty =
    DependencyProperty.RegisterAttached("ImageURI",
        GetType(String),
        GetType(ProVB_WPF_Step3.ImageRotator),
        New FrameworkPropertyMetadata(Nothing,
            FrameworkPropertyMetadataOptions.AffectsRender,
            New PropertyChangedCallback(AddressOf UriChanged)))

Public Shared Sub UriChanged(ByVal prop As DependencyObject,
    ByVal args As DependencyPropertyChangedEventArgs)
    CType(prop, ImageRotator).ImageURI = args.NewValue
End Sub
```

Code snippet from ImageRotator.vb

The original call to reference a DependencyPropertyKey has also been updated and the code now references a true DependencyProperty update. However, your focus should be on the fourth parameter to the RegisterAttached method. While the first three parameters are unchanged, the fourth parameter is now passing two new properties.

The new constructor for the FrameworkPropertyMetadata has a null parameter for the “default” value. It then passes an option flag indicating that when this property is updated, the rendering of the window is affected and will need to be updated. This is true because an update to this property will result in the selection of a new image, which will need to be sized and displayed.

However, it is the final parameter, the new PropertyChangedCallback, that is important. This is registering with the property what method should be notified when a change is made for this property. As noted earlier, when you think of a dependency property as a property plus an event with two-way communication, you need a place that will accept the inbound communications. This callback method is essentially an event handler for the PropertyChanged event when it is fired outside of the local class.

In this case, the address of the UriChanged method is passed. That method is the remaining new code. As you’ll note by looking at the code, the UriChanged method is a Shared method, which means it can’t just reference the local property. Fortunately, the first parameter is the instance of the DependencyObject which needs to be updated, and one of the values passed within the EventArgs parameter is in fact the new value. As a result, the method only requires a single line which casts the inbound dependency object to the local type and then calls the appropriate property on the local class, passing the new value.

This creates an infrastructure that supports two-way communication whereby your object will notify those who are interested in the value of this property about changes to it, and those who need to update this property can notify your object of a new proposed value. Note that if, for example, someone passed a path which wasn’t valid, then you could reject the assignment of that value. If you are looking at the download code, then you know there is one last set of changes to comment out, some of the lines in the Load event of this class; however, that change is covered as the last step in this process.

The code now supports a bi-directional property associated with the image path, allowing updates to be sent to the control via binding within the XAML of the main window. Note that there are no updates to the ImageRotator.xaml file or the MainWindow.xaml.vb file. The data binding is focused on the

MainWindow.xaml file, which has again grown in length, and accordingly complexity. To help manage this, the next code block addresses the changes to this file which occur in the resources and data context for the file, while the updates to individual control binding are the focus of the second block.

The XAML which follows shows a couple of minor modifications to the window, but it is the bold lines which are of interest for the purposes of data binding. Because these lines are located near the top, we’ll discuss them before the code. The first is a new DataContext assigned to the top-level grid. This grid, which isn’t given a name but which is parent to all of the other controls, acts as the central clearing for the binding contexts.

The first highlighted line, which creates a data context for the grid, actually binds it to the new ListBox control. The selected item in the ListBox is then bound to the grid. By referencing this context across all of the other controls in the window, these controls can use this data context as their current context. Because updates to the selected item in the list are automatically updated to this context, each control can thus be kept in sync with the selected item in the grid, with no further code.

What may then interest you is the next highlighted section, which contains the grid resources. Most of the time developers would traditionally take these resources and map them to the selected item in the ListBox. However, as just discussed with WPF, the grid is binding to the selected item in the ListBox; thus, all of the other controls can inherit that context for the data context.

The implication is that the one control that won’t inherit is the ListBox. Instead, as you’ll see later, the ListBox explicitly binds to the first of the grid resources, the XmlDataProvider. This class is available to provide a way for XAML to load an XML file and bind to its contents. Either the provider can use a Source property, or you could embed the data within an x:Data block. Once bound, the provider is assigned a key so that it can be referenced from other controls. In this example, only the ListBox control will actually bind to this data source, but in theory other controls could bind to it. Additionally, the top-level node for XPath queries is defined as People. When the code asks for a property, it will get one based on entries under People. This is the starting point for the very simple XPath that the application will use.

The creation of the data provider is short and sweet; what comes next, however, is a data template. Called the PersonName template, this template defines an output format. It is also used by the ListBox control, although it could be used, for example, to populate the window title if you wanted a different title on the window. Within is a short snippet of WPF that describes a container — in this case, a StackPanel and the controls which are on the StackPanel. This means that a DataTemplate can be an extremely powerful way to format complex data structures. The controls within map directly to the default data source, in this case referencing two of the nodes from the Person structure in the XML.

These represent the only highlighted areas for binding in the first section of XML. The block which follows includes the top-level window showing a partially transparent background, through the buttons that are on the title bar rectangle:

```
<Window x:Class="MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="ProVB_WPF" Height="363" Width="444" Name="MainWindow"
    WindowStyle="None" AllowsTransparency="True" xmlns:my="clr-namespace:ProVB_WPF_Step3"
    WindowStartupLocation="CenterScreen" Background="#B4FFFFFF">
    <Grid OpacityMask="Black" Opacity="1"
        DataContext="{Binding ElementName=ListBox1, Path=SelectedItem}">
        <Grid.RowDefinitions>
            <RowDefinition Height="25*" />
            <RowDefinition Height="215*" />
        </Grid.RowDefinitions>
        <Grid.Resources>
            <XmlDataProvider Source="People.xml" x:Key="People"
                XPath="People">
            </XmlDataProvider>
            <DataTemplate x:Key="PersonName">
```

```
<StackPanel Orientation="Horizontal">
    <TextBlock>
        <TextBlock.Text>
            <Binding XPath="FirstName"/></Binding>
        </TextBlock.Text>
    </TextBlock>
    <TextBlock Text=" "/></TextBlock>
    <TextBlock>
        <TextBlock.Text>
            <Binding XPath="LastName"/></Binding>
        </TextBlock.Text>
    </TextBlock>
</StackPanel>
</DataTemplate>
</Grid.Resources>
<Rectangle Name="TitleBar" HorizontalAlignment="Stretch" Margin="0,0,0,0" Stroke="#00000000" VerticalAlignment="Stretch" Opacity="0.5">
    <Rectangle.Fill>
        <LinearGradientBrush EndPoint="1,0.5" StartPoint="0,0.5">
            <GradientStop Color="#FF0AFF0A" Offset="0" />
            <GradientStop Color="Blue" Offset="1" />
            <GradientStop Color="#0059C4B" Offset="0.474" />
            <GradientStop Color="#00638F54" Offset="0.785" />
            <GradientStop Color="#9D0000FF" Offset="0.826" />
            <GradientStop Color="#FF00ED00" Offset="0.359" />
        </LinearGradientBrush>
    </Rectangle.Fill>
</Rectangle>
<Label Grid.Row="0" Height="28" HorizontalAlignment="Left" Margin="10,0,0,0" Name="labelWindowTitle" VerticalAlignment="Top">
    <Label.Content>
        <Binding ElementName="imageRotator1" Path="ImageURI"/></Binding>
    </Label.Content>
</Label>
<Button Height="20" Width="23" HorizontalAlignment="Right" Margin="0,1,1,0" Name="ButtonClose" VerticalAlignment="Top" >
    <Image Margin="0,0,0,0" Name="Image2" Stretch="Fill" Source="/ProVB_WPF_Step3;component/Resources/1385_Disable_24x24_72.png"/>
</Button>
<Button Height="20" Width="20" HorizontalAlignment="Right" Margin="0,1,25,0" Name="ButtonMax" VerticalAlignment="Top" >
    <Image Margin="0,0,0,0" HorizontalAlignment="Center" Name="Image3" Stretch="Fill" Source="/ProVB_WPF_Step3;component/Resources/112_Plus_Green_24x24_72.png"/>
</Button>
<Button Height="20" Width="20" HorizontalAlignment="Right" Margin="0,1,47,0" Name="ButtonMin" VerticalAlignment="Top" >
    <Image Margin="0,0,0,0" Name="Image4" Stretch="Fill" Source="/ProVB_WPF_Step3;component/Resources/112_DownArrowShort_Green_24x24_72.png"/>
</Button>
```

Code snippet from MainWindows.xaml

Note that a couple of minor changes to the preceding XAML aren’t covered here — for example, the gradient information for the LinearGradientBrush. In addition, note something that has not been changed. The first step in the binding process was to have the labelWindowTitle control bind to the ImageURI property of the ImageRotator. With the changes you are about to make, it would make sense to have this property bind locally instead of to the control. This is not changed in the sample in order to reduce the complexity of the changes to the code, but it’s something you can do on your own.

The focus is on the highlighted sections and the changes to support data binding. You can see that the changes to support data binding in the XAML are relatively minor. The second half of the MainWindow.xaml file starts
