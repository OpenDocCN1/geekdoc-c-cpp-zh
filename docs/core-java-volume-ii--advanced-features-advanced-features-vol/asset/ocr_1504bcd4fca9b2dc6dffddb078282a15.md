For example, you can obtain a reader that reads JPEG files as follows:

```
```java
ImageReader reader = null;
Iterator<ImageReader> iter = ImageIO.getImageReadersByFormatName("JPEG");
if (iter.hasNext()) reader = iter.next();
```
```

The getImageReadersBySuffix and getImageReadersByMIMEType methods enumerate readers that match a file extension or MIME type.

It is possible that the ImageIO class can locate multiple readers that can all read a particular image type. In that case, you have to pick one of them, but it isn't clear how you can decide which one is the best. To find out more information about a reader, obtain its *service provider interface*:

```
```java
ImageReaderSpi spi = reader.getOriginatingProvider();
```
```

Then you can get the vendor name and version number:

```
```java
String vendor = spi.getVendor();
String version = spi.getVersion();
```
```

Perhaps that information can help you decide among the choices—or you might just present a list of readers to your program users and let them choose. For now, we assume that the first enumerated reader is adequate.

In the sample program in Listing 11.20, we want to find all file suffixes of all available readers so that we can use them in a file filter. Use the static ImageIO.getReaderFileSuffixes method for this purpose:

```
```java
String[] extensions = ImageIO.getReaderFileSuffixes();
chooser.setFileFilter(new FileNameExtensionFilter("Image files", extensions));
```
```

For saving files, we have to work harder. We'd like to present the user with a menu of all supported image types. Unfortunately, the getWriterFormatNames of the ImageIO class returns a rather curious list with redundant names, such as

```
```
jpg, BMP, bmp, JPG, jpeg, wbmp, png, JPEG, PNG, WBMP, GIF, gif
```
```

That's not something one would want to present in a menu. What is needed is a list of “preferred” format names. We supply a helper method getWriterFormats for this purpose (see Listing 11.20). We look up the first writer associated with each format name. Then we ask it what its format names are, in the hope that it will list the most popular one first. Indeed, for the JPEG writer, this works fine—it lists "JPEG" before the other options. (The PNG writer, on the other hand, lists "png" in lower case before "PNG". We hope this behavior will be addressed at some point in the future. For now, we force all-lowercase names to upper case.) Once we pick a preferred name, we remove all alternate names from the original set. We keep going until all format names are handled.