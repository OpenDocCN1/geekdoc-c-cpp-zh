```
```java
if (KeyEvent.VK_ENTER == typedChar ) {
    strings.add( "" );
}
else {
    addCharacter( typedChar );
}
drawCursor = true;
blink = 0.0f;
}

private void addCharacter( Character c ) {
    strings.add( strings.remove( strings.size() - 1 ) + c );
}

private void removeCharacter() {
    String line = strings.remove( strings.size() - 1 );
    if ( line.isEmpty() ) {
        strings.add( line.substring( 0, line.length() - 1 ) );
    }

    if ( strings.isEmpty() ) {
        strings.add( "" );
    }
}

@Override
protected void updateObjects( float delta ) {
    super.updateObjects( delta );

    blink += delta;
    if ( blink > 0.5f ) {
        blink = -0.5f;
        drawCursor = !drawCursor;
    }
}

@Override
protected void render( Graphics g ) {
    super.render( g );

    textPos = Utility.drawString( g, 20, textPos,
        "",
        "Sleep Value: " + appSleep,
        "Space Count: " + spacesCount,
        "Press Up to increase sleep",
        "Press Down to decrease sleep",
```
```