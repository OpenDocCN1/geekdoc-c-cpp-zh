```
struct Spline
{
    // Control points for spline
    // (Requires n+2 points where n is number
    //  of points in segment)
    std::vector<Vector3> mControlPoints;

    // Given spline segment where startIdx = P1,
    //  compute position based on t value
    Vector3 Compute(size_t startIdx, float t) const;
    size_t GetNumPoints() const { return mControlPoints.size(); }
};
```