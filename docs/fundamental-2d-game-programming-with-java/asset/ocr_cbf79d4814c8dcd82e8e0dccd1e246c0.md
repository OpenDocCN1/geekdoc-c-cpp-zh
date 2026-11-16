```
```java
@Override
protected void render( Graphics g ) {
    super.render( g );

    Graphics2D g2d = (Graphics2D)g;
    g2d.setRenderingHint( RenderingHints.KEY_ANTIALIASING,
            RenderingHints.VALUE_ANTIALIAS_ON );

    Font font = new Font( "Times New Roman", Font.BOLD | Font.ITALIC, 40 );
    g2d.setFont( font );
    g2d.setColor( Color.GREEN );
    String str = "Groovy Baby BLAH";
    int x = 50;
    int y = 50;
    g2d.drawString( str, x, y );

    // Text Layout gives floating point values
    FontRenderContext frc = g2d.getFontRenderContext();
    TextLayout tl = new TextLayout( str, font, frc );
    // draw another line, should be at
    // y + ascent + decent + leading
    int newY =
        y + (int)( tl.getAscent() + tl.getDescent() + tl.getLeading() );
    g2d.drawString( str, x, newY );

    // draw centered Text
    // first lets draw the center of the window...
    g2d.setColor( Color.GRAY );
    int sw = canvas.getWidth();
    int sh = canvas.getHeight();
    int cx = sw / 2;
    int cy = sh / 2;
    g2d.drawline(0, cy, sw, cy);
    g2d.drawline(cx, 0, cx, sh);

    String center = "Should Center: Center Baby's @";
    // to calculate the x, i need the width...
    int stringWidth = g2d.getFontMetrics().stringWidth( center );
    float dy = g2d.getFontMetrics().getLineMetrics( center, g2d )
            .getBaselineOffsets()[ Font.CENTER_BASELINE ];
    g2d.drawString(center, cx - stringWidth / 2, cy - dy );

    // draw the pixel where we are drawing the text...
    g2d.setColor( Color.WHITE );
    g2d.fillRect( x - 1, y - 1, 3, 3 );
}
```
```