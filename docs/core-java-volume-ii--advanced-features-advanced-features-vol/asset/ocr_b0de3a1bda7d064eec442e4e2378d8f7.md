# java.awt.geom.AffineTransform 1.2 *(Continued)*

+   - `static AffineTransform getShearInstance(double shx, double shy)`  
+     creates a shear transformation that shears the *x* axis by `shx` and the *y* axis by `shy`. The transformation matrix is:
+   
+     ```
+     [ 1   shx  0 ]
+     [ shy  1   0 ]
+     [ 0    0   1 ]
+     ```
+   
+   - `static AffineTransform getTranslateInstance(double tx, double ty)`  
+     creates a translation transformation that moves the *x* axis by `tx` and the *y* axis by `ty`. The transformation matrix is:
+   
+     ```
+     [ 1   0   tx ]
+     [ 0   1   ty ]
+     [ 0   0   1  ]
+     ```
+   
+   - `void setToRotation(double a)`
+   - `void setToRotation(double a, double x, double y)`
+   - `void setToScale(double sx, double sy)`
+   - `void setToShear(double shx, double shy)`
+   - `void setToTranslation(double tx, double ty)`  
+     sets this affine transformation to a basic transformation with the given parameters. See the `getXxxInstance` methods for an explanation of the basic transformations and their parameters.

# java.awt.Graphics2D 1.2

+   - `void setTransform(AffineTransform t)`  
+     replaces the existing coordinate transformation of this graphics context with `t`.
+   - `void transform(AffineTransform t)`  
+     composes the existing coordinate transformation of this graphics context with `t`.
+   - `void rotate(double a)`
+   - `void rotate(double a, double x, double y)`
+   - `void scale(double sx, double sy)`
+   - `void shear(double sx, double sy)`
+   - `void translate(double tx, double ty)`  
+     composes the existing coordinate transformation of this graphics context with a basic transformation with the given parameters. See the `AffineTransform.getXxxInstance` methods for an explanation of the basic transformations and their parameters.