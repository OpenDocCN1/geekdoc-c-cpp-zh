```
AlphaComposite.SRC_OUT,
AlphaComposite.DST_OUT,
AlphaComposite.SRC_OVER,
AlphaComposite.DST_OVER,
AlphaComposite.SRC_ATOP,
AlphaComposite.DST_ATOP,
AlphaComposite.XOR,
AlphaComposite.CLEAR,
});
```

```
private int compositeIndex;
private float srcAlpha;
private float dstAlpha;
private float extAlpha;
private BufferedImage sprite;
private BufferedImage sourceImage;
private BufferedImage destinationImage;
public AlphaCompositeExample() {
appBackground = Color.DARK_GRAY;
appWidth = 640;
appHeight = 480;
appSleep = 10L;
appTitle = "Alpha Composite Example";
}
```

```
@Override
protected void initialize() {
super.initialize();
srcAlpha = 1.0f;
dstAlpha = 1.0f;
extAlpha = 1.0f;
destinationImage =
new BufferedImage(320, 320, BufferedImage.TYPE_INT_ARGB);
sourceImage =
new BufferedImage(320, 320, BufferedImage.TYPE_INT_ARGB);
sprite = new BufferedImage(320, 320, BufferedImage.TYPE_INT_ARGB);
createImages();
}
```

```
private void createImages() {
// source image
Graphics2D g2d = sourceImage.createGraphics();
g2d.setComposite(AlphaComposite.getInstance(AlphaComposite.CLEAR));
g2d.fillRect(0, 0, sourceImage.getWidth(), sourceImage.getHeight());
```