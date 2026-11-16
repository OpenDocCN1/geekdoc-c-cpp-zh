
```java
} finally {
if( reader != null ) {
try {
reader.close();
} catch( Exception e ) {
}
}
}
```

```java
protected void onSaveXML() {
JFileChooser chooser = new JFileChooser( currentDirectory );
chooser.setFileFilter( xmlFilter );
int retVal = chooser.showSaveDialog( this );
if( retVal == JFileChooser.APPROVE_OPTION ) {
File file = chooser.getSelectedFile();
currentDirectory = file;
if( file.exists() ) {
int overwrite = JOptionPane.showConfirmDialog( this,
"Overwrite existing file?" );
if( overwrite == JOptionPane.YES_OPTION ) {
writeXML( file );
}
} else {
writeXML(file);
}
}
}
```

```java
private void writeXML( File file ) {
PrintWriter out = null;
try {
out = new PrintWriter( file );
writeXML( out );
} catch( FileNotFoundException fex ) {
fex.printStackTrace();
} finally {
try {
out.close();
} catch( Exception e ) {
}
}
}
```

```java
private void writeXML( PrintWriter out ) {
    out.println( "<model bounds=\"" + bounds + "\">" );
    for( Vector2f point : polygon ) {
        out.println(
            "\\t<coord x=\"" + point.x + "\" y=\"" + point.y + "\" />"
        );
    }
    out.println( "</model>" );
}
```

```java
protected void increaseBounds() {
    bounds += DELTA;
    if( bounds > BOUNDS ) {
        bounds = BOUNDS;
    }
}
```

```java
protected void decreaseBounds() {
    bounds -= DELTA;
    if( bounds < DELTA ) {
        bounds = DELTA;
    }
}
```

```java
protected void exportImage() {
    JFileChooser chooser = new JFileChooser( currentDirectory );
    chooser.setFileFilter( imageFilter );
    int retVal = chooser.showSaveDialog( this );
    if( retVal == JFileChooser.APPROVE_OPTION ) {
        File file = chooser.getSelectedFile();
        currentDirectory = file;
        if( file.exists() ) {
            int overwrite = JOptionPane.showConfirmDialog( this,
                "Overwrite existing file?" );
            if( overwrite == JOptionPane.YES_OPTION ) {
                exportImage( file );
            }
        } else {
            exportImage( file );
        }
    }
}
```

```java
private void exportImage( File file ) {
    int imageWidth = Integer.parseInt( widthControl.getText() );
    int imageHeight = Integer.parseInt( heightControl.getText() );
BufferedImage image = new BufferedImage( imageWidth, imageHeight,
        BufferedImage.TYPE_INT_ARGB );
Matrix3x3f view = Utility.createViewport( bounds, bounds, imageWidth,
        imageHeight );
Graphics g = image.getGraphics();
drawPolygon( g, view );
g.dispose();
try {
    System.out.println(
            "Export: " + ImageIO.write( image, "png", file )
    );
} catch ( IOException e ) {
    e.printStackTrace();
}
}
```

```java
protected void importImage() {
JFileChooser chooser = new JFileChooser( currentDirectory );
chooser.setFileFilter( imageFilter );
int retVal = chooser.showOpenDialog( this );
if ( retVal == JFileChooser.APPROVE_OPTION ) {
    File file = chooser.getSelectedFile();
    currentDirectory = file;
    try {
        sprite = ImageIO.read( file );
        scaled = null;
    } catch ( IOException e ) {
        e.printStackTrace();
    }
}
}
```

```java
private void parseModel( Element model ) {
bounds = Float.parseFloat( model.getAttribute( "bounds" ) );
polygon.clear();
for ( Element coords : XMLUtility.getAllElements( model, "coord" ) ) {
    float x = Float.parseFloat( coords.getAttribute( "x" ) );
    float y = Float.parseFloat( coords.getAttribute( "y" ) );
    polygon.add( new Vector2f( x, y ) );
}
}
```

```java
@Override
protected void initialize() {
super.initialize();
polygon = new ArrayList<Vector2f>();
}

@Override
protected void processInput( float delta ) {
super.processInput( delta );
mousePos = getWorldMousePosition();
if (mouse.buttonDownOnce( MouseEvent.BUTTON1 ) ) {
polygon.add( mousePos );
}
if (mouse.buttonDownOnce( MouseEvent.BUTTON2 ) ) {
closed = !closed;
}
if (mouse.buttonDownOnce( MouseEvent.BUTTON3 ) ) {
if ( !polygon.isEmpty() ) {
polygon.remove( polygon.size() - 1 );
}
}
}

@Override
protected void render( Graphics g ) {
super.render( g );
((Graphics2D)g).setRenderingHint( RenderingHints.KEY_ANTIALIASING,
RenderingHints.VALUE_ANTIALIAS_ON );
((Graphics2D)g).setRenderingHint( RenderingHints.KEY_INTERPOLATION,
RenderingHints.VALUE_INTERPOLATION_BILINEAR );
textPos = Utility.drawString( g, 20, textPos, "Left Mouse: Add point",
"Right Mouse: Remove point", "Center Mouse: Toggle Close" );
drawSprite( g );
drawAxisLines( g );
drawPolygon( g, getViewportTransform() );
drawBoundingBox( g );
}
```

