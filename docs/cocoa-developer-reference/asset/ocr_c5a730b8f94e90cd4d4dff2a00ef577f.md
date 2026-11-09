Key features of the code include:

+   - The code is still using an animator.
+   - The default animation object is replaced by an instance of CAKeyFrameAnimation.
+   - The calculationMode property is used to pace the animation, creating a more natural look.
+   - A timing function is applied to the path as a whole. The animation code automatically applies the timing function as it calculates each point on the path.
+   - The path is created with the Core Graphics CGPathCreateMutable() function.
+   - The starting point is set with CGPathMoveToPoint(), which takes a path pointer, an optional transformation matrix which isn't used here, and two points.
+   - A curve segment is added with CGPathAddCurveToPoint(), which takes four control points and is very similar to NSBezierPath.
+   - The path is recalculated for each mouse click, using the current and previous mouse values.
+   - The path is assigned to the animation object's path property.

The complex path adds a wiggle to the animation, illustrated in Figure 17.4.

**Figure 17.4**

An animation with a custom path. The animated object wiggles its way from the starting point to the destination. This simple path is created with a single curved path segment. But it could be made arbitrarily complex, with many subpaths.

![](bbox=[0.18, 0.55, 0.57, 0.87])