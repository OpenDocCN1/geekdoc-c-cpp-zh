
appearing (for example, Key.snk) and the "Protect my key file with a password" checkbox. Click OK, and the key file is immediately added to the project.

The user interface of the wizard is a simple list box, as shown in 4-19.

The user interface of the wizard is a WPF form using controls and data binding to keep the UI logic simple. A WPF User Control item to the project with the CommentSelector.xaml name. Listing 4-7 shows the XAML file defining it.

![](img/b5597c749e848b27b0d305153ae16106_143_0.png)

FIGURE 4-19: The UI of the Simple Comment Wizard

# LISTING 4-7: CommentSelector.xaml

Available for download on Wrox.com

```
<Window x:Class="SimpleCommentWizard.CommentSelector"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xml"
xmlns:mc="http://schemas.microsoft.com/expression/2006/markup/2006"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:src="clr-namespace:SimpleCommentWizard"
mc:Ignorable="d"
d:DesignHeight="300" d:DesignWidth="300" ResizeMode="NoResize"
Title="Comment Wizard"
Width="300" Height="220" WindowStartLocation="CenterScreen">
<Resources>
<src:CommentDescriptorCollection x:Key="CommentTypes">
  <src:CommentDescriptor
  ShortName="No restriction"
  Description="You can use this application with no restriction."/>
  <src:CommentDescriptor
  ShortName="AS"
  Description="The application is provided as it is."/>
  <src:CommentDescriptor
  ShortName="No commercial use"
  Description="The application cannot be used in commercial products."/>
</src:CommentDescriptorCollection>
</Resources>
<DockPanel>
<DockPanel DockPanel.Dock="Bottom" Height="36" Margin="4">
<Button Name="OK" IsDefault="true" DockPanel.Dock="Right"
Width="80" Margin="4" Click="OK_Click">OK</Button>
<Button Name="CancelButton" HorizontalAlignment="Right"
DockPanel.Dock="Right" Width="80" Margin="4"
Click="Cancel_Click">Cancel</Button>
</DockPanel>
</DockPanel>
<StackPanel Margin="4">
<TextBlock x:Name="4">Select a comment:</TextBlock>
<ListBox x:Name="CommentListBox" Margin="4" SelectedIndex="0"
ItemsSource="{StaticResource CommentTypes}">
</StackPanel>
</Window>
```

* www.it-ebooks.info

```
<DisplayMemberPath="ShortName" />
<Border BorderBrush="DarkGray" Margin="4" BorderThickness="2">
<TextBlock HorizontalAlignment="Stretch" TextWrapping="Wrap"
VerticalAlignment="Stretch" Padding="8,8,8,8"
Text="{Binding ElementName=CommentListBox, Path=SelectedItem.Description}
Background="LightGoldenrodYellow" />
</TextBlock>
</Border>
</StackPanel>
</DockPanel>
</Window>
```

Code file [CommentSelector.xml] available for download at Wrox.com

Although you have added a WPF user control, which you change to a WPF window, as you can see from Listing 4-7. The code-behind of the XAML definition is very simple. It responds on the OK and Cancel buttons, as shown in Listing 4-8.

![](img/b5597c749e848b27b0d305153ae16106_144_0.png)

# LISTING 4-8: CommentSelector.xml

```
using System.Windows;

namespace SimpleCommentWizard
{
    public partial class CommentSelector : Window
    {
        public string SelectedComment { get; set; }
        public CommentSelector()
        {
            InitializeComponent();
        }

        private void OkButton_Click(object sender, RoutedEventArgs args)
        {
            var comment = CommentListBox.SelectedItem;
            SelectedComment = comment == null ? null : comment.Description;
            Close();
        }

        private void CancelButton_Click(object sender, RoutedEventArgs args)
        {
            SelectedComment = null;
            Close();
        }
    }
}
```

Code file [CommentSelector.xml.cs] available for download at Wrox.com

The SelectedComment property holds the value of the comment to be inserted into the source code. CancelButton sets to null, the OkButton assigns it with the value of the description belonging to the comment selected in the list.

The CommentListBox control is responsible for listing the comments from which the user can select. It binds a collection of CommentDescriptor items defined in Listing 4-9.

# LISTING 4-9: CommentDescriptor.cs

```
using System.Collections.Generic;

namespace SimpleCommentWizard
{
    class CommentDescriptor
    {
        public string ShortName { get; set; }
        public string Description { get; set; }
    }

    class CommentDescriptorCollection : List<CommentDescriptor>
    {
    }
```

> Code file [CommentDescriptor.cs] available for download at Wrox.

Add a new class with name CommentDescriptor.cs to the project and copy the content of the listing into the file. The CommentSelector.xml file defines a resource with the key CommentTypes bound to the file.

## Implementing IWizard

Table 4-7 shows a few methods to implement the IWizard interface.

| METHOD | DESCRIPTION |
| --- | --- |
| BeforeOpeningFile | Runs the wizard logic after the code generation, when an item is about to open in the IDE with its corresponding editor. The method accepts an input parameter with the type of EnvDTE.WidgetItem that describes the item to be opened. When you implement this method, you can obtain information about the item to be opened, or even change the item's properties. |
| ProjectFinishedGenerating | Runs the wizard logic when a project has finished generating. This method is called by the IDE only when the wizard belongs to a project template. The method has an input parameter with the type of `EnvDTE.Project` that describes the project. You can use this method to obtain information about the project or to change the project structure. This method is a good placeholder for activities to add new files to the projects — or change existing ones — according to the information collected from the user. |
| ProjectItemFinishedGenerating | Runs the wizard logic when a project item has finished generating. This method is called by the IDE only when the wizard belongs to an item template. The method has an input parameter with the type of `EnvDTE.ProjectItem` that describes the item generated. You can use this method to obtain information about the item or to change its properties. |
| RunFinished | Runs wizard logic when the wizard has completed all the tasks. You can use this method to clean up resources used by the wizard. |
| RunStarted | Runs custom wizard logic at the beginning of a template run. This is the method where the user interface of the wizard will be displayed. The user interface can collect information from the user and build the template accordingly. This method has four parameters: `automationObject` — This is a reference to an automation object, allowing access to the `EnvDTE` instance representing IDE objects and services. `replacementsDictionary` — this is a dictionary associating placeholders and their replacement values. |
| ShouldAddProjectItem | Indicates whether the project item should be added to the project. The parameter of the method is the full path to the file. |

The order of the methods shown in Table 4-7 does not reflect the order and mode they are fired in. Following is the real order these methods called:

1. Before any other activities happen, for any kind of wizard, the RunStarted method is called to initialize your wizard logic and collect information from users through the UI.
2. The template system uses the replacement dictionary (the RunStarted method can override the default), and creates the list of files to be added to the project. ShouldAddProjectItem is called for each file with the full path of the file. Returning true from this method tells the template system to add the file in the project and add any replacements in the original template file.
3. When all files have been added, one of the ProjectFinishedGenerating or the ProjectFinishedGenerating methods is called, depending on whether it is a project or an item. In both cases, the automation object representing the project or the item is passed to the appropriate method.
4. For each file the OpenInEditor was set to true in the template manifest file, the BeforeOpenFile is called, passing the automation object representing the.
5. At the very end, the RunFinished method is called.

The IWizard interface implementation is really not as complex as it may seem according to Table 4-7 and the steps just described. Listing 4-10 shows how the Simple Comment Wizard does this job.
