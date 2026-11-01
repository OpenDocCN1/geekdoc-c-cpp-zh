+   - `StackPanel` — This control positions its child controls in a sequential horizontal or vertical layout.
+   - `WrapPanel` — This control positions its child controls in a sequential horizontal or vertical layout as `StackPanel`, but rather than a single row or column of controls, this control wraps its children into multiple rows or columns according to the space available.

You'll look at how to use these controls in more detail shortly. First, however, there are a few basic concepts to understand:

+   - How controls appear in stack order
+   - How to use alignment, margins, and padding to position controls and their content
+   - How to use the `Border` control

# Stack Order

When a container control contains multiple child controls, they are drawn in a specific stack order. You might be familiar with this concept from drawing packages. The best way to think of stack order is to imagine that each control is contained in a plate of glass, and the container contains a stack of these plates of glass. The appearance of the container, therefore, is what you would see if you looked down from the top through these layers of glass. The controls contained by the container overlap, so what you see is determined by the order of the glass plates. If a control is higher up the stack, then it will be the control that you see in the overlap area. Controls lower down may be partially or completely hidden by controls above them.

This also affects hit testing when you click on a window with the mouse. The target control will always be the one that is uppermost in the stack when considering overlapping controls. The stack order of controls is determined by the order in which they appear in the list of children for a container. The first child in a container is placed on the lowest layer in the stack, and the last child on the topmost layer. The children between the first and last child are placed on increasingly higher layers. The stack order of controls has additional implications for some of the layout controls that you can use in WPF, as you will see shortly.

# Alignment, Margins, Padding, and Dimensions

Earlier examples used the `Margin`, `HorizontalAlignment`, and `VerticalAlignment` properties to position controls in a Grid container, but without going into much detail about their use. You have also seen how you can use `Height` and `Width` to specify dimensions. These properties, along with `Padding`, which you haven't looked at yet, are useful for all of the layout controls (or most of them, as you will see), but in different ways. Different layout controls can also set default values for these properties. You'll see a lot of this by example in subsequent sections, but before doing that, it is worth covering the basics.

The two alignment properties, `HorizontalAlignment` and `VerticalAlignment`, determine how the control is aligned. `HorizontalAlignment` can be set to Left, Right, Center, or Stretch. Left and Right tend to position controls to the left or right edges of the container, Center positions controls