```java
private void drawSprite( Graphics g ) {
if ( sprite == null ) {
return;
}
Vector2f topLeft = new Vector2f( -bounds / 2.0f, bounds / 2.0f );
Vector2f bottomRight = new Vector2f( bounds / 2.0f, -bounds / 2.0f );
Matrix3x3f view = getViewportTransform();
topLeft = view.mul( topLeft );
bottomRight = view.mul( bottomRight );

int width = (int)Math.abs( topLeft.x - bottomRight.x );
int height = (int)Math.abs( topLeft.y - bottomRight.y );

if( scaled == null || scaled.getWidth() != width
|| scaled.getHeight() != height )
scaled = Utility.scaleImage( sprite, width, height );

g.drawImage( scaled, (int)topLeft.x, (int)topLeft.y, null );
}
```

```java
private void drawAxisLines( Graphics g ) {
g.setColor( Color.WHITE );
Vector2f left = new Vector2f( appWorldWidth / 2.0f, 0.0f );
Vector2f right = new Vector2f( -left.x, 0.0f );
drawLine( g, getViewportTransform(), left, right );

Vector2f top = new Vector2f( 0.0f, appWorldHeight / 2.0f );
Vector2f bottom = new Vector2f( 0.0f, -top.y );
drawLine( g, getViewportTransform(), top, bottom );
}
```

```java
private void drawPolygon( Graphics g, Matrix3x3f view ) {
g.setColor( Color.GREEN );

if( polygon.size() == 1 ) {
drawPoint( g, view, polygon.get( 0 ) );
}

for( int i = 0; i < polygon.size() - 1; ++i ) {
drawLine( g, view, polygon.get( i ), polygon.get( i + 1 ) );
}

if( closed && polygon.size() > 1 ) {
Vector2f P = polygon.get( polygon.size() - 1 );
Vector2f S = polygon.get( 0 );
drawLine( g, view, S, P );
}

if( ! polygon.isEmpty() || closed ) {
Vector2f P = polygon.get( polygon.size() - 1 );
Vector2f S = mousePos;
drawLine( g, view, S, P );
}
}
```

```java
private void drawPoint( Graphics g, Matrix3x3f view, Vector2f v ) {
    Vector2f S = view.mul( v );
    g.drawRect( (int)S.x, (int)S.y, 1, 1 );
}

private void drawLine(
    Graphics g, Matrix3x3f view, Vector2f v0, Vector2f v1 ) {
    Vector2f S = view.mul( v0 );
    Vector2f P = view.mul( v1 );
    g.drawLine( (int)S.x, (int)S.y, (int)P.x, (int)P.y );
}

private void drawBoundingBox( Graphics g ) {
    Vector2f[] bb = { new Vector2f( -bounds / 2.0f, bounds / 2.0f ),
        new Vector2f( bounds / 2.0f, bounds / 2.0f ),
        new Vector2f( bounds / 2.0f, -bounds / 2.0f ),
        new Vector2f( -bounds / 2.0f, -bounds / 2.0f ) };
    Matrix3x3f view = getViewportTransform();
    for( int i = 0; i < bb.length; ++i ) {
        bb[ i ] = view.mul( bb[ i ] );
    }
    g.setColor( Color.WHITE );
    Utility.drawPolygon( g, bb );
}

public static void main( String[] args ) {
    LaunchApp( new PolygonEditor() );
}
```

## DRAWING A SPRITE

The Sprite class is added to the javagames.util package to handle drawing images in pixel size to rectangles in world space. Just like the drawSprite() method in the PolygonEditor, the Sprite class has a top-left and bottom-right vector defining the bounding rectangle in world space.

The sprite can be drawn with an optional rotation. The render method first calculates the screen size of the rectangle and then, if the scaled image isn't the correct size, the original image is scaled. The AffineTransform with a bilinear interpolation from Chapter 10 is used to render the image. Remember that the AffineTransform class is column major, so the transformations are in reverse order. The image is transformed to the center, rotated by the negative of the rotation angle (to take into account the flipped y-axis in screen space), and finally transformed to the screen position.

There is also an extra scaleImage() method to scale the image before rendering it, which can save time by performing the scaling when the sprite image is first loaded. As long as the world-to-screen viewport matrix can be created when the sprite's image is loaded, this method will scale the image to the correct size before the first image is rendered.

```java
package javagames.util;

import java.awt.*;
import java.awt.geom.AffineTransform;
import java.awt.image.BufferedImage;

public class Sprite {
private BufferedImage image;
private BufferedImage scaled;
private Vector2f topLeft;
private Vector2f bottomRight;

public Sprite(
BufferedImage image, Vector2f topLeft, Vector2f bottomRight ) {
this.image = image;
this.topLeft = topLeft;
this.bottomRight = bottomRight;
}

public void render( Graphics2D g, Matrix3x3f view ) {
render( g, view, new Vector2f(), 0.0f );
}

public void render(
Graphics2D g, Matrix3x3f view, Vector2f position, float angle ) {
if ( image != null ) {
Vector2f tl = view.mul( topLeft );
Vector2f br = view.mul( bottomRight );
int width = (int)Math.abs( br.x - tl.x );
int height = (int)Math.abs( br.y - tl.y );
if ( scaled == null || width != scaled.getWidth() ||
height != scaled.getHeight() ) {
scaled = Utility.scaleImage( image, width, height );
}
g.setRenderingHint(
RenderingHints.KEY_INTERPOLATION,
RenderingHints.VALUE_INTERPOLATION_BILINEAR
);
}
}
