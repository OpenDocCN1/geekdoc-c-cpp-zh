# LAYOUT AND RENDER TRANSFORMS

WPF controls have two transformation properties: LayoutTransform and RenderTransform.

WPF applies a control's LayoutTransform before it arranges that control and the others on the window. It then uses the transformed control's new width and height to calculate placement. For example, if you rotate a square 45 degrees, the result is a diamond that is wider and taller than the original. If the square is placed inside a StackPanel, the StackPanel will allow enough room for the rotated square to fit.

WPF applies a RenderTransform after the controls have been arranged and before they are drawn. This can produce some strange results in arranging controls such as StackPanel and WrapPanel, with controls sticking past the edges of the areas allocated by them.

RenderTransforms work well, however, if a control's container doesn't use control sizes to arrange its children. For example, a Canvas doesn't use control sizes to arrange controls, so RenderTransforms work there.

> TRANSLATION TRICKNESS

Depending on a control's container, transformations sometimes produce unexpected results or may have no noticeable effect.

For example, suppose you place a Label inside a Grid and give the Label a transformation. WPF translates the Label but centers it inside the Grid so it appears in the same place it would have been if you hadn't bothered with the translation.

In situations like this, it is easier to get the result if you use a RenderTransform instead of a LayoutTransform, or if you move the control into a Canvas.

The LayoutVsRender example program shown in Figure 20-3 demonstrates the difference between the LayoutTransform and RenderTransform properties.

The StackPanel on the left contains three Labels rotated with LayoutTransforms, so the StackPanel allows enough height for each rotated Label. After allowing room for the Labels, the StackPanel centers each of them.

The StackPanel on the right contains three Labels rotated with RenderTransformations. The StackPanel only allows enough vertical space for each Label to fit before it is rotated and then drops in the Labels whether they or not.

![](bbox=[0.553, 0.673, 0.863, 0.866])

FIGURE 20-3