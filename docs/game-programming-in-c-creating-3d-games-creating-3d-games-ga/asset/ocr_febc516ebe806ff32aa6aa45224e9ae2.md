Since the homogenous coordinates for 3D are (x, y, z, w), you need a 4×4 matrix.

The Boolean tracks whether you need to recalculate the world transform matrix. The idea is that you want to recalculate the world transform only if the actor's position, scale, or rotation changes. In each of the setter functions for the position, scale, and rotation of the actor, you set mRecomputeWorldTransform to true. This way, whenever you change these component properties, you'll be sure to compute the world transform again.

You also initialize mRecomputeWorldTransform to true in the constructor, which guarantees to compute the world transform at least once for each actor.

Next, implement a CreateWorldTransform function, as follows:

Click here to view code image

```
void Actor::ComputeWorldTransform()
{
    if (mRecomputeWorldTransform)
    {
        mRecomputeWorldTransform = false;

        // Scale, then rotate, then translate

        mWorldTransform = Matrix4::CreateScale(mScale);
```