```
for( int i = 0; i < 2; ++i ) {
    Vector2f n = rect[i].sub( rect[i+1] );
    n = n.norm();
    float e0 = n.dot( rect[i].sub( 0 ) );
    float e1 = n.dot( rect[i+1].sub( 0 ) );
    float f = n.dot( d );
    if( Math.abs( f ) > EPSILON ) {
        // calculate intersection
    } else if( e0*e1 > 0 ) {
        return null;
    }
}
return intersection; // TODO
```

+   1. Loop through the rectangle and test each pair of parallel sides.
+   2. Compute the perpendicular normal to the two sides being tested.
+   3. Normalize the vector, because this vector is used with the dot product (see Chapter 6 for more information).
+   4. Compute the numerator for the intersection equation of the first side.
+   5. Compute the numerator for the intersection equation of the second side.
+   6. Compute the denominator for the intersection equation.
+   7. Check if the denominator is zero, which means the ray is parallel to the sides.
+   8. Test if the parallel line is between the two sides. If it isn't, there can be no intersection.
+   9. Since the parallel line is outside the rectangle, no intersection is possible.
+   10. Return the intersection here, but that can't happen yet.

The test in line 8 can be confusing. The e0 and e1 values are the signed distances from the origin to the side. The only way for the parallel line to be between the sides is if one distance is negative and the other is positive. If they are both positive or both negative, then they cannot be between the sides. The product of two positive or two negative values is always positive, so only if the product is negative can they be between the two sides.