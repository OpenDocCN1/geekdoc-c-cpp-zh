
Vector3 cameraPos = target + mOffset;

Matrix4x4 view = Matrix4x4::CreateLookAt(cameraPos, target, up);

SetViewMatrix(view);
}

For the look-at matrix, the target position of the camera is simply the owner's position, the camera position is the owner's position plus the offset, and the up is the camera up. This yields the final orbited camera. Figure 9.5 demonstrates the orbit camera with the car as the target.

![](img/e9afcec1487716b0ef80d7e7c09869c8_623_0.png)

Figure 9.5 Orbit camera focused on the car

## SPLINE CAMERA

A spline is a mathematical representation of a curve specified by a series of points on the curve. Splines are popular in games because they enable an object to smoothly move along a curve over some period. This can be very useful for a cutscene camera because the camera can follow a predefined spline path. This type of camera also sees use in games like God of War, where the camera follows along a set path as the player progresses through the world.

The Catmull-Rom spline is a type of spline that's relatively simple to compute, and it is therefore used frequently in games and computer graphics. This type of spline minimally requires four control points, named P0 through P3. The actual curve runs from P1 to P2, while P0 is a control point prior to the curve and P3 is a control point after the curve. For best results, you can space these control points roughly evenly along the curve—and you can approximate this with Euclidean distance. Figure 9.6 illustrates a Catmull-Rom spline with four control points.

![](img/e9afcec1487716b0ef80d7e7c09869c8_624_0.png)

Given these four control points, you can express the position between P1 and P2 as the following parametric equation, where t = 0 is at P1 and t = 1 is at P2:

```
p(t) = 0.5
· (2P1 + (-P0 + P2) t
+ (2P0 - 5P1 + 4P2 - P3) t³)
```

Although the Catmull-Rom spline equation has only four control points, you can extend the spline to any arbitrary number of control points. This works provided that there still is one point before the path and one point after the path because those control points are not part of the path. In other words, you need n + 2 points to represent a curve of n points. You can then take any sequence of four neighboring points and substitute them into the spline equation.

To implement a camera that follows a spline path, you first create a struct to define a spline. The only member data `Spline` needs is a vector of the control points:

Click here to view code image

```
struct Spline
{

// Control points for spline

// (Requires n + 2 points where n is number
// of points in segment)
    std::vector<Vector3> mControlPoints;

// Given spline segment where startIdx = P1,
// compute position based on t value

Vector3 Compute(size_t startIdx, float t) const;

size_t GetNumPoints() const { return mControlPoints.size(); }
};
```

The `Spline::Compute` function applies the spline equation given a start index corresponding to $P_1$ and a $t$ value in the range [0.0, 1.0]. It also performs boundary checks to make sure `startIdx` is a valid index, as shown in Listing 9.7.

## Listing 9.7 Spline::Compute Implementation

Click here to view code image

```
Vector3 Spline::Compute(size_t startIdx, float t) const
{

// Check if startIdx is out of bounds
if (startIdx >= mControlPoints.size())
{ return mControlPoints.back(); } 

else if (startIdx == 0)
{ return mControlPoints[startIdx]; }

else if (startIdx + 2 >= mControlPoints.size())
{ return mControlPoints[startIdx]; }

// Get p0 through p3
Vector3 p0 = mControlPoints[startIdx - 1];
Vector3 p1 = mControlPoints[startIdx];
Vector3 p2 = mControlPoints[startIdx + 1];
Vector3 p3 = mControlPoints[startIdx + 2];

// Compute position according to Catmull-Rom equation
Vector3 position = 0.5f * ((2.0f * p1) + (-p0 + p2) * t +
        (2.0f * p0 - 5.0f * p1 + 4.0f * p2 - p3) * t * t +
        (-p0 + 3.0f * p1 - 3.0f * p2 + p3) * t * t * t);
return position;
}
```

