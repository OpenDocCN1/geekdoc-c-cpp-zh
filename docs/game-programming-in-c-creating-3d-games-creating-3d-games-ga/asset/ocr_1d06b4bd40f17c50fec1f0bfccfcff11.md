```
bool Intersect(const LineSegment& l, const AABB& b, float& outT)
{
    // Vector to save all possible t values
    std::vector<float> tValues;
    // Test the x planes
    TestSidePlane(l.mStart.x, l.mEnd.x, b.mMin.x, tValues);
    TestSidePlane(l.mStart.x, l.mEnd.x, b.mMax.x, tValues);
    // Test the y planes
    TestSidePlane(l.mStart.y, l.mEnd.y, b.mMin.y, tValues);
    TestSidePlane(l.mStart.y, l.mEnd.y, b.mMax.y, tValues);
    // Test the z planes
    TestSidePlane(l.mStart.z, l.mEnd.z, b.mMin.z, tValues);
    TestSidePlane(l.mStart.z, l.mEnd.z, b.mMax.z, tValues);
```