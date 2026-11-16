```
if (hide && hidden < 1.0f ) {
    hidden += delta ;
    if (hidden > 1.0f ) hidden = 1.0f;
} else if ( hide && hidden > 0.0f ) {
    hidden -= delta;
    if ( hidden < 0.0f ) hidden = 0.0f;
}
```

```
if(hidden > 0.0f ) {
    g.setComposite(
        AlphaComposite.getInstance( AlphaComposite.CLEAR ) );
    // clear left
    int xHide = (int)(console.getWidth() * hidden * 0.5f);
    g.fillRect( 0, 0, xHide, console.getHeight() );
    // clear right
    g.fillRect(
        console.getWidth() - xHide, 0,
        console.getWidth(), console.getHeight()
    );
    // clear top
    int yHide = (int)(console.getHeight() * hidden * 0.5f);
    g.fillRect( 0, 0, console.getWidth(), yHide );
    // clear bottom
    g.fillRect(
        0, console.getHeight() - yHide,
        console.getWidth(), console.getHeight()
    );
    g.dispose();
}
```

```
@Override
protected void render( Graphics g ) {
    super.render( g );
    Graphics2D g2d = (Graphics2D)g;
    int dx = (canvas.getWidth() ) / 8;
    int dy = (canvas.getHeight()) / 8;
    for( int i = 0; i < 8; ++i ) {
        for( int j = 0; j < 8; ++j ) {
            g2d.setColor( ((i+j) % 2 == 0 ? Color.BLACK : Color.WHITE ) );
            g2d.fillRect( i*dx, j*dy, dx, dy );
        }
    }
}
```