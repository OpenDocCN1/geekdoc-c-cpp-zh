
```java
private boolean realtime = true;
private boolean bufferedImage = true;
public ImageSpeedTest() {
    appWidth = 640;
    appHeight = 640;
    appSleep = 0L;
    appTitle = "Image Speed Test";
}

@Override
protected void initialize() {
    super.initialize();
    GraphicsEnvironment ge = GraphicsEnvironment
        .getLocalGraphicsEnvironment();
    GraphicsDevice gd = ge.getDefaultScreenDevice();
    gc = gd.getDefaultConfiguration();
    bi = gc.createCompatibleImage( appWidth, appHeight );
    createVolatileImage();
    renderToBufferedImage();
}

@Override
protected void processInput( float delta ) {
    super.processInput( delta );
    if( keyboard.keyDownOnce( KeyEvent.VK_B ) ) {
        bufferedImage = !bufferedImage;
    }
    if( keyboard.keyDownOnce( KeyEvent.VK_R ) ) {
        realtime = !realtime;
    }
}

private void createVolatileImage() {
    if( vi != null ) {
        vi.flush();
        vi = null;
    }
    vi = gc.createCompatibleVolatileImage( getWidth(), getHeight() );
}

@Override
protected void render( Graphics g ) {
    if( bufferedImage ) {
        renderToBufferedImage( g );
    } else if( realtime ) {
        renderToVolatileImageEveryFrame( g );
    } else {
        renderToVolatileImage( g );
    }
    super.render( g );
    // spit out help
    g.drawString( "(B)ffered Image: " + bufferedImage, 20, 35 );
    g.drawString( "(R)eal Time Rendering: " + realtime, 20, 65 );
}

private void renderToVolatileImage( Graphics g ) {
    do {
        int returnCode = vi.validate( gc );
        if( returnCode == VolatileImage.IMAGE_RESTORED ) {
            // Contents need to be restored
            renderVolatileImage();
        } else if( returnCode == VolatileImage.IMAGE_INCOMPATIBLE ) {
            // incompatible GraphicsConfig
            createVolatileImage();
            renderVolatileImage();
        }
        g.drawImage( vi, 0, 0, null );
    } while( vi.contentsLost() );
}

private void renderToVolatileImageEveryFrame( Graphics g ) {
    do {
        int returnCode = vi.validate( gc );
        if( returnCode == VolatileImage.IMAGE_INCOMPATIBLE ) {
            // incompatible GraphicsConfig
            createVolatileImage();
        }
        renderVolatileImage();
        g.drawImage( vi, 0, 0, null );
    } while( vi.contentsLost() );
}

protected void renderVolatileImage() {
    Graphics2D g2d = vi.createGraphics();
    g2d.setColor( new Color( rand.nextInt() ) );
    g2d.fillRect( 0, 0, getWidth(), getHeight() );
    g2d.dispose();
}

private void renderToBufferedImage( Graphics g ) {
    if (realtime) {
        renderToBufferedImage();
    }
    g.drawImage( bi, 0, 0, null );
}

private void renderToCreatedImage() {
    Graphics2D g2d = bi.createGraphics();
    g2d.setColor( new Color( rand.nextInt() ) );
    g2d.fillRect( 0, 0, getWidth(), getHeight() );
    g2d.dispose();
}

public static void main( String[] args ) {
    launchApp( new ImageSpeedTest() );
}
}
```

## CREATING TRANSPARENT IMAGES

The TransparentImageExample, as seen in Figure 10.10 and located in the javagames.images package, creates an image with transparent pixels. Up until now, none of the images had any transparent pixels. For any kind of game sprite (sprite is used as a generic term for any image file drawn to the screen) that isn't a square, transparent pixels around the edges are necessary so that there are no borders around all the game objects.

![](img/588a4cda8f2acae94a7e1987bf99400d_294_0.png)

Figure 10.10
Transparent Image Example.
© 2014 Timothy Wright.

If all that is required to create an image with a transparent background, it is very easy. A newly created BufferedImage with a type supporting transparency is by default full of zeros, which means the whole image is transparent.

```java
BufferedImage img =
new BufferedImage( 256, 256, BufferedImage.TYPE_INT_ARGB );
```

The image created in the previous code snippet, which includes alpha values, defaults to a transparent background. The TransparentImageExample code creates a new BufferedImage in the initialize() method. Every even square is drawn white, leaving the other squares as transparent.

