```
</Storyboard>
</phone:PhoneApplicationPage.Resources>

<Grid x:Name="LayoutRoot" Background="Transparent">
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="*"/>
    </Grid.RowDefinitions>

    <StackPanel
        x:Name="TitlePanel" Grid.Row="0" Margin="12,17,0,28">
        <TextBlock x:Name="ApplicationTitle"
Text="MY APPLICATION" Style="{StaticResource PhoneTextNormalStyle}"/>
        <TextBlock x:Name="PageTitle" Text="page name"
Margin="9,-7,0,0" Style="{StaticResource PhoneTextTitle1Style}"/>
        <!-- <ListBox x:Name="myList">
            <ListBox.ItemTemplate>
                <DataTemplate>
                    <StackPanel Orientation="Horizontal">
                        <Image Source="pistol_bullet.png"/>
                        <TextBlock Height="30" Text="{Binding}"
                            Margin="10,10,10,10" />
                    </StackPanel>
                </DataTemplate>
            </ListBox.ItemTemplate>
        </ListBox>-->
        <Canvas Width="300" Height="500">
            <Button Canvas.Top="10"
                Canvas.Left="10"
                x:Name="animateButton"
                Click="animateButton_Click">
                <TextBlock Text="Click to Animate"/>
            </Button>
        </Canvas>
        <TextBlock x:Name="buttonPosition" Text="(none)"/>
    </StackPanel>

    <Grid x:Name="ContentPanel" Grid.Row="1"
        Margin="12,0,12,0"></Grid>
</Grid>
</phone:PhoneApplicationPage>
```

At this point, your app won’t compile, so resist the urge to click Build. We still need to write a few more lines of code.