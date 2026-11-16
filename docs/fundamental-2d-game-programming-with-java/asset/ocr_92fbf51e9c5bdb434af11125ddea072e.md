```
```java
do {
    w = (int)(w * 1.5);
    if (w > targetWidth) {
        w = targetWidth;
    }
    h = (int)(h * 1.5);
    if (h > targetHeight) {
        h = targetHeight;
    }
}
BufferedImage tmp =
    new BufferedImage(w, h, BufferedImage.TYPE_INT_ARGB);
Graphics2D g2d = tmp.createGraphics();
g2d.setRenderingHint(RenderingHints.KEY_INTERPOLATION, hintValue);
g2d.drawImage(ret, 0, 0, w, h, null);
g2d.dispose();
ret = tmp;
} while (w != targetWidth || h != targetHeight);
return ret;
}

private ImageConsumer getConsumer() {
    return new ImageConsumer() {
        public void setProperties(Hashtable<?, ?> props) { }
        public void setPixels(int x, int y, int w, int h, ColorModel model,
            int[] pixels, int off, int scansize) { }
        public void setPixels(int x, int y, int w, int h, ColorModel model,
            byte[] pixels, int off, int scansize) { }
        public void setHints(int intflags) { }
        public void setDimensions(int width, int height) { }
        public void setColorModel(ColorModel model) { }
        public void imageComplete(int status) { }
    };
}

public static void main(String[] args) {
    launchApp(new ScaleUpImageExample());
}
```
```

# RESOURCES AND FURTHER READING

Campbell, Chris, “Java 2D Trickery: Antialiased Image Transforms,” 2007, https://weblogs.java.net/blog/campbell/archive/2007/03/java_2d_tricker.html.