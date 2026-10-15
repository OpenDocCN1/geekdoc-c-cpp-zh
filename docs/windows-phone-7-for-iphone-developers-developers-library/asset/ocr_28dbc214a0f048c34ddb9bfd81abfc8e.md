```
<my:SelectedColorConverter x:Key="colorConverter"/>
</phone:PhoneApplicationPage.Resources>

<Grid x:Name="LayoutRoot" Background="Transparent">
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="*"/>
    </Grid.RowDefinitions>

    <StackPanel x:Name="TitlePanel" Grid.Row="0" Margin="12,17,0,28">
        <TextBlock x:Name="ApplicationTitle"
                   Text="Iso Store App"
                   Style="{StaticResource PhoneTextNormalStyle}"/>
        <TextBlock x:Name="PageTitle"
                   Text="Customers" Margin="9,-7,0,0"
                   Style="{StaticResource PhoneTextTitle1Style}"/>
    </StackPanel>

    <Grid x:Name="ContentPanel" Grid.Row="1" Margin="12,0,12,0">
        <ListBox x:Name="MainListBox" Margin="0,0,-12,0"
                 ItemsSource="{Binding Items}"
                 SelectionChanged="MainListBox_SelectionChanged">
            <ListBox.ItemTemplate>
                <DataTemplate>
                    <StackPanel Margin="0,0,0,17" Width="432"
                                Background="{Binding Path=IsSelected,
                                          Converter={StaticResource colorConverter}}">
                        <TextBlock Text="{Binding Name}"
                                   TextWrapping="Wrap"
                                   Style="{StaticResource PhoneTextExtraLargeStyle}"/>
                        <TextBlock Text="{Binding Description}"
                                   TextWrapping="Wrap" Margin="12,-6,12,0"
                                   Style="{StaticResource PhoneTextSubtleStyle}"/>
                    </StackPanel>
                </DataTemplate>
            </ListBox.ItemTemplate>
        </ListBox>
    </Grid>
</Grid>

<phone:PhoneApplicationPage.ApplicationBar>
    <shell:ApplicationBar IsVisible="True" IsMenuEnabled="false">
        <shell:ApplicationBarIconButton x:Name="appBarAddButton"
                                        IconUri="/Images/appbar.add.rest.png"
                                        Text="Add" Click="appBarAddButton_Click"/>
    </shell:ApplicationBar>
</phone:PhoneApplicationPage.ApplicationBar>
```