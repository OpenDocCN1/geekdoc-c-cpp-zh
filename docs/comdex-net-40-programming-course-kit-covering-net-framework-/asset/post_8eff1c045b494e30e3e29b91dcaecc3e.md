
```csharp
mediaFile.Text += mediaFile.Source.ToString();
duration.Text += mediaFile.NaturalDuration.TimeSpan.Hours.ToString() +
    ":" + mediaFile.NaturalDuration.TimeSpan.Minutes.ToString() + ":" +
    mediaFile.NaturalDuration.TimeSpan.Seconds.ToString();
}
}
public void mediaError(object sender, RoutedEventArgs e)
{
    errorText.Text = "Failed to open the media";
}
public void mediaPlay(object sender, RoutedEventArgs e)
{
    mediaEle.Play();
    play.Content = "Play";
}
public void mediaPause(object sender, RoutedEventArgs e)
{
    mediaEle.Pause();
    play.Content = "Resume";
}
public void mediaStop(object sender, RoutedEventArgs e)
{
    mediaEle.Stop();
    play.Content = "Play";
}
}
```

In Listing 11.3, we have created the **mediaOpen()**, **mediaPlay()**, **mediaPause()**, and **mediaError()** methods. The **mediaOpen()** method executes when the media in the MediaElement control is opened. This method displays the name and the length (total time) of the media file in the application by using the **Source** and **NaturalDuration** properties of the **MediaElement** control. The **mediaPlay()** method executes when the **Play** button is clicked. This method calls the **Play()** method of the **MediaElement** control. Similarly, when you click the **Pause** and **Stop** buttons in the application, the **Pause()** and **Stop()** methods of the **MediaElement** control are called in the **mediaPause()** and **mediaStop()** methods, respectively. In case there are any errors while opening or playing the media, the **mediaError()** method executes.

20. Press the F5 key to run the Web site. The output appears, as shown in Fig.ASP-11.23:

![](img/9862a98a1a2d3bb14334137965a1ec60_715_0.png)

Fig.ASP-11.23

You can click the **Play**, **Pause**, and **Stop** buttons on the Web site to play, pause, and stop the video, respectively.

## Creating Applications Using Different Controls

Silverlight provides numerous controls that you can use to define appearance of your Silverlight applications. Most of the controls are the same as WPF; however, Silverlight also offers some exclusive controls, such as WebBrowser and ViewBox, to provide additional functionality for Web applications. The new controls offered by Silverlight are as follows:

- The AutoCompleteBox control
- The DataPager control
- The TreeView control
- The RichTextBox control
- The WebBrowser control
- The ViewBox control

Let’s learn how to use these controls, one by one.

### Using the AutoCompleteBox control

The **AutoCompleteBox** control, first introduced in Silverlight 3.0, is a combination of a text box and a drop-down list control. When you enter any text in the text box, a drop-down list is displayed that contains a list of all the possible values that match with the entered text. Using the **AutoCompleteBox** control, you can select an appropriate item from the drop-down list to complete your input in the text box rather than typing the entire word.

Perform the following steps to use the **AutoCompleteBox** control in a Silverlight application:

1. *Open* **Microsoft Visual Studio 2010** and *select* **File→New→Project**. The New Project dialog box appears.
2. *Select* **Visual C#→Silverlight** from the **Installed Templates** pane in the New Project dialog box.
3. *Select* **Silverlight Application** from the middle pane.
4. *Specify* the name of the application as **MyAutoCompleteBox** (also available on CD) in the **Name** text box and the appropriate location in the **Location** combo box.
5. Click the **OK** button. The **New Silverlight Application** dialog box appears.
6. *Select* the Host Silverlight application in a new Web site check box.
7. *Select* the **ASP.NET Web Application Project** option from the **New Web** project type drop down box.
8. *Select* **Silverlight 4** from the **Silverlight Version** drop down box.
9. *Select* the **Enable WCF RIA Services** check box.
10. Click the **OK** button. The **MyAutoCompleteBox** application is created.
11. *Replace* the code of **MainPage.xaml** file with the code shown in Listing 11.4, to design the UI of your application:

**Listing 11.4:** Showing the Code for the **MainPage.xaml** File of the **MyAutoCompleteBox** Application

