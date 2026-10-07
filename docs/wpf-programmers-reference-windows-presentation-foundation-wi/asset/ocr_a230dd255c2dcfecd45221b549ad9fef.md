A child control can use attached properties to tell the Canvas how to position the child. The key attached properties of Canvas are given in Table C-2.

# TABLE C-2: Key Attached Properties of Canvas

| PROPERTY | PURPOSE |
| Canvas.Bottom | Sets the distance between the child's bottom edge and the Canvas's bottom edge. |
| Canvas.Left | Sets the distance between the child's left edge and the Canvas's left edge. |
| Canvas.Right | Sets the distance between the child's right edge and the Canvas's right edge. |
| Canvas.Top | Sets the distance between the child's top edge and the Canvas's top edge. |

The control will honor only one attached property vertically or horizontally. For example, if you specify both Canvas.Left and Canvas.Right, then the Canvas honors the Left value and ignores the Right value.

# EXAMPLE Using Canvas

The following code positions a Label 10 pixels from the upper-left corner of a Canvas and a TextBox 10 pixels from the lower-right corner:

```
<Canvas>
  <Label Canvas.Left="10" Canvas.Top="10" Content="First Name:"/>
  <TextBox Canvas.Right="10" Canvas.Bottom="10" Width="100"/>
</Canvas>
```

# DOCKPANEL

The DockPanel lets you attach controls to its top, left, right, and bottom edges. The key properties of DockPanel are given in Table C-3.

# TABLE C-3: Key Properties of DockPanel

| PROPERTY | PURPOSE |
| Background | The color used to fill the DockPanel's interior |
| LastChildFill | If True, the DockPanel makes its last child fill all remaining available space. |

A child control can use these properties to tell the DockPanel how to position the child. The key attached properties of DockPanel are given in Table C-4.