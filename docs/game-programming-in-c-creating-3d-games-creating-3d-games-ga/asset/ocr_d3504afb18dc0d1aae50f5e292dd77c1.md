```
Plane::Plane(const Vector3& a, const Vector3& b, const Vector3& c)
{
    // Compute vectors from a to b and a to c
    Vector3 ab = b - a;
    Vector3 ac = c - a;

    // Cross product and normalize to get normal
    mNormal = Vector3::Cross(ab, ac);
    mNormal.Normalize();

    // d = -P * Normal
    md = -Vector3::Dot(a, mNormal);
}
```