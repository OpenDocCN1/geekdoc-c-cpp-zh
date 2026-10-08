```
<MediaElement Width="100" Height="75">
Source="http://mschnline.vo.llnwd.net/di/ch9/0/8/7/7/4/
SL3Expression3Launch_ch9.wmv" />
</StackPanel>
</Button.Content>
</Button>
```

In this snippet, the TextBlock has also received a new, VerticalAlignment attribute. If it is omitted, the TextBlock will have the same height as the MediaElement next to it, and thus, the text will be displayed on the top instead of inside the medium.

This shows how Silverlight works. It is not the controls that determine and how they will be displayed, rather rather their containing. The StackPanel arranges its children to be each other (if the Orientation property is set to the default value of Orientation.Vertical), or the children can be next to each other (if the Orientation property is Orientation.Horizontal).

The actual layout is a little bit more complex. The children have their say in what size they would prefer to be. This allows for adapting to the size of the content. As the first step of the layout, from the top of the visual tree, Silverlight asks every element how it would like to be by calling the MeasureOverride method. Composite controls, like Panels and ContentView calculate their answers by invoking the MeasureOverride method of their children.

In the second step, the ArrangeOverride method is called throughout the entire tree in a similar manner. In this case, the parents tell their children the actual amount of space available for them — and it is the responsibility of children to fit in. If the available space is smaller than what the control needs can add a scroll bar, scale their content to a size (such as an image or video), or simply perform a crop. The ultimate limit for how big the root element can be is the size given to the HTML <object> tag — or, in the case of an out-of-browser (OOB) application, the size of the hosting window.

# Layout Containers in Silverlight

Layout containers in Silverlight include the following:

+   - Border
- Canvas
- StackPanel
- Grid
- Viewbox

# Border

Borders can have only one child. (But, as in the previous Button, this can be another layout container.) As name implies, Border puts a border around its content.

```
<Border HorizontalAlignment="Center" VerticalAlignment="Center">
BorderBrush="Black" BorderThickness="3" CornerRadius="5">
<TextBox Text="TextBox with a lot of text" Background="LightGray" />
</Border>
```