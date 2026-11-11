
![](img/7dd923a566750151a3aab0dacd0cdaa5_865_0.png)

**Figure 11.30** Blurring an image

$$
\begin{bmatrix}
1/9 & 1/9 & 1/9 \\
1/9 & 1/9 & 1/9 \\
1/9 & 1/9 & 1/9
\end{bmatrix}
$$

The kernel of a convolution is a matrix that tells what weights should be applied to the neighboring values. The kernel above produces a blurred image. A different kernel carries out *edge detection*, locating the areas of color changes:

$$
\begin{bmatrix}
0 & -1 & 0 \\
-1 & 4 & -1 \\
0 & -1 & 0
\end{bmatrix}
$$

Edge detection is an important technique for analyzing photographic images (see Figure 11.31).

To construct a convolution operation, first set up an array of the values for the kernel and construct a `Kernel` object. Then, construct a `ConvolveOp` object from the kernel and use it for filtering.

```java
float[] elements =
{
   0.0f, -1.0f, 0.0f,
   -1.0f, 4.0f, -1.0f,
   0.0f, -1.0f, 0.0f
};
Kernel kernel = new Kernel(3, 3, elements);
ConvolveOp op = new ConvolveOp(kernel);
op.filter(image, filteredImage);
```

![](img/7dd923a566750151a3aab0dacd0cdaa5_866_0.png)

Figure 11.31 Edge detection and inversion

The program in Listing 11.9 allows a user to load in a GIF or JPEG image and carry out the image manipulations that we discussed. Thanks to the power of the operations provided by Java 2D API, the program is very simple.

### Listing 11.9 imageProcessing/ImageProcessingFrame.java

```java
1 package imageProcessing;
2
3 import java.awt.*;
4 import java.awt.geom.*;
5 import java.awt.image.*;
6 import java.io.*;
7
8 import javax.imageio.*;
9 import javax.swing.*;
10 import javax.swing.filechooser.*;
11
12 /**
13  * This frame has a menu to load an image and to specify various transformations, and a component
14  * to show the resulting image.
15  */
16 public class ImageProcessingFrame extends JFrame
17 {
18    private static final int DEFAULT_WIDTH = 400;
19    private static final int DEFAULT_HEIGHT = 400;
20
21    private BufferedImage image;
22
23    public ImageProcessingFrame()
24    {
JMenuItem edgeDetectItem = new JMenuItem("Edge detect");
edgeDetectItem.addActionListener(event ->
{
    float[] elements = { 0.0f, -1.0f, 0.0f, -1.0f, 4.0f, -1.0f, 0.0f, -1.0f, 0.0f };
    convolve(elements);
});
editMenu.add(edgeDetectItem);

JMenuItem negativeItem = new JMenuItem("Negative");
negativeItem.addActionListener(event ->
{
    short[] negative = new short[256];
    for (int i = 0; i < 256; i++)
        negative[i] = (short) (255 - i);
    ShortLookupTable table = new ShortLookupTable(0, negative);
    LookupOp op = new LookupOp(table, null);
    filter(op);
});
editMenu.add(negativeItem);

JMenuItem rotateItem = new JMenuItem("Rotate");
rotateItem.addActionListener(event ->
{
    if (image == null) return;
    AffineTransform transform = AffineTransform.getRotateInstance(Math.toRadians(5),
        image.getWidth() / 2, image.getHeight() / 2);
    AffineTransformOp op = new AffineTransformOp(transform,
        AffineTransformOp.TYPE_BICUBIC);
    filter(op);
});
editMenu.add(rotateItem);

JMenuBar menuBar = new JMenuBar();
menuBar.add(fileMenu);
menuBar.add(editMenu);
setJMenuBar(menuBar);
}

/**
 * Open a file and load the image.
 */
public void openFile()
{
   JFileChooser chooser = new JFileChooser("");
   chooser.setCurrentDirectory(new File(getClass().getPackage().getName()));
   String[] extensions = ImageIO.getReaderFileSuffixes();
   chooser.setFileFilter(new FileNameExtensionFilter("Image files", extensions));
   int r = chooser.showOpenDialog(this);
   if (r != JFileChooser.APPROVE_OPTION) return;

   try
   {
      Image img = ImageIO.read(chooser.getSelectedFile());
      image = new BufferedImage(img.getWidth(null), img.getHeight(null),
         BufferedImage.TYPE_INT_RGB);
      image.getGraphics().drawImage(img, 0, 0, null);
   }
   catch (IOException e)
   {
      JOptionPane.showMessageDialog(this, e);
   }
   repaint();
}

/**
 * Apply a filter and repaint.
 * @param op the image operation to apply
 */
private void filter(BufferedImageOp op)
{
   if (image == null) return;
   image = op.filter(image, null);
   repaint();
}

/**
 * Apply a convolution and repaint.
 * @param elements the convolution kernel (an array of 9 matrix elements)
 */
private void convolve(float[] elements)
{
   Kernel kernel = new Kernel(3, 3, elements);
   ConvolveOp op = new ConvolveOp(kernel);
   filter(op);
}
```

