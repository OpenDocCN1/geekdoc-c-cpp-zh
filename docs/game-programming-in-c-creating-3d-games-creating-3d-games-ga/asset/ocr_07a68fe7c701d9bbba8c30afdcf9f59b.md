```
```cpp
}
else
{
    disc = Math::Sqrt(disc);
    // Compute min and max solutions of t
    float tMin = (-b - disc) / (2.0f * a);
    float tMax = (-b + disc) / (2.0f * a);
    // Check whether either t is within bounds of segment
    if (tMin >= 0.0f && tMin <= 1.0f)
    {
        outT = tMin;
        return true;
    }
    else if (tMax >= 0.0f && tMax <= 1.0f)
    {
        outT = tMax;
        return true;
    }
    else
    {
        return false;
    }
}
```
```