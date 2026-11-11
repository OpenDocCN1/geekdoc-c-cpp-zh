
| `java.awt.image.ColorModel` | 1.2 |
|---|---|
| `int getRGB(Object data)` | returns the ARGB value that corresponds to the sample data passed in the data array. Its element type and length depend on the color model. |
| `Object getDataElements(int argb, Object data);` | returns the sample data for a color value. If data is not null, it is assumed to be an array that is appropriate for holding sample data, and it is filled. If data is null, a new array is allocated and filled with the sample data for a pixel. Its element type and length depend on the color model. |

| `java.awt.Color` | 1.0 |
|---|---|
| `Color(int argb, boolean hasAlpha)` 1.2 | creates a color with the specified combined ARGB value if hasAlpha is true, or the specified RGB value if hasAlpha is false. |
| `int getRGB()` | returns the ARGB color value corresponding to this color. |

## 11.4.2.2 Filtering Images

In the preceding section, you saw how to build up an image from scratch. However, often you want to access image data for a different reason: You already have an image and you want to improve it in some way.

Of course, you can use the getPixel/getDataElements methods that you saw in the preceding section to read the image data, manipulate them, and write them back. Fortunately, the Java 2D API already supplies a number of filters that carry out common image processing operations for you.

The image manipulations all implement the `BufferedImageOp` interface. After you construct the operation, simply call the filter method to transform an image into another.

```java
BufferedImageOp op = . . .;
BufferedImage filteredImage
    = new BufferedImage(image.getWidth(), image.getHeight(), image.getType());
op.filter(image, filteredImage);
```

Some operations can transform an image in place (`op.filter(image, image)`), but most can’t.

Five classes implement the `BufferedImageOp` interface:

- `AffineTransformOp`
- `RescaleOp`
- `LookupOp`
- `ColorConvertOp`
- `ConvolveOp`

The `AffineTransformOp` carries out an affine transformation on the pixels. For example, here is how you can rotate an image about its center:

```java
AffineTransform transform = AffineTransform.getRotateInstance(Math.toRadians(angle),
    image.getWidth() / 2, image.getHeight() / 2);
var op = new AffineTransformOp(transform, interpolation);
op.filter(image, filteredImage);
```

The `AffineTransformOp` constructor requires an affine transform and an interpolation strategy. Interpolation is necessary to determine the target image pixels if the source pixels are transformed somewhere between target pixels. For example, if you rotate source pixels, they will generally not fall exactly onto target pixels. There are three interpolation strategies: `AffineTransformOp.TYPE_BICUBIC`, `AffineTransformOp.TYPE_BILINEAR`, and `AffineTransformOp.TYPE_NEAREST_NEIGHBOR`. Bicubic interpolation takes a bit longer but looks better than the other two.

The program in Listing 11.22 lets you rotate an image by 5 degrees (see Figure 11.57).

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_786_0.png)

**Figure 11.57** A rotated image

The `RescaleOp` carries out a rescaling operation

$$x_{new} = a \cdot x + b$$

for each of the color components in the image. (Alpha components are not affected.) The effect of rescaling with `a > 1` is to brighten the image. Construct the `RescaleOp` by specifying the scaling parameters and optional rendering hints. In Listing 11.22, we use:

```java
float a = 1.1f;
float b = 20.0f;
var op = new RescaleOp(a, b, null);
```

You can also supply separate scaling values for each color component—see the API notes.

The `LookupOp` operation lets you specify an arbitrary mapping of sample values. Supply a table that specifies how each value should be mapped. In the example program, we compute the *negative* of all colors, changing the color `c` to `255 - c`.

The `LookupOp` constructor requires an object of type `LookupTable` and a map of optional hints. The `LookupTable` class is abstract, with two concrete subclasses: `ByteLookupTable` and `ShortLookupTable`. Since RGB color values are bytes, a `ByteLookupTable` should suffice. However, because of the bug described in http://bugs.sun.com/bugdatabase/view_bug.do?bug_id=4818321, we will use a `ShortLookupTable` instead. Here is how we construct the `LookupOp` for the example program:

