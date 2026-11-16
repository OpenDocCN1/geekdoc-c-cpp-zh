```
try {
    g = bs.getDrawGraphics();
    g.clearRect(0, 0, getWidth(), getHeight());
    render(g);
} finally {
    if (g != null) {
        g.dispose();
    }
}
} while (bs.contentsRestored());
bs.show();
} while (bs.contentsLost());
}

private void sleep( long sleep ) {
    try {
        Thread.sleep(sleep);
    } catch (InterruptedException ex) {
    }
}

private void processInput() {
    keyboard.poll();
    mouse.poll();

    Point p = mouse.getPosition();
    if (mouse.isRelative()) {
        point.x += p.x;
        point.y += p.y;
    } else {
        point.x = p.x;
        point.y = p.y;
    }

    // Wrap rectangle around the screen
    // if (point.x + 25 < 0)
    if (point.x == canvas.getWidth() - 1;
    else if (point.x > canvas.getWidth() - 1 )
        point.x = -25;
    if (point.y < 0)
        point.y = canvas.getHeight() - 1;
    else if (point.y > canvas.getHeight() - 1 )
        point.y = -25;

    // Toggle relative
    if (keyboard.keyDownOnce( KeyEvent.VK_SPACE ) ) {
        mouse.setRelative( !mouse.isRelative() );
    }
}
```