### java.awt.image.BufferedImageOp 1.2

- `BufferedImage filter(BufferedImage source, BufferedImage dest)`
  applies the image operation to the source image and stores the result in the destination image. If dest is null, a new destination image is created. The destination image is returned.

### java.awt.image.AffineTransformOp 1.2

- `AffineTransformOp(AffineTransform t, int interpolationType)`
  constructs an affine transform operator. The interpolation type is one of TYPE_BILINEAR, TYPE_BICUBIC, or TYPE_NEAREST_NEIGHBOR.

### java.awt.image.RescaleOp 1.2

- `RescaleOp(float a, float b, RenderingHints hints)`
- `RescaleOp(float[] as, float[] bs, RenderingHints hints)`

  constructs a rescale operator that carries out the scaling operation x_new = a · x + b. When using the first constructor, all color components (but not the alpha component) are scaled with the same coefficients. When using the second constructor, you supply either the values for each color component, in which case the alpha component is unaffected, or the values for both alpha and color components.

### java.awt.image.LookupOp 1.2

- `LookupOp(LookupTable table, RenderingHints hints)`
  constructs a lookup operator for the given lookup table.

### java.awt.image.ByteLookupTable 1.2

- `ByteLookupTable(int offset, byte[] data)`
- `ByteLookupTable(int offset, byte[][] data)`

  constructs a lookup table for converting byte values. The offset is subtracted from the input before the lookup. The values in the first constructor are applied to all color components but not the alpha component. When using the second constructor, you supply either the values for each color component, in which case the alpha component is unaffected, or the values for both alpha and color components.

### java.awt.image.ShortLookupTable 1.2

- `ShortLookupTable(int offset, short[] data)`
- `ShortLookupTable(int offset, short[][] data)`

  Constructs a lookup table for converting short values. The offset is subtracted from the input before the lookup. The values in the first constructor are applied to all color components but not the alpha component. When using the second constructor, you supply either the values for each color component, in which case the alpha component is unaffected, or the values for both alpha and color components.

### java.awt.image.ConvolveOp 1.2

- `ConvolveOp(Kernel kernel)`
- `ConvolveOp(Kernel kernel, int edgeCondition, RenderingHints hints)`

  Constructs a convolution operator. The edge condition specified is one of `EDGE_NO_OP` and `EDGE_ZERO_FILL`. Edge values need to be treated specially because they don’t have sufficient neighboring values to compute the convolution. The default is `EDGE_ZERO_FILL`.

### java.awt.image.Kernel 1.2

- `Kernel(int width, int height, float[] matrixElements)`

  Constructs a kernel for the given matrix.

## 11.12 Printing

The original JDK had no support for printing at all. It was not possible to print from applets, and you had to get a third-party library if you wanted to print from an application. JDK 1.1 introduced very lightweight printing support, just enough to produce simple printouts, as long as you were not too particular about the print quality. The 1.1 printing model was designed to allow browser vendors to print the surface of an applet as it appears on a web page (which, however, the browser vendors have not embraced).

Java SE 1.2 introduced the beginnings of a robust printing model that is fully integrated with 2D graphics. Java SE 1.4 added important enhancements, such as discovery of printer features and streaming print jobs for server-side print management.
