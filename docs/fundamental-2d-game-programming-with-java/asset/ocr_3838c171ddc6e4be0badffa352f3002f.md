```
```
consoleFont = new Font( "Courier New", Font.BOLD, 20 );
FontMetrics fm = getFontMetrics( consoleFont );
fontHeight = fm.getAscent() + fm.getDescent() + fm.getLeading();
currY = 0;
text = new Vector<String>();
text.add( "Press the 'H' key to" );
text.add( "show and hide the console." );
text.add( "Hover the mouse over the" );
text.add( "text to change transparency." );
text.add( "Press Space Bar to move text." );
text.add( "Press 'B' to toggle hidden boxes." );
text.add( 0, text.lastElement() );
int consoleHeight = fontHeight * ( text.size() + 1 );
console = new BufferedImage(
canvas.getWidth() - 40,
consoleHeight,
BufferedImage.TYPE_INT_ARGB
);
xConsole = 20;
yConsole = 50;
hide = false;
hidden = 1.0f;
}
@Override
protected void processInput( float delta ) {
super.processInput( delta );
Point pos = mouse.getPosition();
int minX = xConsole;
int minY = yConsole;
int maxX = minX + console.getWidth();
int maxY = minY + console.getHeight();
if ( pos.x > minX && pos.x < maxX &&
pos.y > minY && pos.y < maxY ) {
alpha = 1.0f;
} else {
alpha = 0.75f;
}
if ( keyboard.keyDownOnce( KeyEvent.VK_SPACE ) ) {
text.remove( 0 );
text.add( text.get( 0 ) );
currY = fontHeight;
```
```