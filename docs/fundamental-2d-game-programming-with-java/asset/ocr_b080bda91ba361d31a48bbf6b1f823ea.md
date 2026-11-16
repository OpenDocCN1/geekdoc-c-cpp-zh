```
// Add mouse listeners
// For full screen : mouse = new RelativeMouseInput( this );
mouse = new RelativeMouseInput( canvas );
canvas.addMouseListener( mouse );
canvas.addMouseMotionListener( mouse );
canvas.addMouseWheelListener( mouse );

setVisible( true );
canvas.createBufferStrategy( 2 );
bs = canvas.getBufferStrategy();
canvas.requestFocus();

gameThread = new Thread( this );
gameThread.start();
}

public void run() {
    running = true;
    initialize();
    while( running ) {
        gameLoop();
    }
}

private void gameLoop() {
    processInput();
    renderFrame();
    sleep( 10L );
}

private void renderFrame() {
    do
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
```