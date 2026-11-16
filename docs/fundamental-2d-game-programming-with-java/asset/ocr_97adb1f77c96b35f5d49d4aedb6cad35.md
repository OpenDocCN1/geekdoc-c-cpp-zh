```
private void writeXML( PrintWriter out ) {
    out.println( "<model bounds=\"" + bounds + \">" );
    for( Vector2f point : polygon ) {
        out.println(
            "\\t<coord x=\"" + point.x + \"" y=\"" + point.y + \"" />"
        );
    }
    out.println( "</model>" );
}
```

```
protected void increaseBounds() {
    bounds += DELTA;
    if( bounds > BOUNDS ) {
        bounds = BOUNDS;
    }
}
```

```
protected void decreaseBounds() {
    bounds -= DELTA;
    if( bounds < DELTA ) {
        bounds = DELTA;
    }
}
```

```
protected void exportImage() {
    JFileChooser chooser = new JFileChooser( currentDirectory );
    chooser.setFileFilter( imageFilter );
    int retVal = chooser.showSaveDialog( this );
    if( retVal == JFileChooser.APPROVE_OPTION ) {
        File file = chooser.getSelectedFile();
        currentDirectory = file;
        if( file.exists() ) {
            int overwrite = JOptionPane.showConfirmDialog( this,
                "Overwrite existing file?" );
            if( overwrite == JOptionPane.YES_OPTION ) {
                exportImage( file );
            }
        } else {
            exportImage( file );
        }
    }
}
```

```
private void exportImage( File file ) {
    int imageWidth = Integer.parseInt( widthControl.getText() );
    int imageHeight = Integer.parseInt( heightControl.getText() );
```