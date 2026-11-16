```
// Toggle cursor
if (keyboard.keyDownOnce(KeyEvent.VK_C)) {
    disableCursor = !disableCursor;
    if (disableCursor) {
        disableCursor();
    } else {
        // setCursor( Cursor.DEFAULT_CURSOR ) is deprecated
        setCursor( new Cursor( Cursor.DEFAULT_CURSOR ) );
    }
}
```

```
private void render(Graphics g) {
    g.setColor( Color.GREEN );
    frameRate.calculate();
    g.drawString( mouse.getPosition().toString(), 20, 20 );
    g.drawString( "Relative: " + mouse.isRelative(), 20, 35 );
    g.drawString( "Press Space to switch mouse modes", 20, 50 );
    g.drawString( "Press C to toggle cursor", 20, 65 );

    g.setColor( Color.WHITE );
    g.drawRect( point.x, point.y, 25, 25 );
}
```

```
private void disableCursor() {
    Toolkit tk = Toolkit.getDefaultToolkit();
    Image image = tk.createImage( "" );
    Point point = new Point( 0, 0 );
    String name = "CanBeAnything";
    Cursor cursor = tk.createCustomCursor( image, point, name );
    setCursor( cursor );
}
```

```
protected void onWindowClosing() {
    try {
        running = false;
        gameThread.join();
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
    System.exit( 0 );
}
```

```
public static void main( String[] args ) {
    final RelativeMouseExample app = new RelativeMouseExample();
    app.addWindowListener( new WindowAdapter() {
        public void windowClosing( WindowEvent e ) {
```