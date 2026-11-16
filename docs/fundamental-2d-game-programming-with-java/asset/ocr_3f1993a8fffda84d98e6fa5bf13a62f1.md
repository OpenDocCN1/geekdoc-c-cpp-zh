```
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
```