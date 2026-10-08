
```csharp
{
    public partial class VSContextControl : UserControl
    {
        public VSContextControl()
        {
            InitializeComponent();
        }

        private void Grid_DataChanged(object sender, DependencyPropertyChangedEventArgs e)
        {
            var context = e.NewValue as DataSource;
            if (context == null) return;
            context.PropertyChanged += ContextPropertyChanged;
            RefreshContext(context);
        }

        private void ContextChanged(object sender, System.ChangedEventArgs args)
        {
            var context = sender as DataSource;
            if (context != null) RefreshContext(context);
        }

        private void RefreshContext(DataSource context)
        {
            Context.Items.Clear();
            AddIntrinsicPropertyValue(context, "CustomizationEnabled");
            AddIntrinsicPropertyValue(context, "ClosePageOpenProject");
            AddIntrinsicPropertyValue(context, "ShowPageAtStartup");
            AddIntrinsicPropertyValue(context, "Source");
            AddIntrinsicPropertyValue(context, "ExtensionId");
            AddIntrinsicPropertyValue(context, "WebProjectsSupported");
            AddDataSourcePropertyValue(context, "Links");
            AddDataSourcePropertyValue(context, "Background");
            AddDataSourcePropertyValue(context, "Rss");
            AddDataSourcePropertyValue(context, "RecentProjects");
            AddIntrinsicPropertyValue(context, "SelectedTabItemIndex");
            AddIntrinsicPropertyValue(context, "SelectedSubitem1Index");
            AddIntrinsicPropertyValue(context, "SelectedSubitem2Index");
            AddIntrinsicPropertyValue(context, "SelectedSubitem3Index");
            AddIntrinsicPropertyValue(context, "SelectedSubitem4Index");
        }

        private void AddIntrinsicPropertyValue(DataSource source, string propName)
        {
            var prop = source.GetValue(propName);
            Context.Items.Add(new ContextItem(propName, prop.ToString()));
        }

        private void AddDataSourcePropertyValue(DataSource source, string propName)
        {
            var props = source.GetValue(propName) as DataSource;
        }
    }
}
```

# LISTING 5-9 (continued)

```csharp
if (props == null) return;
var propNames = string.Concat(prop => prop.Name + "
```

Code file [VSControlContext.xaml] available for download from Wrox.

The Grid_DataContextChanged method occurs when the control data is set. This event is raised when Visual Studio parses the StartPage.xml file and instantiates the LayoutRoot grid. The context can be accessed through the e.NewValue property, which should be an instance of the DataSource class (declared in the Microsoft.Internal.Visual.PlatformUI namespace). The method body responds to the PropertyChanged event. You can experiment with how the page responds to property changes. You can check or uncheck the "Close page after project load" and see that "CustomizationEnabled" and "ClosePageOnOpenProject" property values will change accordingly.

If the data context or one of its properties is set, the RefreshContext method will set up the list with the current property values. The intrinsic properties (Boolean or string values) are handled by the AddIntrinsicPropertyValue method, while other properties with DataSource are displayed with the AddDataSourceProperty method.

The DataSource class provides a GetValue method to query the value of the property named in the argument. The value returned by this method is a System.Object that can be cast to the native type behind it. For all intrinsic properties, the ToString() method retrieves the representation of the property, and so it can be directly displayed.

There are properties (for example "Links") that retrieve a DataSource when querying their values with GetValue. With the Properties enumeration — be aware, not that you can obtain metadata-like type and name about the properties of the DataSource instance. As shown in Listing 5-9, the AddDataSourceProperty simply concatenates the property names.

# Accessing the Visual Studio Object Model

Table 5-5 lists property as part of the StartPage data context. Using this property, you can access the object model of Visual Studio. The root of this model is the DTE object (with the same name as its accessor property), and you can utilize it to programmatically carry out miscellaneous tasks with Visual Studio.

> The DTE object model covers more than hundred object types with more than a thousand methods and properties. DTE is used by macros, add-ins and VSPacks heavily. Chapter 6 provides more information about using DTE in several scenarios.

To have a simple example of using DTE, let's create a new Start Page that lists all available Visual Studio commands and allows the user to execute them. Figure 5-33 shows this Start Page in action.

![](img/b5597c749e848b27b0d305153ae16106_224_0.png)

**FIGURE 5-33:** The Start Page displaying Visual Studio commands

Create a new Start page and name it CommandListStartPage. Add the Microsoft .VisualStudio.Shell.Interop.10.0 assembly to the CommandListStartPageControl project. Modify the StartPage.xml file to rename the MyControl tab's header:

```xml
<TabItem Header="VS Command List" Style="{DynamicResource StartPage.TabItemStyle}">
  <my:MyControl/>
</TabItem>
```

Change the Grid within the MyControl.xml to define a ListBox control holding the collection of the Visual Studio controls:

```xml
<Grid Background="DynamicResource (x:Static vfx:VsBrushes.StartPageBackgroundColor)"
      DataContextChanged="Grid_DataContextChanged">
  <Border Margin="20" CornerRadius="10" BorderThickness="3"
          BorderBrush="DynamicResource (x:Static vfx:VsBrushes.StartPageSeparator)">
    <DockPanel HorizontalAlignment="Stretch"
               VerticalAlignment="Stretch">
      <TextBlock Foreground="DynamicResource (x:Static vfx:VsBrushes.StartPageTextBlock)">
        <TextBlock DockPanel.Dock=
```

The application logic is defined in the MyControl.xaml file, and it is very straightforward. The Grid_DataContextChanged catches the moment when the data context is set, and is used to obtain the list of commands. The CommandList_MouseDoubleClick method executes the selected command. Listing 5-10 shows this simple code-behind.

# LISTING 5-10: MyControl.xml (CommandListStartPage)

```csharp
using System;
using System.Windows;
using System.Windows.Controls;
using Microsoft.Internal.VisualStudio.PlatformUI;

namespace CommandListStartPageControl
{
    public partial class MyControl : UserControl
    {
        private dynamic _dte;

        public MyControl()
        {
            InitializeComponent();
        }

        private void Grid_DataContextChanged(object sender, DependencyPropertyChangedEventArgs e)
        {
            var context = e.NewValue as DataSource;
            if (context == null) return;
            _dte = context.GetValue("DTE");
            foreach (var command in _dte.Commands)
            {
                if (!string.IsNullOrEmpty(command.Name))
                    CommandList.Items.Add(command.Name);
            }
        }

        private void CommandList_MouseDoubleClick(object sender, System.Windows.Input.MouseButtonEventArgs e)
        {
            var command = CommandList.SelectedItem;
            if (command == null) return;
            try
            {
                _dte.ExecuteCommand(command);
            } catch (SystemException ex)
            {
                MessageBox.Show(ex.Message);
            }
        }
    }
}
```
