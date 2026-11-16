```
BufferedImage tmp =
    new BufferedImage( w, h, BufferedImage.TYPE_INT_ARGB );
Graphics2D g2d = tmp.createGraphics();
g2d.setRenderingHint( RenderingHints.KEY_INTERPOLATION, hintValue );
g2d.drawImage( ret, 0, 0, w, h, null );
g2d.dispose();
ret = tmp;
} while( w != targetWidth || h != targetHeight );
return ret;
}

private ImageConsumer getConsumer() {
    return new ImageConsumer() {
    public void setProperties( Hashtable<?, ?> props ) { }
    public void setDimensions( int x, int y, int w, int h, ColorModel model,
    int[] pixels, int off, int scansize ) { }
    public void setPixels( int x, int y, int w, int h, ColorModel model,
    byte[] pixels, int off, int scansize ) { }
    public void setPixels( int x, int y, int w, int h, ColorModel model,
    int[] pixels, int off, int scansize ) { }
    public void setHints( int hintflags ) { }
    public void setDimensions( int width, int height ) { }
    public void setColorModel( ColorModel model ) { }
    public void imageComplete( int status ) { }
    };
};

public static void main( String[] args ) {
    launchApp( new ScaleImageExample() );
}
}
```