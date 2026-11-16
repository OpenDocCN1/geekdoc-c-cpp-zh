The file chooser has two methods for displaying the dialog: one for loading files and one for saving.

```
JFileChooser.showOpenDialog()
JFileChooser.showSaveDialog()
```

There are a lot of different methods in the JFileChooser class. While the online documentation explains all the details, the two examples of loading and saving both PNG and XML files are a good introduction.

Also, notice that the image scaling updates to the Utility class, the width and height text fields, and the bounding screen rectangle are all necessary to import and export images. Because the images are saved by pixel width and height, but displayed in the editor by world units (in this case, 2 x 2 units), an imported image needs to be scaled to fit to the bounds. Exporting from a 2 x 2 bounding rectangle in screen space needs text fields to specify a width and height for the image size.

One new method to examine is the drawSprite() method:

```
private void drawSprite(Graphics g) {
    if (sprite == null) {
        return;
    }
    Vector2f topLeft = new Vector2f( -bounds / 2.0f, bounds / 2.0f );
    Vector2f bottomRight = new Vector2f( bounds / 2.0f, bounds / 2.0f );
    Matrix3x3f view = getViewportTransform();
    topLeft = view.mul( topLeft );
    bottomRight = view.mul( bottomRight );
    int width = (int)Math.abs( topLeft.x - bottomRight.x );
    int height = (int)Math.abs( topLeft.y - bottomRight.y );
    if (scaled == null || scaled.getWidth() != width
            || scaled.getHeight() != height ) {
        scaled = Utility.scaleImage( sprite, width, height );
    }
    g.drawImage( scaled, (int)topLeft.x, (int)topLeft.y, null );
}
```

This method creates a topLeft and bottomRight vector and scales this rectangle to the screen. This screen size is then used to scale the sprite image to the same screen size. This method is the basis for the Sprite class presented later in the chapter.

The rest of the code for drawing points, polygons, and handling the mouse button input is the same as the previous editor. Except for the new Swing controls, there is nothing in this example that hasn't already been presented.