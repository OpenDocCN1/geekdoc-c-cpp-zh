```
{
    return bc.LengthSq();
}

// Case 3: C projects onto line
else
{
    // Compute p

    float scalar = Vector3::Dot(ac, ab)
    // Vector3::Dot(ab, ab);
    Vector3 p = scalar * ab;

    // Compute length squared of ac - p
    return (ac - p).LengthSq();
}
}
```

# # Planes

A **plane** is a flat, two-dimensional surface that extends infinitely, much as a line is a one-dimensional object that extends infinitely. In a game, you may use a plane as an abstraction for the ground or walls. The equation of a plane is as follows:

P·n̂+d=0

P·n̂+d=0