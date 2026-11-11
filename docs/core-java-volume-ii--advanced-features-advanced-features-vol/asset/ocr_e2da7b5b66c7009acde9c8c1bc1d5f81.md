you want to work with a “raster” of color data. The following sections show you how to process raster images in Java.

# 11.4.1 Readers and Writers for Images

The `javax.imageio` package contains out-of-the-box support for reading and writing several common file formats, as well as a framework that enables third parties to add readers and writers for other formats. The GIF, JPEG, PNG, BMP (Windows bitmap), and WBMP (wireless bitmap) file formats are supported.

The basics of the library are extremely straightforward. To load an image, use the static `read` method of the `ImageIO` class:

```
File f = ...;
BufferedImage image = ImageIO.read(f);
```

The `ImageIO` class picks an appropriate reader, based on the file type. It may consult the file extension and the “magic number” at the beginning of the file for that purpose. If no suitable reader can be found or the reader can’t decode the file contents, the read method returns null.

Writing an image to a file is just as simple:

```
File f = ...;
String format = ...;
ImageIO.write(image, format, f);
```

Here the format string is a string identifying the image format, such as "JPEG" or "PNG". The `ImageIO` class picks an appropriate writer and saves the file.

# 11.4.1.1 Obtaining Readers and Writers for Image File Types

For more advanced image reading and writing operations that go beyond the static read and write methods of the `ImageIO` class, you first need to get the appropriate `ImageReader` and `ImageWriter` objects. The `ImageIO` class enumerates readers and writers that match one of the following:

+   - An image format (such as "JPEG")
+   - A file suffix (such as "jpg")
+   - A MIME type (such as "image/jpeg")

> **NOTE:** MIME is the Multipurpose Internet Mail Extensions standard. The MIME standard defines common data formats such as `image/jpeg` and `application/pdf`.