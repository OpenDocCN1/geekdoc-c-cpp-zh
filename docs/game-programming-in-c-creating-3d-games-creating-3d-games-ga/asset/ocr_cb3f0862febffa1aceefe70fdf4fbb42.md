# UpdateMinMax:

# Click here to view code image

```
// Assume points is a std::vector<Vector3>

AABB box(points[0], points[0]);

for (size_t i = 1; i < points.size(); i++)
{
    box.UpdateMinMax(points[i]);
}
```

Because an AABB must keep its sides parallel to the coordinate planes, rotating an object does not rotate the AABB. Instead, it changes the dimensions of the AABB, as in Figure 10.4. In some cases, it may be desirable not to compute AABB rotations. For example, most humanoid characters in games only rotate about the up axis. If you make the AABB for the character wide enough, rotating the character does not change the AABB enough to warrant rotating the AABB (though watch out for animations that move the character too much).
However, for other objects, it is necessary to compute a rotated AABB.