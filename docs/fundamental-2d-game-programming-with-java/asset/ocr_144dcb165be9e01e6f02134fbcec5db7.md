```
private void processObjects() {
    // copy data...
    for( int i = 0; i < polygon.length; ++i ) {
        world[i] = new Vector2f( polygon[i] );
    }

    if( doScale ) {
        scale += scaleStep;
        if( scale < 1.0 || scale > 5.0 ) {
            scaleStep = -scaleStep;
        }
    }

    if( doRotate ) {
        rot += rotStep;
        if( rot < 0.0f || rot > 2*Math.PI ) {
            rotStep = -rotStep;
        }
    }

    if( doTranslate ) {
        tx += vx;
        if( tx < 0 || tx > SCREEN_W ) {
            vx = -vx;
        }
        ty += vy;
        if( ty < 0 || ty > SCREEN_H ) {
            vy = -vy;
        }
    }

    if( doXShear ) {
        sx += sxStep;
        if( Math.abs( sx ) > 2.0 ) {
            sxStep = -sxStep;
        }
    }

    if( doYShear ) {
        sy += syStep;
        if( Math.abs( sy ) > 2.0 ) {
            syStep = -syStep;
        }
    }

    for( int i = 0; i < world.length; ++i ) {
        world[i].shear( sx, sy );
    }
}
```