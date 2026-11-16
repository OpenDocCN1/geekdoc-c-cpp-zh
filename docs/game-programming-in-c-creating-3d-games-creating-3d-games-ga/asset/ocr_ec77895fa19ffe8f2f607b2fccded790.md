This way you avoid the expensive square root operation. For the most part, you will calculate the distance squared instead of distance throughout this chapter. Listing 10.1 gives the code for this MinDistSq function.

# Listing 10.1 LineSegment::MinDistSq Implementation

Click here to view code image

```
float LineSegment::MinDistSq(const Vector3& point) co
{
    // Construct vectors

    Vector3 ab = mEnd - mStart;

    Vector3 ba = -1.0f * ab;

    Vector3 ac = point - mStart;

    Vector3 bc = point - mEnd;

    // Case 1: C projects prior to A

    if (Vector3::Dot(ab, ac) < 0.0f)
    {

    return ac.LengthSq();
    }

    // Case 2: C projects after B

    else if (Vector3::Dot(ba, bc) < 0.0f)
```