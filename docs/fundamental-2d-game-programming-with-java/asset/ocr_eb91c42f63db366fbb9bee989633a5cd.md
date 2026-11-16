```
@Override
protected void render( Graphics g ) {
    super.render( g );

    // Box this text...
    g.setColor( Color.BLACK );
    String box = "great Java, now what?";
    Font font = new Font( "Arial", Font.PLAIN, 24 );
    g.setFont( font );
    g.drawString( box, 20, 50 );
    g.setColor( Color.RED );
    g.drawRect( 20, 50, 200, 20 );
}

public static void main( String[] args ) {
    launchApp( new BoxedTextProblem() );
}
}
```

Ignore that the width of the rectangle is just a guess. Even though both the rectangle and text are drawn with their upper-left position at (20, 50), the results are not similar. See Figure 11.1.

![](bbox=[0.1, 0.5, 0.55, 0.65])

# Figure 11.1 Boxed Text Problem. © 2014 Timothy Wright.

The problem is that text is not treated the same as images. Although images are drawn from the upper-left corner, text is drawn from the baseline, and the height and width of the rendered string depends on the selected font type, style, and size.