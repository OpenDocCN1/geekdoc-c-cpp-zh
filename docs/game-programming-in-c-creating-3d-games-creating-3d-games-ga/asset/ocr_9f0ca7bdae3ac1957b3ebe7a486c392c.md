```
if (diff.Length() <= 2.0f)
{
    mNextPoint = GetNextPoint();
    TurnTo(mNextPoint);
}
// This moves the actor forward
MoveComponent::Update(deltaTime);
}
```

This assumes that the `GetNextPoint` function returns the next point on the path. Assuming that the actor starts at the first point on the path, initializing `mNextPoint` to the second point as well as setting a linear speed gets the actor moving along the path.

There's one issue with updating the movement along the path in this way: It assumes that the actor is not moving so fast that it jumps too far past a node in one step. If this happens, the distance between the two will never be close enough, and the actor will get lost.

# Other Graph Representations

For a game with real-time action, non-player characters (NPCs) usually don't move from square to square on a grid. This makes it more complex to represent the world with a graph. This section