# Decoration

You can add decorations to a single element with the `Decorator` class. `Decorator` is a base class that has derivations such as `Border`, `Viewbox`, and `BulletDecorator`. Theme elements such as `ButtonChrome` and `ListBoxChrome` are also decorators.

The following example demonstrates a `Border`, `Viewbox`, and `BulletDecorator`, as shown in Figure 34.4. The `Border` class decorates the `Children` element by adding a border around it. You can define a brush and the thickness of the border, the background, the radius of the corner, and the padding of its children (code file `ControlsSample/DecorationsWindow.xaml`):

```
<Border BorderBrush="Violet" BorderThickness="5.5">
    <Label>Label with a border</Label>
</Border>
```

![](bbox=[0.11, 0.341, 0.892, 0.769])

# Figure 34.4

The `Viewbox` stretches and scales its child to the available space. The `StretchDirection` and `Stretch` properties are specific to the functionality of the `Viewbox`. These properties enable specifying whether the child is stretched in both directions, and whether the aspect ratio is preserved:

```
<Viewbox StretchDirection="Both" Stretch="Uniform">
```