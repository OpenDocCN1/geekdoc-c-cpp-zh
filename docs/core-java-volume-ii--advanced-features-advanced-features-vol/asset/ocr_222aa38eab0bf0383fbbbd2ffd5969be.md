> **CAUTION:** There are also setPixel methods that take array parameters of types `float[]` and `double[]`. However, the values that you need to place into these arrays are **not** normalized color values between `0.0` and `1.0`.

```
float[] red = { 1.0F, 0.0F, 0.0F, 1.0F };
raster.setPixel(i, red); // ERROR
```

You need to supply values between 0 and 255, no matter what the type of the array is.

You can supply a batch of pixels with the setPixels method. Specify the starting pixel position and the width and height of the rectangle that you want to set. Then, supply an array that contains the sample values for all pixels. For example, if your buffered image has a type of `TYPE_INT_ARGB`, supply the red, green, blue, and alpha values of the first pixel, and then the red, green, blue, and alpha values for the second pixel.

```
var pixels = new int[4 * width * height];
pixels[0] = . . .; // red value for first pixel
pixels[1] = . . .; // green value for first pixel
pixels[2] = . . .; // blue value for first pixel
pixels[3] = . . .; // alpha value for first pixel
...
raster.setPixels(x, y, width, height, pixels);
```

Conversely, to read a pixel, use the getPixel method. Supply an array of four integers to hold the sample values.

```
var sample = new int[4];
raster.getPixel(x, y, sample);
var color = new Color(sample[0], sample[1], sample[2], sample[3]);
```

You can read multiple pixels with the getPixels method.

```
raster.getPixels(x, y, width, height, samples);
```

If you use an image type other than `TYPE_INT_ARGB` and you know how that type represents pixel values, you can still use the getPixel/setPixel methods. However, you have to know the encoding of the sample values in the particular image type.

If you need to manipulate an image with an arbitrary, unknown image type, then you have to work a bit harder. Every image type has a color model that can translate between sample value arrays and the standard RGB color model.