# 158 | CHAPTER 9 PROPERTIES

```
</Image.ContextMenu>
</Image>
<GroupBox Grid.Row="0" Grid.Column="1" Grid.ColumnSpan="2" Margin="10">
  <GroupBox Header>
    <StackPanel Orientation="Horizontal">
      <Label Content="Keys"/>
      <Image Width="30" Source="Keys.ico">
        <Image.BitmapEffect>
          <DropShadowBitmapEffect/>
        </Image.BitmapEffect>
      </Image>
    </StackPanel>
  </GroupBox>
  <Image Grid.Row="1" Grid.Column="0" Width="75" Source="Fog.jpg">
    <Image.LayoutTransform>
      <RotateTransform Angle="-10"/>
    </Image.LayoutTransform>
  </Image>
  <Label Content="Stretched Text" FontSize="25" Foreground="Yellow" HorizontalAlignment="Center" VerticalAlignment="Top" Margin="0, -40" Grid.Row="1" Grid.Column="1" Grid.ColumnSpan="2">
    <Label.RenderTransform>
      <TransformGroup>
        <ScaleTransform ScaleY="3"/>
        <SkewTransform Angle="20"/>
        <RotateTransform Angle="20"/>
      </TransformGroup>
    </Label.RenderTransform>
  </Label>
</Grid>
</Window>
```

# PropertyElements

The main Window element contains a Window.Background property element to make the Window display a red gradient-brush.

The Grid control contains Grid.ColumnDefinitions and Grid.RowDefinitions property elements to define its three columns and two rows.

The Image displays a lighthouse containing an Image.BitmapEffect property element to give the image a beveled appearance so it looks like a tall button. The original image doesn't have the shaded edges — those are added by the BevelBitmapEffect object.

That Image also has an Image.ContextMenu property element to define its context menu. The ContextMenu contains two MenuItems.

![](bbox=[0.545, 0.645, 0.875, 0.835])

FIGURE 9-3