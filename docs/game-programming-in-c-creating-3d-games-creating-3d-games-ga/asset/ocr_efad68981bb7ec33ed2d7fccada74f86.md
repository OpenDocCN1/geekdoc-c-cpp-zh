```
bool Intersect(const LineSegment& l, const Plane& p, float& outT)
{
    // First test if there's a solution for t
    float denom = Vector3::dot(l.mEnd - l.mStart,
                               p.mNormal);
    if (Math::NearZero(denom))
    {
        // The only way they intersect if start/end are
        // points on the plane (P dot N) == d
        if (Math::NearZero(Vector3::dot(l.mStart, p.mNormal) - p.mD))
        {
            outT = 0.0f;
            return true;
        }
        else
        { return false; }
    }
}
```