The SplineCamera class then needs a Spline in its member data. In addition, it tracks the current index corresponding to P1, the current t value, a speed, and whether the camera should move along the path:

Click here to view code image

```
// Spline path camera follows
Spline mPath;
// Current control point index and t
size_t mIndex;
float mT;
// Amount t changes/sec
float mSpeed;
// Whether to move the camera along the path
bool mPaused;
```

The spline camera updates by first increasing the $t$ value as a function of speed and delta time. If the $t$ value is greater than or equal to 1.0, $P_1$ advances to the next point on the path (assuming that there are enough points on the path). Advancing $P_1$ also means you must subtract 1 from the $t$ value. If the spline has no more points, the spline camera pauses.

For the camera calculations, the position of the camera is simply the point computed from the spline. To compute the target point, you increase $t$ by a small delta to determine the direction the spline camera is moving. Finally, the up vector stays at (0, 0, 1), which assumes that you do not want the spline to flip upside down. Listing 9.8 gives the code for `SplineCamera::Update`, and Figure 9.7 shows the spline camera in action.

![](img/e9afcec1487716b0ef80d7e7c09869c8_629_0.png)

Figure 9.7 Spline camera in a game

## Listing 9.8 SplineCamera::Update Implementation

Click here to view code image

```
void SplineCamera::Update(float deltaTime)
{
    CameraComponent::Update(deltaTime);

    // Update t value
    if (!mPaused)
    {
        mT += mSpeed * deltaTime;
    }

    // Advance to the next control point if needed.
    // This assumes speed isn't so fast that you just
    // move multiple control points in one frame.
    if (mT >= 1.0f)
    {
        // Make sure we have enough points to advance
        if (mIndex < mPath.GetNumPoints() - 3)
        {
            mIndex++;
            mT = mT - 1.0f;
        }
        else
        {
            // Path's done, so pause
            mPaused = true;
        }
    }

    // Camera position is the spline at the current t value
    Vector3 cameraPos = mPath.Compute(mIndex, mT);

    // Target point is just a small delta ahead on the spline
    Vector3 target = mPath.Compute(mIndex, mT + 0.01f);

    // Assume spline doesn't flip upside-down
    const Vector3 up = Vector3::UnitZ;

    Matrix4 view = Matrix4::CreateLookAt(cameraPos, target, up);
    SetViewMatrix(view);
}
```

## UNPROJECTION

Given a point in world space, to transform it into clip space, you first multiply by the view matrix followed by the projection matrix. Imagine that the player in a first-person shooter wants to fire a projectile based on the screen position of the aiming reticule. In this case, the aiming reticule position is a coordinate in screen space, but to correctly fire the projectile, you need a position in world space. An **unprojection** is a calculation that takes in a screen space coordinate and converts it into a world space coordinate.

Assuming the screen space coordinate system described in Chapter 5, “OpenGL,” the center of the screen is (0, 0), the top-left corner is (-512, 384), and the bottom-right corner is (512, -384). The first step to calculating an unprojection is converting a screen space coordinate into a normalized device coordinate with a range of [-1, 1] for both the x and y components:

```
ndcX = screenX / 512
ndcY = screenY / 384
```

However, the issue is that any single (x, y) coordinate can correspond to any z coordinate in the range [0, 1], where 0 is a point on the near plane (right in front of the camera), and 1 is a point on the far plane (the maximum distance you can see from the camera). So, to correctly perform the unprojection, you also need a z component in the range [0, 1]. You then represent this as a homogeneous coordinate:

```
ndc = (ndcX, ndcY, z, 1)
```

Now you construct an unprojection matrix, which is simply the inverse of the view-projection matrix:

```
Unprojection = (View * Projection)^-1
```

When multiplying the NDC point by the unprojection matrix, the w component changes. However, you need to renormalize the w component (setting it back to 1) by dividing each component by w. This yields the following calculation for the point in world space:

```
temp = ndc * Unprojection
worldPos = temp / temp_w
```

You add a function for an unprojection into the
