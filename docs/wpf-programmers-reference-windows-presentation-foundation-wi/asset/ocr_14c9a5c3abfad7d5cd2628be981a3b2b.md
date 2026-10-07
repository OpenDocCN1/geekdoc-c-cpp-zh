# EXAMPLE Border and Grid

The following XAML code makes a simple Border containing a Grid that could hold other controls:

```
<Border Brush="Orange" BorderThickness="3" Background="Yellow"
CornerRadius="20" Width="100" Height="*100">
<Grid>
  ...
</Grid>
</Border>
```

# BULLETDECORATOR

The BulletDecorator displays a single item and bullet in a bulleted list. The Bullet property defines the bullet. The control's single child defines the content. The key properties are given in Table B-2.

# TABLE B-2: Key Properties of BulletDecorator

| PROPERTY | PURPOSE |
|---|---|
| Bullet | The object displayed as the bullet |
| Child | The object displayed next to the bullet |

# EXAMPLE Diamond-ShapedBulletDecorator

The following XAML code creates a blue diamond bullet to the left of the text “Bullet Point.” The code uses Margin properties to provide some separation between the bullet and the text.

```
<BulletDecorator>
  <BulletDecorator.Bullet>
    <Polygon Margin="2,0,0,0" Points="0,5 5,10 10,10" Fill="Blue"/>
  </BulletDecorator.Bullet>
  <TextBlock Margin="10,0,0,0" Text="Bullet Point"/>
</BulletDecorator>
```

Note that the BulletDecorator does not arrange controls in the same way that a StackPanel does. In particular, increasing the bullet’s right margin does not move the TextBlock further to the right. That’s why this code uses the TextBlock’s Margin property.

# DOCUMENTVIEWER