```java
var negative = new short[256];
for (int i = 0; i < 256; i++) negative[i] = (short) (255 - i);
var table = new ShortLookupTable(0, negative);
var op = new LookupOp(table, null);
```

The lookup is applied to each color component separately, but not to the alpha component. You can also supply different lookup tables for each color component—see the API notes.

> **NOTE:** You cannot apply a `LookupOp` to an image with an indexed color model. (In those images, each sample value is an offset into a color palette.)

The `ColorConvertOp` is useful for color space conversions. We do not discuss it here.

The most powerful of the transformations is the `ConvolveOp`, which carries out a mathematical *convolution*. We won't get too deeply into the mathematical details, but the basic idea is simple. Consider, for example, the *blur filter* (see Figure 11.58).

The blurring is achieved by replacing each pixel with the *average* value from the pixel and its eight neighbors. Intuitively, it makes sense why this operation would blur out the picture.

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_788_0.png)

**Figure 11.58** Blurring an image

Mathematically, the averaging can be expressed as a convolution operation with the following *kernel*:

$$\begin{bmatrix} 1/9 & 1/9 & 1/9 \\ 1/9 & 1/9 & 1/9 \\ 1/9 & 1/9 & 1/9 \end{bmatrix}$$

The kernel of a convolution is a matrix that tells what weights should be applied to the neighboring values. The kernel above produces a blurred image. A different kernel carries out *edge detection*, locating the areas of color changes:

$$\begin{bmatrix} 0 & -1 & 0 \\ -1 & 4 & -1 \\ 0 & -1 & 0 \end{bmatrix}$$

Edge detection is an important technique for analyzing photographic images (see Figure 11.59).

To construct a convolution operation, first set up an array of the values for the kernel and construct a Kernel object. Then, construct a ConvolveOp object from the kernel and use it for filtering.

```java
float[] elements =
{
    0.0f, -1.0f, 0.0f,
   -1.0f,  4.0f, -1.0f,
    0.0f, -1.0f, 0.0f
};
```

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_789_0.png)

**Figure 11.59** Edge detection and inversion

```java
var kernel = new Kernel(3, 3, elements);
var op = new ConvolveOp(kernel);
op.filter(image, filteredImage);
```

The program in Listing 11.22 allows a user to load a GIF or JPEG image and carry out the image manipulations that we discussed. Thanks to the power of the operations provided by Java 2D API, the program is very simple.

**Listing 11.22** `ImageProcessing/ImageProcessingFrame.java`

```java
package imageProcessing;

import java.awt.*;
import java.awt.event.*;
import java.awt.image.*;
import java.io.*;

import javax.imageio.*;
import javax.swing.*;
import javax.swing.filechooser.*;

/**
 * This frame has a menu to load an image and to specify various transformations, and a
 * component to show the resulting image.
 */
public class ImageProcessingFrame extends JFrame
{
   private static final int DEFAULT_WIDTH = 400;
   private static final int DEFAULT_HEIGHT = 400;

   private BufferedImage image;

   public ImageProcessingFrame()
   {
      setTitle("ImageProcessingTest");
      setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);

      add(new JComponent()
         {
            public void paintComponent(Graphics g)
            {
               if (image != null) g.drawImage(image, 0, 0, null);
            }
         });

      var fileMenu = new JMenu("File");
      var openItem = new JMenuItem("Open");
      openItem.addActionListener(event -> openFile());
      fileMenu.add(openItem);

      var exitItem = new JMenuItem("Exit");
      exitItem.addActionListener(event -> System.exit(0));
      fileMenu.add(exitItem);

      var editMenu = new JMenu("Edit");
      var blurItem = new JMenuItem("Blur");
      blurItem.addActionListener(event ->
         {
            float weight = 1. / 9.0f;
            float[] elements = new float[9];
            for (int i = 0; i < 9; i++)
               elements[i] = weight;
            convolve(elements);
         });
      editMenu.add(blurItem);

      var sharpenItem = new JMenuItem("Sharpen");
      sharpenItem.addActionListener(event ->
         {
            float[] elements = { 0.0f, -1.0f, 0.0f, -1.0f, 5.f, -1.0f, 0.0f, -1.0f, 0.0f };
            convolve(elements);
         });
      editMenu.add(sharpenItem);
```
