```
```cpp
float SkeletalMeshComponent::PlayAnimation(const Animation* anim,
    float playRate)
{
    mAnimation = anim;
    mAnimTime = 0.0f;
    mAnimPlayRate = playRate;

    if (!mAnimation) { return 0.0f; }
    ComputeMatrixPalette();

    return mAnimation->GetDuration();
}
```
```