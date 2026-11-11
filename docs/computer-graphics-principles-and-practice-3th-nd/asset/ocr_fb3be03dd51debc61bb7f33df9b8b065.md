**Inline Exercise 21.2:** Under what conditions on A, B, and C is the rotation ill-defined? Can you think of a situation in a typical interaction where this might be a problem, or will such a problem never arise?

**Inline Exercise 21.3:** ◇ We’ve specified the rotation quite carefully. If A and B are two distinct but nonantipodal points of a sphere, describe the set S of rotations of the sphere that take A to B. Is S a finite set? The space SO(3) of sphere rotations is three-dimensional. Is S a zero-, one-, two-, or three-dimensional subset of it?

In this interaction sequence, a right-click on the object (our demonstration example has only a single object) makes a transparent sphere appear surrounding the object; a first left-click on the sphere initializes a rotation action; and a drag to a new point defines a rotation, which is applied to the object so that it appears to be dragged within the transparent sphere. The mouse release makes the currently applied rotation permanent. By the way, **undragging** (i.e., returning to the starting click point) resets the transformation to its initial value.
In the implementation, we need to do three things.

+   1. Create the transparent sphere and respond to click, drag, and release events there.
+   2. Handle a click event by recording the current transformation on the object, and storing the initially clicked point. It’s best to store this in the frame of reference of the object at the time of clicking.
+   3. Handle drag events by transforming the current mouse position into the frame of the object at initial-click time, and then computing the rotation that takes the initial click to the current mouse position. This rotation is applied to the object, followed by its pre-drag transformation.

There is one tricky problem: What happens when the drag leaves the sphere? For this, we project back onto the sphere: We find the sphere point closest to the eye-through-cursor ray, and pretend that the cursor is there.

With this in mind, let’s look at the code. We start by creating a scene (see Figure 21.8) containing a single manipulable object, a cube. If pick correlation shows a right-click on the cube, we create an interactor to handle the subsequent interactions:

![](bbox=[0.71, 0.472, 0.951, 0.643])

```
    public partial class Window1 : Window
    {
        private RotateTransform3D m_cubeRotation = new RotateTransform3D();
        private ModelVisual3D m_cube1;
        private Interactor interactor = null;
        public Window1()
        {
            // initialize, and build a ground and two walls
            m_cube1 = a cube model;
            m_cube1.Transform = new TranslateTransform3D(4, .5, 1);
            mainViewport.Children.Add(m_cube1);

            this.MouseRightButtonDown +=
                new MouseButtonEventHandler(Window1_MouseRightButtonDown);
        }
```