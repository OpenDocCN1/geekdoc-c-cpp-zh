# HOW'D YOU DO?

Your image will be different, of course, but here's my version:

```
<Window ...>
<Grid>
...
<BulletDecorator Grid.Row="0" Grid.Column="2"
 Background="Gainsboro" Margin="10">
 <BulletDecorator.Bullet>
 <Image Source="Thinking Hat.tif" Width="50" />
 </BulletDecorator.Bullet>
 </BulletDecorator>
 <Rectangle Margin="10" Fill="Black" />
 </BulletDecorator>
 <Border Grid.Row="1" Grid.Column="2" Background="Gainsboro" Margin="10"
 BorderBrush="Black" BorderThickness="10">
 <Ellipse Width="50" Height="50" Fill="Black" />
 </Border>
 <Viewbox Grid.Row="2" Grid.Column="2" Stretch="Fill">
 <Image Source="Thinking Hat.tif" />
 </Viewbox>
</Grid>
</Window>
```

# TAKE A BREAK

Compared to some of the WPF elements we've used, the shape and decorator classes are pretty easy to use. What they do is straightforward, and there aren't any tricky properties or structures to worry about. So why don't you take a break before we move on to building control templates with these and other objects?