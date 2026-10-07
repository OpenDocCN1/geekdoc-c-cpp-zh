# Ellipse Button Controls

Figure 15-12 shows the template's control structure. The controls' labels are shown in left-to-right and top-to-bottom order, so you tell tell controls are defined by the XAML code before the others. For example, the “Inner surface” is defined in the XAML code before the “Outer edge.”

A Grid (with a dashed box) contains all of the other controls, most of which are Ellipses.

The inner surface is an ellipse filled with a brush that shades from lime to green. It lies beneath all of the other controls.

The outer edge is an ellipse with a transparent parent center and a black edge. Because its StrokeThickness is 10, it forms a wide band around the control.

![](bbox=[0.537, 0.137, 0.93, 0.363])

| Grid | Outer edge | Inner surface | Edge highlight |
|---|---|---|---||
| | Upper left highlight | Lower right highlight | ContentPresenter |

The highlight is an ellipse with Margin = 4 and StrokeThickness = 4, forming a band within the outer edge. It has a transparent center. Its Stroke property is a gradient brush that shades from lime on the left, to transparent, lime on the right; this makes two highlights on the edge. Its BitmapEffect is set to a BlurEffect object, so it’s fuzzy, giving the edge a rounded, 3D appearance.

The sparkle highlight is not shown in Figure 15-12. It is similar to the green edge highlight except that it’s white and has only one visible piece instead of two. It is visible only when the mouse is over the control and is animated.

The upper-left highlight is an ellipse filled with a brush that shades from white to transparent. Its Margin property is set to 12, 12, 20, 20, it is a bit off the upper left.

The lower-right highlight is shown in Figure 15-12 as a dashed ellipse with Opacity = 0, making invisible. It is displayed when the user presses the button. If you look closely, you can see it in Figure 15-11. The upper-left highlight, this ellipse shades from white to transparent but is centered with a Margin value of 15.

The ContentPresenter is centered in the Template’s Grid.

The final Template control is a light gray ellipse that covers everything. Its Opacity is 0.3 and it tones down the color of all of the other controls.

Many of the controls have Opacity less than 1, so they are semitparent. When the control changes state—for example, when the mouse is over the button or the user presses the button—ton—the template’s Triggers change the Opacity of the controls to give a Button different appearance.