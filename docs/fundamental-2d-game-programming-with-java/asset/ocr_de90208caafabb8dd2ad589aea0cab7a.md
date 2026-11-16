```
public void run() {
    running = true;
    initialize();
    long curTime = System.nanoTime();
    long lastTime = curTime;
    double nsPerFrame;
    while( running ) {
        curTime = System.nanoTime();
        nsPerFrame = curTime - lastTime;
        gameLoop( nsPerFrame / 1.0E9 );
        lastTime = curTime;
    }
}
```

```
private void gameLoop( double delta ) {
    processInput( delta );
    updateObjects( delta );
    renderFrame();
    sleep( 10L );
}
```

```
private void renderFrame() {
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
        } while( bs.contentsRestored() );
        bs.show();
    } while( bs.contentsLost() );
}
```

```
private void sleep( long sleep ) {
    try {
        Thread.sleep( sleep );
    } catch( InterruptedException ex ) { }
}
```