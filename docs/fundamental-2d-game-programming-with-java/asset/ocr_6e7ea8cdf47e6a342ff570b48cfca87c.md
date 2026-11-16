```
```java
float ty = screenHeight / 2.0f;
viewport = viewport.mul( Matrix3x3f.translate( tx, ty ) );

for( int i = 0; i < cannon.length; ++i ) {
    cannonCpy[i] = viewport.mul( cannonCpy[i] );
}

drawPolygon( g, cannonCpy );

if( bullet != null ) {
    bulletCpy = viewport.mul( bulletCpy );
    g.drawRect( (int)bulletCpy.x-2, (int)bulletCpy.y-2, 4, 4 );
}
```
```

```
```java
private void drawPolygon( Graphics g, Vector2f[] polygon ) {
    Vector2f P;
    Vector2f S = polygon[ polygon.length - 1 ];
    for( int i = 0; i < polygon.length; ++i ) {
        P = polygon[i];
        g.drawLine( (int)S.x, (int)S.y, (int)P.x, (int)P.y );
        S = P;
    }
}
```
```

```
```java
protected void onWindowClosing() {
    try {
        running = false;
        gameThread.join();
    } catch( InterruptedException e ) {
        e.printStackTrace();
    }
    System.exit( 0 );
}
```
```

```
```java
public static void main( String[] args ) {
    final CannonExample app = new CannonExample();
    app.addWindowListener( new WindowAdapter() {
        public void windowClosing( WindowEvent e ) {
            app.onWindowClosing();
        }
    });
}
```
```