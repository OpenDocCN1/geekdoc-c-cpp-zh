
```xml
VisualStudio.Shell.StartPage;component/Images/StartPage/
"
<vs:ImageButton>
</Grid>
<!-- Recent Projects -->
<Grid Row="1" HorizontalAlignment="Left" Width="779">
<GridRowDefinitions>
<RowDefinition Height="Auto" />
<RowDefinition Height="Auto" />
<RowDefinition Height="Auto" />
</GridRowDefinitions>
<TextBlock Text="Recent Projects" VerticalAlignment="Top"
Style="{DynamicResource StartPage.HeadingTextStyle}" 
x:Uid="RecentProjects" />
<ScrollView Row="1" HorizontalAlignment="Stretch"
Style="{DynamicResource StartPage.ScrollViewStyle}" 
VerticalScrollBarVisibility="Auto">
<ListBox
DataContext="{Binding RecentProjects}"
ItemsSource="{Binding Path=Items}" 
Background="Transparent"
BorderThickness="0" 
AutomationID="MruList" />
</ScrollView>
<!-- Recent project count label -->
<WrapPanel>
<TextBlock Foreground="{DynamicResource Brushes.StartPageTextBlock}" />
<TextBlock Row="2" Text="Number of recent projects: " />
<TextBlock Text="{Binding RecentProjects.Items.Count}" />
</WrapPanel>
</Grid>
</Grid>
```

Although this list looks long, the code in the original is shorter than the original StartPage.xaml template. Most of the code in the original file was related to the information tabs, and those are removed. This listing uses the same pattern as Listing 5-3 to define command buttons, and the same code as used in Listing 5-4 to implement the project list. The command buttons have been changed to include the View.Tasklist and File.NewFile commands — have a look at the CommandParameter properties of the vs:ImageButton.

The recent project count label is composed from two TextBlock elements embedded into a WrapPanel. The Text property of the second element is simply bound to the RecentProjects.Items.Count path to display the counter.

Build and run the project. Then go to the Tools > Options to select the "[Installed Extension] ModifiedStartPage item in the Customize Start Page combo box to display the new Start Page. Page 5-31 shows how this new page loads.

![](img/b5597c749e848b27b0d305153ae16106_217_0.png)

**FIGURE 5-31: The Start Page implemented in the ModifiedStartPage project**

## Accessing the Visual Studio Context

The previous example showed that the Start Page accesses the current Visual Studio context. For example, the list of recent projects was bound to its list box with the following declaration (in Listing 5-4 and Listing 5-5):

```xml
<mru:MruListBox
DataContext="{Binding RecentProjects}"
ItemsSource="{Binding Path=Items}"
Background="Transparent"
BorderThickness="0"
AutomationProperties.AutomationId="MruList"/>
```

Here the DataContext of the MruListBox control is bound to the RecentProjects data source property of the control's parent.

You might also have noticed that the MyControl property displays the name of the application with the following binding:

```xml
<TextBlock
Text="{Binding Path=DTE.Name}"
FontSize="12"
HorizontalAlignment="Center"/>
```

Here the DTE.Name property of the parent control's data context provides that name.

The Start Page is a XAML file that is loaded and parsed by Visual Studio at start-up, or when you change the current Start Page in the Options dialog. After the XAML file is loaded, the LayoutRoot grid is instantiated, and its DataContext property is set to an instance of the Microsoft.Internal.VisualStudio.PlatformUI.DataSource class that can be found in the Microsoft.VisualStudio.Shell.10.0.dll assembly.

Table 5-5 summarizes the properties of the data context for the LayoutRoot grid.

### Table 5-5: Visual Studio Context Properties

| PROPERTY | DESCRIPTION |
| --- | --- |
| CustomizationEnabled | This flag indicates whether the customization of the Shell (menus, toolbars) is enabled. |
| CloseTabPageOpen | This flag indicates whether the Start Page should be closed when a project is opened. |
| ShowTabPageStartup | This flag indicates whether the Start Page should be displayed by Visual Studio Startup. |
| Source | This property shows the full name of the Start Page currently used. |
| ExtensionId | This string shows the identifier of the extension defining the Start Page currently used. |
| WebProjectsSupported | This flag indicates whether the Visual Studio instance supports web projects. |
| TeamFoundationClientSupported | This flag indicates whether the Visual Studio instance running accounts accessing Team Foundation Server access. |
| Links | This data source property allows access to the links that can be found on the Start Page tabs. |
| Background | This data source property allows accessing data related to information to be painted in the background, such as the logo bitmap and the application name. |
| Rss | This data source property can be used to access RSS information displayed on the Latest News Start Page tab. |
| RecentProjects | This data source property can be used to access the list of recent projects. |

### TABLE 5-5 (continued)

| PROPERTY | DESCRIPTION |
| --- | --- |
| SelectedTabIndex | This integer stores the index of the tab currently on the Start Page. |
| SelectedItem1Index, SelectedItem2Index, SelectedItem3Index, SelectedItem4Index | These integer properties allow up to four hierarchical levels under the Start Page tabs. Each property stores the index of the current selection at the related level. |
| DTE | This property allows you to access the root DTE object of Visual Studio (the root object of the Visual Studio run-time model that can be used by extensions). |

While you are using these properties from XAML, you can use the (Binding) markups. To access from them, you need a workaround.

Let's create a new Start Page extension so that you can see how these properties can be used programmatically. When this extension runs, it displays information about the context properties summarized in Table 5-5, as shown in Figure 5-32.

![](img/b5597c749e848b27b0d305153ae16106_219_0.png)

FIGURE 5-32: The Start Page displaying context information

Create a new project with the Custom Start Page Template and name it ContextPage. Change the name of the MyControl in the StartPage.xaml to "VS Context" (you'll find this TabItem almost at the start of the file):

```xml
<TabItem Header="VS Context" Style="DynamicResource StartPage.TabItem">
  <my:VSContext />
</TabItem>
```

```xml
<UserControl x:Class="ContextPage.VSContext"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="d"
xmlns:my="clr-namespace:ContextPage"
xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell, Version=10.0"
d:Height="300" d:Width="300">
<Grid Background="{StaticResource vsfx:Brushes.StartBackgroundColor}"
     DataContextChanged="Grid.DataContextChanged">
<Border Margin="20" CornerRadius="10" BorderThickness="3" Border="{StaticResource vsfx:Brushes.StartPageSeparator}">
<DockPanel>
</Border>
</Grid>
</UserControl>
```

This code does not contain anything. Instead of using the default ListBox appearance, this source defines a simple ItemTemplate for the list box in Figure 5-32. Add the ContextItem.cs to the ContextPageControl to encapsulate information about context properties. This contains a very simple data object, as shown in Listing 5-8.

### LISTING 5-8: ContextItem.cs

```csharp
namespace ContextPage
{
    public class ContextItem
    {
        public ContextItem(string name, string value)
        {
            Name = name;
            Value = value;
        }

        public string Name { get; private set; }
        public string Value { get; private set; }
    }
}
```

The lion's share of the work is in the code-behind file of the VSContextControl. It responds to the events when the control's DataContext property is set, or any of the properties the current data context change. When any of these changes occur, the content of the ListBox is refreshed, as shown in Listing 5-9.

### LISTING 5-9: VSContextControl.xaml.cs

```csharp
using System;
using System.Windows;
using System.Windows.Controls;
using Microsoft.Internal.VisualStudio.PlatformUI;
using System.Linq;

namespace ContextPage
{
    public partial class VSContextControl : UserControl
    {
        private void DataContextChanged(object sender, DependencyPropertyChanged e)
        {
            // Implementation here
        }
    }
}
```
