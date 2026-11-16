```
```cpp
Vector3 Actor::GetRight() const
{
    // Rotate right axis using quaternion rotation
    return Vector3::Transform(Vector3::UnitY, mRotation);
}
```
```