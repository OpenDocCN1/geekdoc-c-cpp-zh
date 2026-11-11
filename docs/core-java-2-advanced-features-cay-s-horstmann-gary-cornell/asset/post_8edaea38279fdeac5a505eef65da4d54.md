
## Listing 11.8 rasterImage/RasterImageFrame.java

```java
package rasterImage;

import java.awt.*;
import java.awt.image.*;
import javax.swing.*;

/**
 * This frame shows an image with a Mandelbrot set.
 */
public class RasterImageFrame extends JFrame
{
    private static final double XMIN = -2;
    private static final double XMAX = 2;
    private static final double YMIN = -2;
    private static final double YMAX = 2;
    private static final int MAX_ITERATIONS = 16;
    private static final int IMAGE_WIDTH = 400;
    private static final int IMAGE_HEIGHT = 400;

    public RasterImageFrame()
    {
        BufferedImage image = makeMandelbrot(IMAGE_WIDTH, IMAGE_HEIGHT);
        add(new JLabel(new ImageIcon(image)));
        pack();
    }

    /**
     * Makes the Mandelbrot image.
     * @param width the width
     * @param height the height
     * @return the image
     */
    public BufferedImage makeMandelbrot(int width, int height)
    {
        BufferedImage image = new BufferedImage(width, height, BufferedImage.TYPE_INT_ARGB);
        WritableRaster raster = image.getRaster();
        ColorModel model = image.getColorModel();

        Color fractalColor = Color.red;
        int argb = fractalColor.getRGB();
        Object colorData = model.getDataElements(argb, null);

        for (int i = 0; i < width; i++)
            for (int j = 0; j < height; j++)
            {
                double a = XMIN + i * (XMAX - XMIN) / width;
                double b = YMIN + j * (YMAX - YMIN) / height;
                if (escapesToInfinity(a, b)) raster.setDataElements(i, j, colorData);
            }
        return image;
    }

    private boolean escapesToInfinity(double a, double b)
    {
        double x = 0.0;
        double y = 0.0;
        int iterations = 0;
        while (x <= 2 && y <= 2 && iterations < MAX_ITERATIONS)
        {
            double xnew = x * x - y * y + a;
            double ynew = 2 * x * y + b;
            x = xnew;
            y = ynew;
            iterations++;
        }
        return x > 2 || y > 2;
    }
}
```

### `java.awt.image.BufferedImage` 1.2

- **BufferedImage(int width, int height, int imageType)**  
  constructs a buffered image object.

  *Parameters:*  
  `width, height` — The image dimensions  
  `imageType` — The image type. The most common types are `TYPE_INT_RGB`, `TYPE_INT_ARGB`, `TYPE_BYTE_GRAY`, and `TYPE_BYTE_INDEXED`.

- **ColorModel getColorModel()**  
  returns the color model of this buffered image.

- **WritableRaster getRaster()**  
  gets the raster for accessing and modifying pixels of this buffered image.

### `java.awt.image.Raster` 1.2

| Method | Description |
|---|---|
| `Object getDataElements(int x, int y, Object data)` | returns the sample data for a raster point, in an array whose element type and length depend on the color model. If data is not null, it is assumed to be an array that is appropriate for holding sample data, and it is filled. If data is null, a new array is allocated. Its element type and length depend on the color model. |
| `int[] getPixel(int x, int y, int[] sampleValues)` |  |
| `float[] getPixel(int x, int y, float[] sampleValues)` |  |
| `double[] getPixel(int x, int y, double[] sampleValues)` |  |
| `int[] getPixels(int x, int y, int width, int height, int[] sampleValues)` |  |
| `float[] getPixels(int x, int y, int width, int height, float[] sampleValues)` |  |
| `double[] getPixels(int x, int y, int width, int height, double[] sampleValues)` | returns the sample values for a raster point, or a rectangle of raster points, in an array whose length depends on the color model. If sampleValues is not null, it is assumed to be sufficiently long for holding the sample values, and it is filled. If sampleValues is null, a new array is allocated. These methods are only useful if you know the meaning of the sample values for a color model. |

### `java.awt.image.WritableRaster` 1.2

| Method | Description |
|---|---|
| `void setDataElements(int x, int y, Object data)` | sets the sample data for a raster point. data is an array filled with the sample data for a pixel. Its element type and length depend on the color model. |
| `void setPixel(int x, int y, int[] sampleValues)` |  |
| `void setPixel(int x, int y, float[] sampleValues)` |  |
| `void setPixel(int x, int y, double[] sampleValues)` |  |
| `void setPixels(int x, int y, int width, int height, int[] sampleValues)` |  |
| `void setPixels(int x, int y, int width, int height, float[] sampleValues)` |  |
| `void setPixels(int x, int y, int width, int height, double[] sampleValues)` | sets the sample values for a raster point or a rectangle of raster points. These methods are only useful if you know the encoding of the sample values for a color model. |

