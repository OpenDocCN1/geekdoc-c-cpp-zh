
In Listing 11.1, you can see that various controls and XAML elements are used in the application. The root XAML element in the **MainPage.xaml** file is a **UserControl** element. It has the **xmlns** attribute to refer to the essential XML namespace. The **UserControl** element, by default, has a **Grid** element in which all the other controls and elements, such as **Ellipse** and **Rectangle**, are defined. Several properties, such as **Background**, **Height**, **Width**, and **Margin**, of these elements are appropriately set.

- 14. Press the **F5** key to run the **MyFirstSilverlightApp** application. The output appears, as shown in Fig.ASP-11.18:

![](img/9862a98a1a2d3bb14334137965a1ec60_712_0.png)

Fig.ASP-11.18

In Figure 11.18, note that when a Silverlight application is compiled, the .aspx page is displayed in the Web browser. This implies that the ASP.NET test page hosts the Silverlight application.

## Hosting Video in a Web site

As discussed, Silverlight can also be used to host audio and video files in a Web site. Silverlight provides the **MediaElement** control to host audio and video files in a Web site. Now, let’s create a Web site, named **PlayVideoApp** (also available on CD), which plays a video file on the Web page. To host the video file in the Web site, perform the following steps:

- 1. *Open* **Microsoft Visual Studio 2010 IDE** and select **File→New→Project**. The **New Project** dialog box appears.
- 2. *Select* **Visual C#→Silverlight** from the **Installed Templates** pane in the **New Project** dialog box.
- 3. *Select* **Silverlight Application** from the middle pane.
- 4. *Specify* the name of the application as **PlayVideoApp** in the **Name** text box and the appropriate location in the **Location** combo box.
  Click the **OK** button.
  The **New Silverlight Application** dialog box appears.
- 5. *Select* the **Host the Silverlight application in a new Web site** check box.
- 6. *Select* the **ASP.NET Web Application Project option** from the **New Web project type** combo box.
- 7. *Select* **Silverlight 4** from the **Silverlight Version** combo box.
- 8. *Select* the **Enable WCF RIA Services** check box.
- 9. Click the **OK** button.
  The **PlayVideoApp** application is created.
- 10. *Right-click* the application name (**PlayVideoApp**) in the **Solution Explorer** window and select **Add→Existing Item** from the context menu, (Fig.ASP-11.19).
    The **Add Existing Item** dialog box appears (Fig.ASP-11.20).
- 12. Browse the desired video file on your computer and click the Add button. In this case, we have added the Wildlife.wmv file, (Fig.ASP.11.20).

![](img/9862a98a1a2d3bb14334137965a1ec60_713_0.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_713_1.png)

The video file is added to your Web site.

- 13. Select the video file (Wildlife.wmv) in the Solution Explorer window and press the F4 key.
    The Properties window appears (Fig.ASP.11.21).
- 14. Select the Copy to Output Directory property in the Properties window (Fig.ASP.11.21).
    The default value of this property is Do not copy.
- 15. Click the down arrow next to the property.
    A drop-down list appears (Fig.ASP.11.21).
- 16. Select the Copy if newer value for the Copy to Output Directory property, (Fig.ASP.11.21).
    The Copy if newer value of the Copy to Output Directory property copies the media file to the current project folder, if the media file is new.
- 17. Set the Build Action property of the Wildlife.wmv file to Resource in the Properties window, (Fig.ASP.11.22).

![](img/9862a98a1a2d3bb14334137965a1ec60_713_2.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_713_3.png)

> By default, the Build Action property is set to None.

- 18. Replace the code of the MainPage.xaml file with the code, shown in Listing 11.2, to design the UI of your Web site:

Listing 11.2: Showing the Code for the MainPage.xaml File of the PlayVideoApp Application

```xml
<UserControl x:Class="PlayVideoApp.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    d:DesignHeight="600" d:DesignWidth="600">
    <Grid x:Name="LayoutRoot" Background="SteelBlue" DataContext="{Binding}">
        <Border BorderBrush="Yellow" BorderThickness="3"/>
        <TextBlock Text="Media Player" HorizontalAlignment="Center" FontWeight="Bold"
            FontSize="24" Margin="0,10,0,0" Foreground="Yellow"/>
        <Button x:Name="play" Height="50" Width="50" Content="Play"
            Margin="0,0,100,425" Background="Yellow" Click="mediaPlay"/>
        <Button x:Name="pause" Height="50" Width="50" Content="Pause"
            Margin="0,0,425,50" Background="Yellow" Click="mediaPause"/>
        <Button x:Name="stop" Height="50" Width="50" Content="Stop"
            Margin="0,0,425,0" Background="Yellow" Click="mediaStop"/>
        <Border Height="425" Width="525" BorderBrush="Yellow" BorderThickness="3"
            Margin="0,100,0,0"/>
        <MediaElement x:Name="mediaEle" Height="400" Width="500" Margin="0,100,0,0"
            Source="Wildlife.wmv" Stretch="UniformToFill" Volume="0.75"
            AutoPlay="False"
            Balance="1" MediaOpened="mediaOpen" MediaFailed="mediaError"/>
        <TextBlock x:Name="errorText" Text="" Height="50" Width="100"
            Foreground="Yellow"/>
        <TextBlock x:Name="mediaText" Height="50" Width="200" Foreground="Yellow"
            Text="Media File:" Margin="0,565,0,0" FontWeight="Bold"/>
        <TextBlock x:Name="duration" Height="50" Width="200" Foreground="Yellow"
            Text="Duration:" Margin="0,0,0,0" FontWeight="Bold"/>
        <TextBlock x:Name="total" Text="Total Time:" Margin="400,565,0,0" FontWeight="Bold"/>
    </Grid>
</UserControl>
```

In Listing 11.2, a **MediaElement** control is added to host a video file (**Wildlife.wmv**). The **Stretch** property of the **MediaElement** control is set to **UniformToFill**, which implies that the video occupies entire control. If the control is smaller than the video, the video is clipped to fit the control. The **Volume** property of the **MediaElement** control is set to 0.75, which implies that the volume, at which the media plays, is 75% of the maximum volume. In addition, the **AutoPlay** property of the **MediaElement** control is set to **False**, which implies that this video does not start automatically after the media file is opened; instead you need to start it manually. In addition, the **Balance** property is set to 1, which means that the right stereo speaker has full volume. There are event handlers associated with the **MediaOpened** and **MediaFailed** events of the **MediaElement** control. Moreover, there are three buttons named **Play**, **Pause**, and **Stop**, which are used to start, pause, and stop the video, respectively. To handle the **MediaOpened** and **MediaFailed** events of the **MediaElement** control and **play**, **pause**, and **stop** the video at runtime, you need to add some code in the code-behind file of the MainPage.xaml file.

- 19. Open the code-behind file (**MainPage.xaml.cs**) of **MainPage.xaml** file and replace the existing code with the code shown in Listing 11.3:

**Listing 11.3:** Showing the Code for the Code-Behind File of the **MainPage.xaml** File

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Net;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Animation;
using System.Windows.Shapes;
namespace PlayVideoApp
{
    public partial class MainPage : UserControl
    {
        public MainPage()
        {
            InitializeComponent();
        }
        public void mediaOpen(object sender, RoutedEventArgs e)
```
