```
<Window x:Class="MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="ProVB_WPF" Height="335" Width="415" Name="MainWindow"
    WindowStyle="None" AllowsTransparency="True">
    <Window.Resources>
        <EllipseGeometry x:Key="RoundPanel" Center="36, 36" RadiusX="34" RadiusY="34">
        </EllipseGeometry>
    </Window.Resources>
    <Grid>
        <Grid.RowDefinitions>
            <RowDefinition Height="25" />
            <RowDefinition Height="215*" />
        </Grid.RowDefinitions>
        <Rectangle Name="TitleBar" HorizontalAlignment="Stretch" Margin="0,0,0,0" Stroke="Black" Fill="Green" VerticalAlignment="Stretch" />
        <Button HorizontalAlignment="Stretch" Margin="0,0,130,2" Name="ButtonBrowse">Images Folders</Button>
        <Button Height="20" Width="23" HorizontalAlignment="Right" Margin="0,1,1,0" Name="ButtonClose" VerticalAlignment="Top">
            <Image Margin="0,0,0,0" Name="Image2" Stretch="Fill" Source="/Resources/20by_Exit.JPG"/>
        </Button>
        <Button Height="20" Width="20" HorizontalAlignment="Right" Margin="0,1,25,0" Name="ButtonMax" VerticalAlignment="Top" >
            <Image Margin="0,0,0,0" HorizontalAlignment="Center" Name="Image3" Stretch="Fill" Source="/Resources/20by_Max.JPG"/>
        </Button>
        <Button Height="20" Width="20" HorizontalAlignment="Right" Margin="0,1,47,0" Name="ButtonMin" VerticalAlignment="Top" >
            <Image Margin="0,0,0,0" Name="Image4" Stretch="Fill" Source="/Resources/20by_Min.JPG"/>
        </Button>
        <Image Grid.Row="1" Margin="0,0,0,0" Name="Image1" Stretch="Uniform" />
        <StackPanel Background="Transparent" VerticalAlignment="Center" Margin="0,25,0,0" Height="75" Name="StackPanelNext" Grid.Row="1" HorizontalAlignment="Right" Width="75" Clip="{StaticResource RoundPanel}">
            <Button Grid.Row="1" HorizontalAlignment="Stretch" VerticalAlignment="Stretch" Name="ButtonNext" Height="75" Width="75" Visibility="Hidden">
                <Image Margin="0,0,0,0" Stretch="Fill" Source="/Resources/RightArrow.jpg"></Image>
            </Button>
        </StackPanel>
        <StackPanel Background="Transparent" VerticalAlignment="Center" Margin="25,0,0,0" Height="75" Name="StackPanelPrev" Grid.Row="1" HorizontalAlignment="Left" Width="75" Clip="{StaticResource RoundPanel}">
            <Button Grid.Row="1" HorizontalAlignment="Left" VerticalAlignment="Center" Name="ButtonPrev" Height="75" Width="75" Visibility="Hidden">
                <Image Margin="0,0,0,0" Stretch="Fill" Source="/Resources/LeftArrow.jpg"></Image>
            </Button>
        </StackPanel>
        <Thumb Grid.Row="1" Cursor="ScrollAll" Background="{StaticResource ResizeImage}" Height="20" Width="20" HorizontalAlignment="Right" Margin="0,0,0,0" Name="ThumbResize" VerticalAlignment="Bottom" />
    </Grid>
</Window>
```