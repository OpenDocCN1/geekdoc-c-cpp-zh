```
```java
IIOImage image = new IIOImage(images[i], null, null);
if (writer.canInsertImage()) writer.writeInsert(i, image, null);
}
}
} catch (IOException e)
{
    JOptionPane.showMessageDialog(this, e);
}
}

/**
 * Gets a set of "preferred" format names of all image writers. The preferred format name is
 * the first format name that a writer specifies.
 * @return the format name set
 */
public static Set<String> getWriterFormats()
{
    Set<String> writerFormats = new TreeSet<>();
    Set<String> formatNames = new TreeSet<>();
    formatNames.addAll(Arrays.asList(ImageIO.getWriterFormatNames()));
    while (formatNames.size() > 0)
    {
        String name = formatNames.iterator().next();
        Iterator<ImageWriter> iter = ImageIO.getImageWritersByFormatName(name);
        ImageWriter writer = iter.next();
        String[] names = writer.getOriginatingProvider().getFormatNames();
        String format = names[0];
        if (format.equals(format.toLowerCase())) format = format.toUpperCase();
        writerFormats.add(format);
        formatNames.removeAll(Arrays.asList(names));
    }
    return writerFormats;
}
```
```

| javax.imageio.ImageIO 1.4 |
|---|
| • `static BufferedImage read(File input)`<br>• `static BufferedImage read(InputStream input)`<br>• `static BufferedImage read(URL input)`<br>&nbsp;&nbsp;reads an image from an input.<br>• `static boolean write(RenderedImage image, String formatName, File output)`<br>• `static boolean write(RenderedImage image, String formatName, OutputStream output)`<br>&nbsp;&nbsp;writes an image in the given format to output. Returns false if no appropriate writer was found. |