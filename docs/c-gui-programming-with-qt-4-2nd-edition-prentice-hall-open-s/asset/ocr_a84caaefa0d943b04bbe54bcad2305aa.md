these use built-in brush patterns (Qt::SolidPattern, Qt::NoBrush). In modern applications, gradients are popular alternative to monochrome fill patterns. Gradients rely on color interpolation to obtain smooth transitions between two or more colors. They are frequently used to produce 3D effects; for example, the Plastique and Cleanlooks styles use gradients to render QPushButton.

Qt supports three types of gradients: linear, conical, and radial. The Oven Timer example in the next section combines all types of gradients in a single widget to make it look like the real thing.

+   Linear gradients are defined by two control points and by a series of "color stops" on the line that connects these two points. For example, the linear gradient in Figure 8.6 that is created using the following code:

```
QLinearGradient gradient(50, 100, 300, 350);
gradientsetColorAt(0.0, Qt::white);
gradientsetColorAt(0.2, Qt::green);
gradientsetColorAt(1.0, Qt::black);
```

# Figure 8.6. QPainter's gradient brushes

![](bbox=[0.057, 0.463, 0.736, 0.793])

We specify three colors at different positions between the two control points. Positions are specified as floating-point values between 0 and 1, where 0 corresponds to the first control point and 1 to the second control point. Colors between the specified stops are linearly interpolated.

+   Radial gradients are defined by a center point (Xc, Yc), a radius r, and a focal point (xf, yf), in addition to the color stops. The center point and the radius specify a circle. The colors spread outward from the focal point, which can be