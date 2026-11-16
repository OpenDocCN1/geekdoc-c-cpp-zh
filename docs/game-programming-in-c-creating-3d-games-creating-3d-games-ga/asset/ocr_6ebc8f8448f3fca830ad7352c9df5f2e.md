```
void HUD::UpdateCrosshair(float deltaTime)
{
    // Reset to regular cursor
    mTargetEnemy = false;
    // Make a line segment
    const float AimDist = 5000.0f;
    Vector3 start, dir;
    mOwner->GetScreenDirection(start, dir);
    LineSegment l(start, start + dir * AimDist);
    // Segment cast
    PhysWorld::CollisionInfo info;
    if (mGame->GetPhysWorld()->SegmentCast(l, info)
    {
        // Check if this actor has a target component
        for (auto tc : mTargetComps)
        {
            if (tc->GetOwner() == info.mActor)
            {
                mTargetEnemy = true;
                break;
            }
        }
    }
}
```