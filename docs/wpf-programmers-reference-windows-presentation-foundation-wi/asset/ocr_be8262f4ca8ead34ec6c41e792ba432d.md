# Tile Brushes

A tile brush fills an area with a repeating pattern. That pattern can be an image, a drawing, or a dynamic drawing that animates at run. The following sections describe the three kinds of tile brushes: image brush, drawing brush, and visual brush.

# Image Brush

An image brush fills an area with a picture. You can use the brush's properties to display some or all of the picture on some or all of the filled area, stretching the picture if necessary.

To make an image brush, create an Image control containing the picture that you want to use. In the Objects and Timeline area, select the new Image control.

On the Tools menu, open the "Make Brush Resource" submenu, and select "Make Image Brush Resource" to open the CreateImageBrush Resource dialog shown in Figure 3-12.

Give it a good name and click OK.

At this point, Expression Blend has created the brush resource.

![](bbox=[0.515, 0.223, 0.866, 0.385])

FIGURE 3-12

> EXPENDABLE IMAGE
After creating the image brush, Expression Blend no longer needs the Image control that you used to create it. You can delete that control if you like.

To see the new brush, click on the Resources tab on Expression Blend's right panel. Click the dropdown to the right of the brush to open the Brush Property dialog shown in Figure 3-13.

The "Tile mode" determines how the image is repeated if necessary to fill the area and can take the following values:

+   - None — The image is not repeated. Parts of the area may be unfilled if a single copy of the image doesn't fill the area completely.

+   - FlipX — The image is flipped horizontally to create new columns of the image.

+   - FlipY — The image is flipped vertically to create new rows of the image. (If you look closely at Figure 3-13, you'll see

![](bbox=[0.646, 0.643, 0.866, 0.843])

FIGURE 3-13