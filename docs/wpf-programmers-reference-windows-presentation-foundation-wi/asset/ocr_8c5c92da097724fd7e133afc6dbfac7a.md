# RESTRICTED SKINS

If you use different skins for different kinds of users (e.g., the order entry clerk and shipping clerk described in the previous section), you'll need to restrict the skins that each user can load. For example, you probably wouldn't want the shipping clerk to be able to load the billing clerk's skin and view the customer's credit card information.

When it displays its red interface, this program adds a small Image in its upper-right corner. This Image has a context menu that displays the choices Red and Blue (shown on the left in Figure 16-8), which let you pick between the red and blue skins.

![](bbox=[0.147, 0.335, 0.705, 0.487])

FIGURE 16-8

The program's blue interface displays a label in its upper-right corner (on the right in Figure 16-8) that displays the same context.

The following code shows how the program displays its Options textbox on the blue interface:

```
<Label MouseDown="Options_MouseDown"
Grid.Row="0" Grid.Column="2" Margin="2"
Content="Options" FontSize="10"
HorizontalAlignment="Right" VerticalAlignment="Top"
Foreground="Black" BorderBrush="Black"
BorderThickness="1"
Visibility="DynamicResource visBlue")/>
<Label.Background>
<LinearGradientBrush StartPoint="0,0" Offset="0,1">
<GradientStop Color="Lime" Offset="0"/>
<GradientStop Color="Green" Offset="1"/>
</LinearGradientBrush>
</Label.Background>
<Label.ContextMenu>
<ContextMenu Name="ctxOptions">
<MenuItem Header="Red" Background="Pink"
Foreground="Red"
Click="ctxSkin_Click" Tag="Reshed.xml"/>
<MenuItem Header="Blue" Background="LightBlue">
</ContextMenu>
</Label.ContextMenu>
```