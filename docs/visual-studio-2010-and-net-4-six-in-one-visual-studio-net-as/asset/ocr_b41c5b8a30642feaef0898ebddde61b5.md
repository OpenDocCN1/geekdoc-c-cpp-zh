# Changing the StartPage.xml File

Although the Custom Start Page Template creates a clone of the Visual Studio Start Page so that you can customize it through the MyControl tab, you are not obliged to do so. If you want to create a simple Start Page and omit the information tabs that you can see by default, you can simplify the StartPage.xml file.

Create a new Start Page project with the Custom Start Page Template, as you have already done with the SimpleStartPage project. Now, this new project ModifiedStartPageControl when the solution has been generated, remove the ModifiedStartPageControl project — you won need it at all.

Using instead of user control, you will change the StartPage in the SimpleStartPage project so that all information tabs will be omitted. Instead, add two new tabs to display the Task List and display the New File dialog, respectively. The list of recent projects will be extended with a TextBox displaying the number of items in the list.

Listing 5-6 shows the modified StartPage.xml file. If you do not want to type it manually, just open the modifiedStartPage project that can be found in the downloaded source code of the book at www.wrox.com.

+   LISTING 5-6: StartPage.xml (ModifiedStartPage Project)

```
<xml xmlns="http://schemas.microsoft.com/winfx/2006/xml"
      xmlns:x="http://schemas.microsoft.com/winfx/2006/xml"
      xmlns:sp="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.Shell.StartPage"
      xmlns:vs="clr-namespace:Microsoft.VisualStudio.UI;assembly=Microsoft.VisualStudio.UI,Version=10.0"
      xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell,Version=10.0"
      mc:Ignorable="d"
      xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
      xmlns:mc="http://schemas.microsoft.com/markupformats/markup-compatibility/2006"
      d:DesignHeight="600" d:DesignWidth="800">

<Grid.Resources>
  <ResourceDictionary>
    <ResourceDictionary.MergedDictionaries>
      <ResourceDictionary>
        <Source="Microsoft.VisualStudio.Shell.StartPage;component/Styles/startpageresources.xml" />
      </ResourceDictionary>
    </ResourceDictionary.MergedDictionaries>
  </ResourceDictionary>
</Grid.Resources>

<Grid Name="LayoutRoot"
  Background="(DynamicResource x:Static vsfx:Brushes.StartPageBackgroundColor)"
  Style="(DynamicResource StartPage.OuterStyle)">
  <Grid Width="Auto" Column="0" Row="1" Margin="15,0,0,0,15"
    VerticalAlignment="Stretch />
</Grid>
```

continues