The updateObjects() method divides the drawing area into five parts. Each of the five bars is shaded by covering half of each bar with a light gray bar. These bars are shifted using the delta value so that the bars move toward the bottom of the screen. The shift value is reset once it is larger than the ribbon height.

The render() method divides the height into pieces and renders each strip, starting one strip before the top of the screen so the strips enter from the top. Finally, the transparent image is drawn over the top of the shifting bars. Because the background of the checkerboard image was transparent, the background can be seen underneath the image.

```java
package javagames.images;

import java.awt.*;
import java.awt.image.BufferedImage;
import javagames.util.SimpleFramework;

public class TransparentImageExample extends SimpleFramework {
    private BufferedImage img;
    private float shift;

    public TransparentImageExample() {
        appWidth = 400;
        appHeight = 300;
        appSleep = 10L;
        appTitle = "Transparent Image Example";
        appBackground = Color.DARK_GRAY;
    }

    @Override
    protected void initialize() {
        super.initialize();

        img = new BufferedImage( 256, 256, BufferedImage.TYPE_INT_ARGB );

        Graphics2D g2d = img.createGraphics();

        int w = 8;
        int h = 8;
        int dx = img.getWidth() / w;
        int dy = img.getHeight() / h;
        for (int i = 0; i < w; ++i) {
            for (int j = 0; j < h; ++j) {
                if ((i+j) % 2 == 0) {
                    g2d.setColor( Color.WHITE );
                    g2d.fillRect( i*dx, j*dy, dx, dy );
                }
            }
        }
        g2d.dispose();
    }

    @Override
    protected void updateObjects( float delta ) {
        super.updateObjects( delta );
        int ribbonHeight = canvas.getHeight() / 5;
        shift += delta * ribbonHeight;
        if ( shift > ribbonHeight ) {
            shift -= ribbonHeight;
        }
    }

    @Override
    protected void render( Graphics g ) {
        super.render( g );

        // draw shifting background
        int hx = canvas.getHeight() / 5;
        g.setColor( Color.LIGHT_GRAY );
        for (int i = -1; i < 5; ++i ) {
            g.fillRect( 0, (int)shift + hx * i, canvas.getWidth(), hx / 2 );
        }

        int x = ( canvas.getWidth() - img.getWidth() ) / 2;
        int y = ( canvas.getHeight() - img.getHeight() ) / 2;
        g.drawImage( img, x, y, null );
    }

    public static void main( String[] args ) {
        launchApp( new TransparentImageExample() );
    }
}
```

## USING THE ALPHA COMPOSITE RULES

In the previous example, the transparent image was drawn on top and the background was visible underneath. But that is not the only option. When the pixels in the source image and destination image have some transparency, there are many ways to blend them. The AlphaComposite contains many rules.

TIP

The Java Docs (see Class AlphaComposite, 2013 at http://docs.oracle.com/javase/7/docs/api/java/awt/AlphaComposite.html) do a great job of explaining the math involved.

The “Compositing Digital Images” paper goes into even greater detail (see T. Porter and T. Duff, “Compositing Digital Images,” SIGGRAPH, 1984, pp. 253–259; http://keithp.com/~keithp/porterduff/p253-porter.pdf).

The different blending operations are as follows:

- SRC—Source is copied to the destination.
- DEST—The destination is unchanged.
- SRC_IN—Only the source inside the destination is copied.
- DEST_IN—Only the destination inside the source is copied.
- SRC_OUT—The destination is replaced only by the outside source.
- DEST_OUT—Only the outside portion of the destination is copied.
- SRC_OVER—The source is copied over the destination.
- DEST_OVER—The destination is copied over the source.
- SRC_ATOP—The source inside the destination is copied onto the destination.
- DEST_ATOP—The destination inside the source is copied over the source.
- XOR—The parts of the source and destination that are outside each other are copied.
- CLEAR—The color and alpha of the destination are cleared.

Not only do each source and destination image have an alpha value, Java adds an extra alpha composite that is applied to the source alpha.

One of the tricky things is understanding that applying an AlphaComposite rule to a shape drawn with a graphics objects is not the same as drawing an entire image. When shapes are used, only the pixels inside the shape follow the composite rule, while images use the entire area.
