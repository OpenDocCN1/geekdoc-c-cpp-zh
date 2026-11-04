# Figure 2-10: Margin and Padding.

![](bbox=[0.28, 0.16, 0.58, 0.46])

Fortunately, there is a simple solution. By setting the Grid.IsSharedSizeScope attached property on the parent Grid, all the child Grids can define Rows and Columns that subscribe to a SharedSizeGroup, and the rendering engine will ensure that they are sized correctly. Figure 2-12 illustrates the effects of setting these properties. The abbreviated XAML is shown in Listing 2-10.

# Listing 2-10: Shared Size Groups

```
<Grid Grid.IsSharedSizeScope="False">
    <Grid Grid.Row="1" Grid.Column="0">
        <Grid.RowDefinitions>
            <RowDefinition Height="Auto" />
            <RowDefinition Height="Auto" />
        </Grid.RowDefinitions>
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="Auto" SharedSizeGroup="Header" />
            <ColumnDefinition Width="*" />
        </Grid.ColumnDefinitions>
    </Grid>
    <Grid Grid.Row="3" Grid.Column="0">
        <Grid.RowDefinitions>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="Auto"/>
        </Grid.RowDefinitions>
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="Auto" SharedSizeGroup="Header"/>
            <ColumnDefinition Width="*" />
        </Grid.ColumnDefinitions>
    </Grid>
</Grid>
```

# Figure 2-11: Multiple grids without shared sizing.

![](bbox=[0.28, 0.85, 0.48, 0.97])