```
canvas.setBackground( Color.BLACK );
canvas.setIgnoreRepaint( true );
getContentPane().add( canvas );
setTitle( "Active Rendering" );
setIgnoreRepaint( true );
pack();
setVisible( true );
canvas.createBufferStrategy( 2 );
bs = canvas.getBufferStrategy();
gameThread = new Thread( this );
gameThread.start();
```

```
public void run() {
    running = true;
    frameRate.initialize();
    while( running ) {
        gameLoop();
    }
}
```

```
public void gameLoop() {
    do {
        do {
            Graphics g = null;
            try {
                g = bs.getDrawGraphics();
                g.clearRect( 0, 0, getWidth(), getHeight() );
                render( g );
            } finally {
                if ( g != null ) {
                    g.dispose();
                }
            }
        } while ( bs.contentsRestored() );
        bs.show();
    } while ( bs.contentsLost() );
}
```

```
private void render( Graphics g ) {
    frameRate.calculate();
    g.setColor( Color.GREEN );
    g.drawString( frameRate.getFrameRate(), 30, 30 );
}
```