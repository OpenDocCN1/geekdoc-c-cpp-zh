
**Inline Exercise 21.2:** Under what conditions on A, B, and C is the rotation ill-defined? Can you think of a situation in a typical interaction where this might be a problem, or will such a problem never arise?

**Inline Exercise 21.3:** ◇ We’ve specified the rotation quite carefully. If A and B are two distinct but non-antipodal points of a sphere, describe the set S of rotations of the sphere that take A to B. Is S a finite set? The space SO(3) of sphere rotations is three-dimensional. Is S a zero-, one-, two-, or three-dimensional subset of it?

In this interaction sequence, a right-click on the object (our demonstration example has only a single object) makes a transparent sphere appear surrounding the object; a first left-click on the sphere initializes a rotation action; and a drag to a new point defines a rotation, which is applied to the object so that it appears to be dragged within the transparent sphere. The mouse release makes the currently applied rotation permanent. By the way, **undragging** (i.e., returning to the starting click point) resets the transformation to its initial value.

In the implementation, we need to do three things.

- 1. Create the transparent sphere and respond to click, drag, and release events there.
- 2. Handle a click event by recording the current transformation on the object, and storing the initially clicked point. It’s best to store this in the frame of reference of the object at the time of clicking.
- 3. Handle drag events by transforming the current mouse position into the frame of the object at initial-click time, and then computing the rotation that takes the initial click to the current mouse position. This rotation is applied to the object, followed by its pre-drag transformation.

There is one tricky problem: What happens when the drag leaves the sphere? For this, we project back onto the sphere: We find the sphere point closest to the eye-through-cursor ray, and pretend that the cursor is there.

With this in mind, let’s look at the code. We start by creating a scene (see Figure 21.8) containing a single manipulable object, a cube. If pick correlation shows a right-click on the cube, we create an interactor to handle the subsequent interactions:

![](img/f464cd0043eb5336aa0543fe20a0561b_631_0.png)

```csharp
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

        // add handlers that forward left-button events to the interactor, if it's not null.

        void Window1_MouseRightButtonDown(object sender, MouseButtonEventArgs e)
        {
            // Check to see if the user clicked on cube1.
            // If so, create a sphere around it.
            ModelVisual3D hit = GetHitTestResult(e.GetPosition(mainViewport));
            if (hit == m_cube1)
            {
                if (interactor == null)
                    interactor = new Interactor(m_cube1, mainViewport, this);
                else
                    endInteraction();
            }
            // if there's already an interactor, delegate to it.
            else if (interactor != null)
            {
                interactor.Cleanup();
                interactor = null;
            }
        }
```

The interactor, just as in the photo-manipulation example, keeps track of the manipulated object (controlled) and the transformation for that object at the start of the manipulation. We also note the viewport from which the object is seen (which allows us to transform mouse clicks into rays from the eye). Initializing the interaction consists of recording the initial transformation on the controlled object, and creating a transparent sphere, centered at the object center. The corresponding cleanup procedure removes the sphere.

```csharp
private void initializeInteraction()
{
    initialTransform = controlled.Transform;
    // find bounds for selected object,
    // locate center and place a sphere there.
    viewport3D.Children.Add(sphere);
}

public void Cleanup()
{
    viewport3D.Children.Remove(sphere);
    initialTransform = null;
}
```

When the user left-clicks on the sphere, we record the current transformation associated to the controlled object and the location of the click. Just as in the photo-manipulation program, we record this position in the coordinate system of the parent of the controlled object. We also record that we are in the midst of a drag operation, and when the left button is released, we reset the drag status.

```csharp
public void mouseLeftButtonDown(System.Windows.Input.MouseButtonEventArgs e)
{
    ModelVisual3D hit = GetHitTestResult(e.GetPosition(viewport3D));
    if (hit != sphere)
        return;
    else if (!inDrag)
    {
        startPoint = spherePointFromMousePosition(e.GetPosition(viewport3D));
        initialTransform = controlled.Transform;
        inDrag = true;
    }
}

public void mouseLeftButtonUp(System.Windows.Input.MouseButtonEventArgs e)
{
    inDrag = false;
}

private Point3D spherePointFromMousePosition(Point mousePoint)
{
    // form a ray from the eye through the mousePoint
    if it hits the sphere
        // return the hit point.
    else // ray misses sphere
        return closest point to ray on the sphere
}
```

product may end up differing from a rotation by a large amount because of round-off errors; the result can (and should!) surprise the user. A solution to this is to accumulate the rotations and then, after perhaps ten are accumulated, reorthogonalize the matrix with the Gram-Schmidt process.

Even with this reprojection onto the set of rotation matrices, the differential form has another drawback. The exact same cursor click-and-drag sequence, executed on two identical scenes, may produce different results. That’s because the mouse motion is sampled by the operating system, and depending on other loads on the machine, the samples may not occur at exactly the same moments. Thus, the two sequences of points used to produce the two sequences of rotations may differ slightly, and the final results will generally differ as well. This is not usually a problem unless the load is rather high so that sampling occurs at a rate that fails to accurately represent the cursor path. For example, if the cursor is moved in a small circle over the course of a half-second, but only two position samples are taken during that time, the results will be very different than if ten samples are taken.

◆ In general, it’s a bad idea to try to numerically integrate differentials, or even very small differences, for the reasons given above. There are two exceptions. First, such an integral may be the only practical way to compute a value. In studying light transport, for example, computing the light arriving at the eye amounts to evaluating an integral, one for which the only known methods are numerical (see Chapter 31). The second is where the summed quantity is known to be an integer; in this case, roundoff errors, if they’re known to be small, can be removed by rounding. (For instance, if you sum four terms and get 3.0000013, you can safely assume that the value is 3.)

### 21.4.2 The Arcball Interface

The arcball interface [Sho92] is exactly like that of the trackball, except that the sphere rotates *twice* as far as the drag would suggest. That is to say, if you drag from *A* to *B*, and they’re 30° apart on the sphere centered at *C*, the object will rotate 60° in the plane of *A*, *B*, and *C*.

This has several practical implications. First, even though we can only see and click on the front half of the sphere, we can perform every possible rotation: Dragging the nearest point to the contour rotates it all the way to the farthest point, for instance. Second, dragging from *P* to *Q*, then *Q* to *R*, then *R* to *P* (where all three are points on the sphere) results in no rotation at all.

In evaluating the arcball, much of what was said about the virtual sphere still holds. If the interaction sphere is textured with some recognizable pattern, such as a world map, then there is some surprise for the user who clicks and drags London: During the drag, London slides out from under the cursor. With a transparent sphere, this effect is largely invisible, however, and the interaction feels quite natural. (If we were to implement a translation-by-dragging interface and translated by twice the drag vector, it would almost certainly be disconcerting to the user, however.)

## 21.5 Mouse-Based Camera Manipulation: Unicam

We now move on to the topic of manipulating the view of a scene. It’s easy to imagine that this is just the same as manipulating an object; after all, the camera
