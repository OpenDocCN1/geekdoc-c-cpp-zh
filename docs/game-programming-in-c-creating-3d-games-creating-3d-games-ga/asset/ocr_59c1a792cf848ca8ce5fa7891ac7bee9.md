First, the `TurnTo` function in `NavComponent` rotates the actor to face a point:

Click here to view code image

```
void NavComponent::TurnTo(const Vector2& pos)
{
    // Vector from me to pos
    Vector2 dir = pos - mOwner->GetPosition();
    // New angle is just atan2 of this dir vector
    // (Negate y because +y is down on screen)
    float angle = Math::Atan2(-dir.y, dir.x);
    mOwner->SetRotation(angle);
}
```

Next, `NavComponent` has a `mNextPoint` variable that tracks the next point in the path. The `Update` function tests whether the actor reaches `mNextPoint`:

Click here to view code image

```
void NavComponent::Update(float deltaTime)
{
    // If you've reached the next point, advance along
    Vector2 diff = mOwner->GetPosition() - mNextPoint;
```