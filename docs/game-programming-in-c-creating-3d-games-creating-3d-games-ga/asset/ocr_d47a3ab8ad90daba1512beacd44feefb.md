```
b = mVertices.front() - point;
b.Normalize();
sum += Math::Acos(Vector2::Dot(a, b));
// Return true if approximately 2pi
return Math::NearZero(sum - Math::TwoPi);
}
```

Unfortunately, this angle summation approach is not terribly efficient because it requires several square roots and arccosine calculations. Other, more complex, methods are more efficient. One such method is to draw an infinite ray starting at the point and to then count the number of edges the ray intersects. If the ray intersects an odd number of edges, the point is inside the polygon; otherwise, it's outside. This ray method works for both convex and concave polygons.

# Bounding Volume Tests

It's very common to compute intersection tests between different bounding volumes. For example, imagine that both the player and the wall use AABBs for collision. When the player tries to move forward, you can test if the player's bounding volume intersects with the wall bounding volume. If they intersect, then you can fix the player's position so that they no longer intersect. (You will see how to do this later in this chapter.) This section doesn't cover