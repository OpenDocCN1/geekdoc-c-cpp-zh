```
if (mouse.buttonDownOnce (MouseEvent.BUTTON3 ) ) {
    A = B = C = D = null;
    intersect = null;
}
}
```

```
@Override
protected void updateObjects( float delta ) {
    super.updateObjects( delta );

    if ( ( A == null ) | | B == null ) | | C == null ) | | D == null ) ) {
        float[ ] t = lineLineIntersection( A, B, C, D );
        if ( t == null ) {
            intersect = null;
        } else {
            intersect = A.add( B.sub( A ).mul( t[ 0 ] ) );
        }
    }
}
```

```
private float[ ] lineLineIntersection(
    Vector2f A, Vector2f B, Vector2f C, Vector2f D ) {
    Vector2f DsubC = D.sub( C );
    Vector2f DsubCperp = DsubC.perp( );
    Vector2f AsubB = A.sub( B );
    float f = DsubCperp.dot( AsubB );
    if ( Math.abs( f ) < EPSILON ) {
        return null; // zero denom
    }

    Vector2f AsubC = A.sub( C );
    float d = DsubCperp.dot( AsubC );
    if ( f > 0 ) {
        if ( d < 0 | | d > f ) return null;
    } else {
        if ( d > 0 | | d < f ) return null;
    }

    Vector2f BsubA = B.sub( A );
    Vector2f BsubAperp = BsubA.perp( );
    float e = BsubAperp.dot( AsubC );
    if ( f > 0 ) {
        if ( e < 0 | | e > f ) return null;
    } else {
        if ( e > 0 | | e < f ) return null;
    }
}
```