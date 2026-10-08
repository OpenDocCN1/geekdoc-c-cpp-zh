```
SelectedIndex="0">
</ListBox>
</ScrollViewer>
</GroupBox>
</DockPanel>

<GridSplitter Grid.Column="1" Grid.RowSpan="2" HorizontalAlignment="Left"
VerticalAlignment="Stretch" Width="15" Background="Transparent"
ShowsPreview="True" />

<GroupBox Grid.Column="1" Grid.Row="1" Margin="7,0,5,5">
<ScrollViewer VerticalScrollBarVisibility="Auto"
HorizontalScrollBarVisibility="Disabled">
<StackPanel>
<Label>Source:</Label><Label Content="{Binding Path=Source}" />
<Label>Size:</Label><Label/>
<Label>Date Image Taken:</Label><Label/>
<Label>Camera Manufacturer:</Label><Label/>
<Label>Camera Model:</Label><Label/>
<Label>Creation Software:</Label><Label/>
<Label>Lens Aperture:</Label><Label/>
<Label>Focal Length:</Label><Label/>
<Label>ISO Speed:</Label><Label/>
<Label>Exposure Time:</Label><Label/>
<Label>Exposure Mode:</Label><Label/>
<Label>Exposure Compensation:</Label><Label/>
<Label>White Balance Mode:</Label><Label/>
<Label>Color Representation:</Label><Label/>
</StackPanel>
</ScrollViewer>
</GroupBox>
```

Although this might seem like a lot of work to create a user interface that isn't very functional at the moment, it has several significant advantages over more traditional user interface development. The simplest, yet probably most significant, is that you can deliver the XAML file to a graphics-oriented person who can apply styles and other visual resources to make the application stand out while you can continue developing the core functionality of the application. As long as the underlying user interface controls aren't changed, the designer and the developer can both continue working without impacting the other.

# ## Styling the Layout

Styling a layout can actually mean a variety of different things, each with varying degrees of complexity. On one end of the spectrum is simply applying colors, background images, and various other visual elements directly to the controls. On the other end is creating complete style sheets (similar to Cascading Style Sheets [CSS] for web development) and data templates that can transform controls with an entirely new look.