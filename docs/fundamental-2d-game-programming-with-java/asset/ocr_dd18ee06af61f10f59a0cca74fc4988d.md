```
```java
end = System.nanoTime();
stepDownBicubicSpeed = (end - start) / 1.0E6;
stepDownBicubicSpeed /= 100;
}

private void createTestImage() {
sprite = new BufferedImage(
IMG_WIDTH, IMG_HEIGHT, BufferedImage.TYPE_INT_ARGB );
Graphics2D g2d = sprite.createGraphics();

// draw checker board
g2d.setColor( Color.WHITE );
g2d.fillRect( 0, 0, IMG_WIDTH / 2, IMG_HEIGHT / 2 );
g2d.fillRect( IMG_WIDTH / 2, IMG_HEIGHT / 2, IMG_WIDTH, IMG_HEIGHT );
g2d.setColor( Color.BLACK );
g2d.fillRect( IMG_WIDTH / 2, 0, IMG_WIDTH , IMG_HEIGHT / 2 );
g2d.fillRect( 0, IMG_HEIGHT / 2, IMG_WIDTH / 2, IMG_HEIGHT );

// gradient circle
float x1 = sprite.getWidth() / 4;
float x2 = sprite.getWidth() * 3 / 4;
float y1 = sprite.getHeight() / 4;
float y2 = sprite.getHeight() * 3 / 4;
GradientPaint gp =
new GradientPaint( x1, y1, Color.BLACK, x2, y2, Color.WHITE );
g2d.setPaint( gp );
g2d.fillOval(
sprite.getWidth() / 4, sprite.getHeight() / 4,
sprite.getWidth() / 2, sprite.getHeight() / 2
);

// draw hash lines
g2d.setColor( Color.GREEN );
int dx = sprite.getWidth() / 4;
for( int i = 0; i < sprite.getWidth(); i += dx ) {
g2d.drawLine( i + 7, 0, i + 7, sprite.getHeight() );
}

g2d.setColor( Color.BLUE );
dx = sprite.getHeight() / 4;
for( int i = 0; i < sprite.getHeight(); i += dx ) {
g2d.drawLine( 0, i + 7, sprite.getWidth(), i + 7 );
}

// draw red diamond
g2d.setColor( Color.RED );
g2d.drawLine( 0, sprite.getHeight() / 2, sprite.getWidth() / 2, 0 );
```
```