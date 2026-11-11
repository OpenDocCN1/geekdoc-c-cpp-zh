| `javax.imageio.ImageReader` | **1.4** |
|---|---|
| • `void setInput(Object input)`<br>• `void setInput(Object input, boolean seekForwardOnly)` | sets the input source of the reader.<br><br>**Parameters:**<br>`input` — An ImageInputStream object or another object that this reader can accept.<br>`seekForwardOnly` — true if the reader should read forward only. By default, the reader uses random access and, if necessary, buffers image data. |
| • `BufferedImage read(int index)` | reads the image with the given image index (starting at 0). Throws an `IndexOutOfBoundsException` if no such image is available. |
| • `int getNumImages(boolean allowSearch)` | gets the number of images in this reader. If `allowSearch` is false and the number of images cannot be determined without reading forward, then -1 is returned. If `allowSearch` is true and the reader is in the “seek forward only” mode, then an `IllegalStateException` is thrown. |
| • `int getNumThumbnails(int index)` | gets the number of thumbnails of the image with the given index. |
| • `BufferedImage readThumbnail(int index, int thumbnailIndex)` | gets the thumbnail with the given `thumbnailIndex` of the image with the given index. |
| • `int getWidth(int index)`<br>• `int getHeight(int index)` | gets the image width and height. Throws an `IndexOutOfBoundsException` if no such image is available. |
| • `ImageReaderSpi getOriginatingProvider()` | gets the service provider that constructed this reader. |

| `javax.imageio.spi.IIOServiceProvider` | **1.4** |
|---|---|
| • `String getVendorName()`<br>• `String getVersion()` | gets the vendor name and version of this service provider. |