### `java.awt.image.ColorModel` 1.2

| Method | Description |
|---|---|
| `int getRGB(Object data)` | returns the ARGB value that corresponds to the sample data passed in the data array. Its element type and length depend on the color model. |
| `Object getDataElements(int argb, Object data)` | returns the sample data for a color value. If data is not null, it is assumed to be an array that is appropriate for holding sample data, and it is filled. If data is null, a new array is allocated. data is an array filled with the sample data for a pixel. Its element type and length depend on the color model. |

### `java.awt.Color` 1.0

| Method | Description |
|---|---|
| `Color(int argb, boolean hasAlpha)` 1.2 | creates a color with the specified combined ARGB value if hasAlpha is true, or the specified RGB value if hasAlpha is false. |
| `int getRGB()` | returns the ARGB color value corresponding to this color. |

## 11.11.2 Filtering Images

In the preceding section, you saw how to build up an image from scratch. However, often you want to access image data for a different reason: You already have an image and you want to improve it in some way.

Of course, you can use the getPixel/getDataElements methods that you saw in the preceding section to read the image data, manipulate them, and write them back. But fortunately, the Java 2D API already supplies a number of filters that carry out common image processing operations for you.

The image manipulations all implement the `BufferedImageOp` interface. After you construct the operation, you simply call the filter method to transform an image into another.

```java
BufferedImage op = ...;
BufferedImage filteredImage =
    new BufferedImage(image.getWidth(), image.getHeight(), image.getType());
op.filter(image, filteredImage);
```

Some operations can transform an image in place (op.filter(image, image)), but most can’t.

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
AffineTransformOp op = new AffineTransformOp(transform, interpolation);
op.filter(image, filteredImage);
```

The `AffineTransformOp` constructor requires an affine transform and an *interpolation* strategy. Interpolation is necessary to determine pixels in the target image if the source pixels are transformed somewhere between target pixels. For example, if you rotate source pixels, then they will generally not fall exactly onto target pixels. There are two interpolation strategies: `AffineTransformOp.TYPE_BILINEAR` and `AffineTransformOp.TYPE_NEAREST_NEIGHBOR`. Bilinear interpolation takes a bit longer but looks better.

The program in Listing 11.9 lets you rotate an image by 5 degrees (see Figure 11.29).

![](img/7dd923a566750151a3aab0dacd0cdaa5_863_0.png)

**Figure 11.29** A rotated image

The `RescaleOp` carries out a rescaling operation $x_{\mathrm{new}} = a \cdot x + b$ for each of the color components in the image. (Alpha components are not affected.) The effect of rescaling with a > 1 is to brighten the image. Construct the `RescaleOp` by specifying the scaling parameters and optional rendering hints. In Listing 11.9, we use:

```java
float a = 1.1f;
float b = 20.0f;
RescaleOp op = new RescaleOp(a, b, null);
```

You can also supply separate scaling values for each color component—see the API notes.

The `LookupOp` operation lets you specify an arbitrary mapping of sample values. Supply a table that specifies how each value should be mapped. In the example program, we compute the negative of all colors, changing the color c to 255 − c.

The `LookupOp` constructor requires an object of type `LookupTable` and a map of optional hints. The `LookupTable` class is abstract, with two concrete subclasses: `ByteLookupTable` and `ShortLookupTable`. Since RGB color values are bytes, a `ByteLookupTable` should suffice. However, because of the bug described in http://bugs.sun.com/bugdatabase/view_bug.do?bug_id=6183251, we will use a `ShortLookupTable` instead. Here is how we construct the `LookupOp` for the example program:

```java
short negative[] = new short[256];
for (int i = 0; i < 256; i++) negative[i] = (short) (255 - i);
ShortLookupTable table = new ShortLookupTable(0, negative);
LookupOp op = new LookupOp(table, null);
```

The lookup is applied to each color component separately, but not to the alpha component. You can also supply different lookup tables for each color component—see the API notes.

> **NOTE:** You cannot apply a `LookupOp` to an image with an indexed color model.
> (In those images, each sample value is an offset into a color palette.)

The `ColorConvertOp` is useful for color space conversions. We do not discuss it here.

The most powerful of the transformations is the `ConvolveOp`, which carries out a mathematical convolution. We won’t get too deeply into the mathematical details, but the basic idea is simple. Consider, for example, the blur filter (see Figure 11.30).

The blurring is achieved by replacing each pixel with the average value from the pixel and its eight neighbors. Intuitively, it makes sense why this operation would blur out the picture. Mathematically, the averaging can be expressed as a convolution operation with the following kernel:
