```
startAbove = endAbove;
start = end;
}
}
return inside != 0;
}

@Override
protected void render( Graphics g ) {
    super.render( g );
    // render instructions
    g.drawString( "Winding: " + (winding?"ON":"OFF"), 20, 35 );
    String mouse =
        String.format( "Mouse: (%.2f,%.2f)", mousePos.x, mousePos.y );
    g.drawString( mouse, 20, 50 );
    g.drawString( "Left-Click to add points", 20, 65 );
    g.drawString( "Right-Click to clear points", 20, 80 );
    g.drawString( "Space Bar to toggle winding", 20, 95 );
    Matrix3x3f view = getViewportTransform();
    // draw test polygon
    if( poly.size() > 1 ) {
        polyCpy.clear();
        for( Vector2f vertex : poly ) {
            polyCpy.add( view.mul( vertex ) );
        }
        g.setColor( selected ? Color.GREEN : Color.BLUE );
        Utility.drawPolygon( g, polyCpy );
    }
    // draw inside point blue, outside points red
    g.setColor( Color.BLUE );
    for( Vector2f vector : inside ) {
        Vector2f point = view.mul( vector );
        g.fillRect( (int)point.x, (int)point.y, 1, 1 );
    }
    g.setColor( Color.RED );
    for( Vector2f vector : outside ) {
        Vector2f point = view.mul( vector );
        g.fillRect( (int)point.x, (int)point.y, 1, 1 );
    }
}

public static void main( String[] args ) {
    launchApp( new PointInPolygonExample() );
}
}
```