It turns out that if $x$ or $y$ ever gets larger than 2, then the sequence escapes to infinity. Only the pixels that correspond to points $(a, b)$ leading to a bounded sequence are colored. (The formulas for the number sequences come ultimately from the mathematics of complex numbers; we’ll just take them for granted.)

Listing 11.21 shows the code. In this program, we demonstrate how to use the `ColorModel` class for translating Color values into pixel data. That process is independent of the image type. Just for fun, change the color type of the buffered image to `TYPE_BYTE_GRAY`. You don’t need to change any other code—the color model of the image automatically takes care of the conversion from colors to sample values.

# Listing 11.21 `rasterImage/RasterImageFrame.java`

```
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
   private static final int IMAGE_ITERATIONS = 16;
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
```