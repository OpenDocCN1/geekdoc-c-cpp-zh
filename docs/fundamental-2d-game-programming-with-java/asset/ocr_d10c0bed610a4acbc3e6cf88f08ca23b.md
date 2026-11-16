```
Vector2f AsubC = A.sub( C );
float d = SubCperp.dot( AsubC );
if ( f > 0 ) {
    if( d < 0 || d > f ) return null;
} else {
    if( d > 0 || d < f ) return null;
}
Vector2f BsubA = B.sub( A );
Vector2f BsubAperp = BsubA.perp();
float e = BsubAperp.dot( AsubC );
if ( f > 0 ) {
    if( e < 0 || e > f ) return null;
} else {
    if( e > 0 || e < f ) return null;
}
return new float[]{
    d / f, e / f
};
}
```

![](bbox=[0.1, 0.46, 0.5, 0.75])

Figure 15.20 Line-Line Intersection Example. © 2014 Timothy Wright.

The LineLineIntersectionExample, as seen in Figure 15.20 and located in the javagames.collision package, finds the intersection between two line segments using the algorithm previously described. The EPSILON value is used to see if the determinant