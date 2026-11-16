this sequence of vertices to define an AABB for the model. To do this, you can create a new function called `UpdateMinMax` that takes in a point and updates min and max, accounting for this point:

Click here to view code image

```
void AABB::UpdateMinMax(const Vector3& point)
{
    // Update each component separately
    mMin.x = Math::Min(mMin.x, point.x);
    mMin.y = Math::Min(mMin.y, point.y);
    mMin.z = Math::Min(mMin.z, point.z);
    mMax.x = Math::Max(mMax.x, point.x);
    mMax.y = Math::Max(mMax.y, point.y);
    mMax.z = Math::Max(mMax.z, point.z);
}
```

Because you do not know where the new point is in relation to all the other points, you must test every component independently to decide which components of min and max should update.

Then, given a container of points, you first initialize min and max of the AABB to the first point in the container. For each remaining point, you simply call