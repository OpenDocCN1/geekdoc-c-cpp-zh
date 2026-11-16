
## VECTOR2F UPDATES

There are updates to the vector class that you need to be aware of before you move on to the intersection-testing algorithms and concepts. The updates are covered in this chapter.

### INV()

```
public Vector2f inv() {
    return new Vector2f( -x, -y );
}
```

The inv() method returns a new vector that is the inverse of the current vector. The inverse of a vector, as shown in Figure 6.1, is a new vector that points in the opposite direction.

![](img/588a4cda8f2acae94a7e1987bf99400d_151_0.png)

Figure 6.1
Vector Inverse.
© 2014 Timothy Wright.

### ADD()

```
public Vector2f add( Vector2f v ) {
    return new Vector2f( x + v.x, y + v.y );
}
```

The add() method returns a new vector that is the sum of the current vector and the given vector. See Figure 6.2.

![](img/588a4cda8f2acae94a7e1987bf99400d_152_0.png)

Figure 6.2 Vector Addition. © 2014 Timothy Wright.

### SUB()

```
public Vector2f sub( Vector2f v ) {
    return new Vector2f( x - v.x, y - v.y );
}
```

The sub() method returns a new vector that is the subtraction of the given vector and the current vector. Notice in Figure 6.3 that order matters. The arrow of the new vector will point to the first vector in the operation.

![](img/588a4cda8f2acae94a7e1987bf99400d_152_1.png)

Figure 6.3 Vector Subtraction. © 2014 Timothy Wright.

Sometimes it is easier to visualize subtraction as adding the inverse of a vector. As shown in Figure 6.4, V1 – V2 and V1 + (–V2) produce the same result.

![](img/588a4cda8f2acae94a7e1987bf99400d_153_0.png)

Figure 6.4
Vector Subtraction as Inverse Addition.
© 2014 Timothy Wright.

### MUL()

```
public Vector2f mul( float scalar ) {
    return new Vector2f( scalar * x, scalar * y );
}
```

The mul() method returns a new vector that is the product of the vector component
and the scalar value. Notice in Figure 6.5 that negative values invert the vector.

![](img/588a4cda8f2acae94a7e1987bf99400d_153_1.png)

Figure 6.5
Vector Multiplication.
© 2014 Timothy Wright.

### DIV()

```
public Vector2f div( float scalar ) {
    return new Vector2f( x / scalar, y / scalar );
}
```

The div() method is the same as multiplying by one over the scalar. Notice that no
checks are made for dividing by zero.

### LEN() AND LENSQR()

```
public float len() {
    return (float)Math.sqrt( x * x + y * y );
}
```

To find the length of a vector, you use the Pythagorean Theorem. See Figure 6.6.

![](img/588a4cda8f2acae94a7e1987bf99400d_154_0.png)

Figure 6.6
Length of Vector.
© 2014 Timothy Wright.

Single lines are used for the absolute value |a|. Double lines are used for the length of a vector ||a||.

If x > y then x² > y²

```
public float lenSqr() {
    return x * x + y * y;
}
```

Because the square root operation can take many computer cycles, sometimes it is easier to just use the squared length value in comparisons.

### NORM()

```
public Vector2f norm() {
    return div( len() );
}
```

The norm() method returns a normalized vector that has a length of one, as shown in Figure 6.7. Many graphics equations can be simplified by using a vector with a length of one. The little hat (a caret) above the variable in the diagrams indicates a unit vector.

![](img/588a4cda8f2acae94a7e1987bf99400d_154_1.png)

Figure 6.7
Vector Normalization.
© 2014 Timothy Wright.

### PERP()

```
public Vector2f perp() {
    return new Vector2f( -y, x );
}
```

The perp() method returns a new vector that is perpendicular to the current vector. See Figure 6.8. This is useful for creating a normal vector that is needed in many of the equations in the following chapters. Notice that either (-y, x) or (y, -x) produce a perpendicular vector. The upside down T represents a perpendicular vector.

![](img/588a4cda8f2acae94a7e1987bf99400d_155_0.png)

Figure 6.8 Perpendicular Vector. © 2014 Timothy Wright.

### DOT()

```
public float dot( Vector2f v ) {
    return v.x * x + y * v.y;
}
```

The dot() method returns the dot product of two vectors. This method of multiplying two vectors is very useful. As shown in Figure 6.9, the dot product projects one vector onto another, forming a right triangle, which is very helpful when testing object intersections.

