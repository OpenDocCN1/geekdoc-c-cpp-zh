```
if (!Math::NearZero(mForwardSpeed) || !Math::NearZero(mStrafeSpeed))
{
    Vector3 pos = mOwner->GetPosition();
    pos += mOwner->GetForward() * mForwardSpeed * deltaTime;
    // Update position based on strafe
    pos += mOwner->GetRight() * mStrafeSpeed * deltaTime;
    mOwner->SetPosition(pos);
}
```