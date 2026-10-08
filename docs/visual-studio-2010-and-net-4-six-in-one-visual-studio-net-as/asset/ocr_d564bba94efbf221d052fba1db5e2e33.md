# LISTING 5-4: StartPage.xaml (Recent Project List Definitions)

```
Available for download on Wprox.com  <StackPanel Grid.Row="*" Margin="0,0,0,10" Orientation="Horizontal">
<TextBlock Text="Recent Projects" VerticalAlignment="Top" Style="DynamicResource StartPage.HeadingTextStyle" x:Uid="RecentProjects"/>
<Path Alignment="Center" Margin="6,0,0,-4" Width="Auto" Height="1" StrokeThickness="11" StrokeLineJoin="Round" 
Stroke="DynamicResource (x:Static vs:Brushes.StartPageSeparatorKey)" 
Data="F M 0.5,0.5L 199.5,0.5"/>
</StackPanel>
<!-- MRU List Container -->
<ScrollView Grid.Row="1" HorizontalAlignment="Stretch" 
Style="DynamicResource StartPage.ScrollViewStyle" 
VerticalAlignment="Stretch" VerticalScrollVisibility="Auto">
<sp:MruListBox 
DataContext="(Binding RecentProjects)" 
ItemsSource="(Binding Path=Items)" 
Background="Transparent"
BorderThickness="0"
AutomationProperties.AutomationId="MruList"/>
</ScrollView>
```

Code file [StartPage.xaml] | available for download at Wrox.com

The sp:MruListBox WPF control implements the behavior in Figure 5-30. It simply binds the list to the RecentProjects.Items property of the Start Page's context.

# MyControl User Control

The Custom Start Page Template allows a simple customization to the Start Page — the MyControl you can see in Figure 5-27. The StartPage.xaml file adds this definition as a sample tab of the TabControl displaying the "Get Started," "Guidance..." and other tabs:

```
<Grid Grid.Row="*" Margin="0,35,15,15">
<TabControl Style="DynamicResource StartPage.TabControlStyle"
SelectedIndex="(Binding SelectedTabIndex, Mode=TwoWay)">
<TabItem Header="Get Started" Height="Auto" ... />
<!-- -- -->
</TabItem>
<TabItem Header="Guidance" Height="Auto" ... />
<!-- -- -->
</TabItem>
<TabItem Header="Latest News" ... />
<!-- -- -->
</TabItem>
<TabItem Header="MyControl" Style="DynamicResource StartPage.TabItemStyle">
<my:MyControl/>
</TabItem>
</TabControl>
</Grid>
```