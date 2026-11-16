projection must be a normal vector and that normal vector needs to be scaled by the dot product.

![](bbox=[0.103, 0.153, 0.417, 0.263])

Figure 6.11
Dot Product Scalar.
© 2014 Timothy Wright.

# ANGLE()

```
public float angle() {
    return (float)Math.atan2( y , x );
}
```

The angle() method returns the angle in radians created by the vector, as shown in Figure 6.12. Notice the atan2() method is used to handle the cases where x is zero, so no additional checks are needed.

![](bbox=[0.103, 0.553, 0.417, 0.663])

Figure 6.12
Angle.
© 2014 Timothy Wright.

# POLAR()

```
public static Vector2f polar( float angle, float radius ) {
    return new Vector2f(
        radius * (float)Math.cos( angle ),
        radius * (float)Math.sin( angle )
    );
}
```