```xml
<UserControl
    xmlns:sdk="http://schemas.microsoft.com/winfx/2006/xaml/presentation/sdk"
    x:Class="MyAutoCompleteBox.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d" d:DesignHeight="300" d:DesignWidth="400">

<Grid x:Name="LayoutRoot" Background="White">
<Border BorderThickness="4" BorderBrush="DarkBlue">
<StackPanel Background="Beige">
<TextBlock Margin="7" FontSize="18" FontFamily="Comic Sans MS"
           FontWeight="Bold" Foreground="DeepPink">
    Displaying the Use of an AutoCompleteBox Control</TextBlock>
<StackPanel x:Name="Layout" Orientation="Horizontal">
<StackPanel.Resources>
<Style x:Key="myTBStyle" TargetType="TextBox">
<Setter Property="Background" Value="LightYellow" />
<Setter Property="Foreground" Value="DarkSlateGray" />
<Setter Property="Margin" Value="5" />
<Setter Property="FontWeight" Value="Bold" />
<Setter Property="FontSize" Value="14" />
<Setter Property="BorderBrush" Value="DarkGray" />
</Style>
<Style x:Key="myLBStyle" TargetType="ListBoxItem">
<Setter Property="Background" Value="Khaki" />
<Setter Property="Foreground" Value="DarkSlateGray" />
<Setter Property="Margin" Value="5" />
<Setter Property="FontStyle" Value="Italic" />
<Setter Property="FontSize" Value="14" />
<Setter Property="BorderBrush" Value="DarkGray" />
</Style>
</StackPanel.Resources>
<TextBox Height="30" Width="Auto" IsReadOnly="True" Text="Enter a City"
         Style="{StaticResource myTBStyle}" BorderBrush="LightGray" />
<sdk:AutoCompleteBox Width="300" x:Name="myACB"
 TextBoxStyle="{StaticResource myTBStyle}"
 ItemContainerStyle="{StaticResource myLBStyle}"
 IsTextCompletionEnabled="True" MinimumPopulateDelay="0"
 MinimumPrefixLength="1"/>
</StackPanel>
</StackPanel>
</Border>
</Grid>
</UserControl>
```

In Listing 11.4, an AutoCompleteBox control, named myACB, is used whose appearance has been changed by creating new styles. A style tag with a unique key value, myTBStyle, is used to declare a style as a static resource and set as a value for the TextBoxStyle property of the text box in the AutoCompleteBox control, myACB. Similarly, a style with a unique key value, myLBStyle, is declared as a static resource and set as a value for the ItemContainerStyle property of the drop-down list in the AutoCompleteBox control, myACB. The AutoCompleteBox control, myACB, uses the style defined for its text box and drop-down list. Note that the IsTextCompletionEnabled property of the AutoCompleteBox control, myACB, is set to true to enable the auto-completion of the text as you type some text into the text box. In addition, the MinimumPopulateDelay and MinimumPrefixLength properties of the AutoCompleteBox control are also set to 0 and 1, respectively.

12. Open the code-behind file of MainPage.xaml (MainPage.xaml.cs) and replace its code with the code shown in Listing 11.5:

**Listing 11.5:** Showing the Code for the Code-Behind File of MainPage.xaml of MyAutoCompleteBox

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
namespace MyAutoCompleteBox
{
    public partial class MainPage : UserControl
    {
        public MainPage()
        {
            InitializeComponent();
            List<string> cityNames = new List<string>();
            cityNames.Add("Arizona");
            cityNames.Add("Atlanta");
            cityNames.Add("California");
            cityNames.Add("Chicago");
            cityNames.Add("Colorado");
            cityNames.Add("Denver");
            cityNames.Add("Detroit");
            cityNames.Add("Durham");
            cityNames.Add("Florida");
            cityNames.Add("Georgia");
            cityNames.Add("Hamilton");
            cityNames.Add("Hampshire");
            cityNames.Add("Lancaster");
            cityNames.Add("Las Vegas");
            cityNames.Add("Los Angeles");
            cityNames.Add("Michigan");
            cityNames.Add("New Jersey");
            cityNames.Add("New Orleans");
            cityNames.Add("New York");
            cityNames.Add("North Carolina");
            cityNames.Add("Ohio");
            cityNames.Add("Olympia");
            cityNames.Add("San Diego");
            cityNames.Add("San Francisco");
            cityNames.Add("San Jose");
            cityNames.Add("Seattle");
            cityNames.Add("Washington");
            cityNames.Add("Texas");
            myACB.ItemsSource = cityNames;
        }
    }
}
```

In Listing 11.5, a List variable, cityNames, is created and a number of city names are added to it. Next, this variable is passed as a value of the **ItemsSource** property of the **AutoCompleteBox** control.

13. **Press F5** to run the application. The output appears, (Fig.ASP-11.24).

14. Enter any character in the **Enter a City Name** text box, a drop-down list appears with the words starting with that character. In our case, we have entered the character S. The drop-down list appears, displaying the words starting with S, (Fig.ASP-11.25).

![](img/9862a98a1a2d3bb14334137965a1ec60_718_0.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_718_1.png)
