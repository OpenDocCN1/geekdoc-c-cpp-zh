```
if ( keyboard.keyDownOnce( KeyEvent.VK_F1 ) ) {
    loadWaveFile( weaponBytes );
    loaded = "weapon";
}

if ( keyboard.keyDownOnce( KeyEvent.VK_F2 ) ) {
    loadWaveFile( rainBytes );
    loaded = "rain";
}

if ( keyboard.keyDownOnce( KeyEvent.VK_1 ) ) {
    oneShotClip.fire();
}

if ( keyboard.keyDownOnce( KeyEvent.VK_2 ) ) {
    oneShotClip.done();
}

if ( keyboard.keyDownOnce( KeyEvent.VK_3 ) ) {
    loopClip.fire();
}

if ( keyboard.keyDownOnce( KeyEvent.VK_4 ) ) {
    loopClip.done();
}

if ( keyboard.keyDownOnce( KeyEvent.VK_5 ) ) {
    restartClip.fire();
}

if ( keyboard.keyDownOnce( KeyEvent.VK_6 ) ) {
    oneShotStream.fire();
}

if ( keyboard.keyDownOnce( KeyEvent.VK_7 ) ) {
    oneShotStream.done();
}

if ( keyboard.keyDownOnce( KeyEvent.VK_8 ) ) {
    loopStream.fire();
}

if ( keyboard.keyDownOnce( KeyEvent.VK_9 ) ) {
    loopStream.done();
}

if ( keyboard.keyDownOnce( KeyEvent.VK_0 ) ) {
    restartStream.fire();
}
}
```

```
@Override
protected void updateObjects( float delta ) {
    super.updateObjects( delta );
}
```