![](img/588a4cda8f2acae94a7e1987bf99400d_155_1.png)

Figure 6.9 Dot Product. © 2014 Timothy Wright.

The dot product proof, as illustrated in Figure 6.10, is as follows:

```
A * B = ||A|| ||B|| cos(θA – θB)
A * B = AB [cos(θA) cos(θB) + sin(θA) sin(θB)]
A * B = A cos(θA) B cos(θB) + A sin(θA) B sin(θB)
```

Reviewing Cartesian polar conversions:

```
Ax = A cos(θA)
Bx = B cos(θB)
Ay = A sin(θA)
By = B sin(θB)
A * B = AxBx + AyBy
```

![](img/588a4cda8f2acae94a7e1987bf99400d_156_0.png)

Figure 6.10 Dot Product Angle. © 2014 Timothy Wright.

The dot product has the following mathematical properties:

```
A * B = B * A
C * (A + B) = C * A + C * B
C(A * B) = CA * B
A * A⊥ = 0
```

The last property is important, and is used for the basis of many mathematical proofs. Because the angle between two perpendicular vectors is always zero, their dot product is always zero.

```
A * A⊥ = ||A|| ||A⊥|| cos(90°)
A * A⊥ = ||A|| ||A⊥|| (0)
A * A⊥ = 0
```

The final important point is that the dot product returns a scalar value, not a vector, as shown in Figure 6.11. To project one vector onto another, the vector receiving the projection must be a normal vector and that normal vector needs to be scaled by the dot product.

![](img/588a4cda8f2acae94a7e1987bf99400d_157_0.png)

Figure 6.11
Dot Product Scalar.
© 2014 Timothy Wright.

### ANGLE()

```
public float angle() {
    return (float)Math.atan2( y , x );
}
```

The angle() method returns the angle in radians created by the vector, as shown in Figure 6.12. Notice the atan2() method is used to handle the cases where x is zero, so no additional checks are needed.

![](img/588a4cda8f2acae94a7e1987bf99400d_157_1.png)

Figure 6.12
Angle.
© 2014 Timothy Wright.

### POLAR()

```
public static Vector2f polar( float angle, float radius ) {
    return new Vector2f(
        radius * (float)Math.cos( angle ),
        radius * (float)Math.sin( angle )
    );
}
```

The polar() method takes an angle in radians and a radius and returns a vector with the converted x and y coordinates, as shown in Figure 6.13.

![](img/588a4cda8f2acae94a7e1987bf99400d_158_0.png)

Figure 6.13
Polar.
© 2014 Timothy Wright.

### TOSTRING()

```
@Override
public String toString() {
    return String.format( "(%.2f,%.2f)", x, y );
}
```

The last update is helpful for displaying the vector values as strings for debugging.

```
package javagames.util;

public class Vector2f {
    public float x;
    public float y;
    public float w;

    public Vector2f() {
        this.x = 0.0f;
        this.y = 0.0f;
        this.w = 1.0f;
    }

    public Vector2f(Vector2f v) {
        this.x = v.x;
        this.y = v.y;
        this.w = v.w;
    }

    public Vector2f(float x, float y) {
        this.x = x;
        this.y = y;
        this.w = 1.0f;
    }
}
public Vector2f(float x, float y, float w) {
    this.x = x;
    this.y = y;
    this.w = w;
}

public void translate(float tx, float ty) {
    x += tx;
    y += ty;
}

public void scale(float sx, float sy) {
    x *= sx;
    y *= sy;
}

public void rotate(float rad) {
    float tmp = (float)(x * Math.cos(rad) - y * Math.sin(rad));
    y = (float)(x * Math.sin(rad) + y * Math.cos(rad));
    x = tmp;
}

public void shear(float sx, float sy) {
    float tmp = x + sx * y;
    y += sy * x;
    x = tmp;
}

public Vector2f add(Vector2f v) {
    return new Vector2f(x + v.x, y + v.y);
}

public Vector2f sub(Vector2f v) {
    return new Vector2f(x - v.x, y - v.y);
}

public Vector2f mul(float scalar) {
    return new Vector2f(scalar * x, scalar * y);
}

public Vector2f div(float scalar) {
    return new Vector2f(x / scalar, y / scalar);
}

public Vector2f inv() {
    return new Vector2f(-x, -y);
}

public Vector2f norm() {
```
