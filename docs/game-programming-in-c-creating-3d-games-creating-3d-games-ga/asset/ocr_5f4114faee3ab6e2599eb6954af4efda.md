SegmentCast can’t simply return after the first intersection. Instead, the function needs to test against all boxes and return the intersection result with the lowest t value, as shown in Listing 10.13. This works because the lowest t value intersection is the one closest to the start of the line segment. SegmentCast uses the segment versus AABB intersection function discussed earlier but now modified to also return the normal of the side the line segment intersects with.

# Listing 10.13 PhysWorld::SegmentCast Implementation

Click here to view code image

```
bool PhysWorld::SegmentCast(const LineSegment& l, Col
{
    bool collided = false;

    // Initialize closestT to infinity, so first
    // intersection will always update closestT
    float closestT = Math::Infinity;
    Vector3 norm;

    // Test against all boxes
    for (auto box : mBoxes)
    {
        float t;
```