```
```java
DisplayModeWrapper wrap = new DisplayModeWrapper( mode );
if( !list.contains( wrap ) ) {
list.add( wrap );
}
}
}
return list.toArray( new DisplayModeWrapper[0] );
}

protected void createAndShowGUI() {
Container canvas = getContentPane();
canvas.add( getMainPanel() );
canvas.setIgnoreRepaint( true );
setDefaultCloseOperation( EXIT_ON_CLOSE );
setTitle( "Display Mode Test" );
pack();
setVisible( true );
}

protected void onEnterFullScreen() {
if( graphicsDevice.isFullScreenSupported() ) {
DisplayMode newMode = getSelectedMode();
graphicsDevice.setFullScreenWindow( this );
graphicsDevice.setDisplayMode( newMode );
}
}

protected void onExitFullScreen() {
graphicsDevice.setDisplayMode( currentDisplayMode );
graphicsDevice.setFullScreenWindow( null );
}

protected DisplayMode getSelectedMode() {
DisplayModeWrapper wrapper =
(DisplayModeWrapper)displayModes.getSelectedItem();
DisplayMode dm = wrapper.dm;
int width = dm.getWidth();
int height = dm.getHeight();
int bit = 32;
int refresh = DisplayMode.REFRESH_RATE_UNKNOWN;
return new DisplayMode( width, height, bit, refresh );
}

public static void main( String[] args ) {
final DisplayModeExample app = new DisplayModeExample();
SwingUtilities.invokeLater( new Runnable() {
public void run() {
```
```