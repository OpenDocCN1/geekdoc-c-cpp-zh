# Command Button Definitions

The Visual Studio 2010 Ultimate Edition's Start Page contains three command buttons in its top-left part under the logo, as shown in Figure 5-29.

These buttons are defined with the XAML code extract shown in List 5-3.

![](bbox=[0.718, 0.105, 0.928, 0.172])

FIGURE 5-29: Command buttons on the Start Page

+   LISTING 5-3: StartPage.xaml (Command Button Definitions)

```
<Grid x:Name="commandButtonsGrid" MinWidth="270" Grid.Row="0" Margin="0,15,0,30" HorizontalAlignment="Left">
<Grid.RowDefinitions>
<RowDefinition Height="Auto"/>
<RowDefinition Height="3"/>
<RowDefinition Height="Auto"/>
<RowDefinition Height="3"/>
<RowDefinition Height="Auto"/>
</Grid.RowDefinitions>
<ImageButton x:Id="ConnectTSSButton" Margin="15,2,15,2" Width="Auto"
Content="Connect To Team Foundation Server"
Visibility="(Binding Path=TeamFoundationClientSupported, Converter={StaticResource boolToVisibilityConverter})"
Style="DynamicResource StartPage.ProjectCommand.ButtonStyle"
Command="{Static sp:VSCommands.ExecuteCommand}"
CommandParameter=".../ConnectToTSSTeamFoundationServer"
ImageNormal=".../ConnectTFSS.png"
ImageHover=".../ConnectTFSMouseOver.png"
ImagePressed=".../ConnectTFSMouseDown.png />
</ImageButton>
<ImageButton Grid.Row="2" x:Id="NewProjectButton" Margin="15,2,0,2" Width="Auto"
Content="New Project..."
Style="DynamicResource StartPage.ProjectCommand.ButtonStyle"
Command="{Static sp:VSCommands.ExecuteCommand}"
CommandParameter="File.NewProject"
ImageNormal=".../NewProject.png"
ImageHover=".../NewProjectMouseOver.png"
ImagePressed=".../NewProjectMouseDown.png" />
</ImageButton>
<ImageButton Grid.Row="4"
```

continues