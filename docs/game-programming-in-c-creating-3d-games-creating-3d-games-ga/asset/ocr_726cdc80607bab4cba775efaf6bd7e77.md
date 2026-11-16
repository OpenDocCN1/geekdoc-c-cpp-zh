```
```cpp
bool TestSidePlane(float start, float end, float negd,
                   std::vector<float>& out)
{
    float denom = end - start;
    if (Math::NearZero(denom))
    {
        return false;
    }
    else
    {
        float numer = -start + negd;
        float t = numer / denom;
        // Test that t is within bounds
        if (t >= 0.0f && t <= 1.0f)
        {
            out.emplace_back(t);
            return true;
        }
        else
            return false;
    }
}
```
```