```
void BoxComponent::OnUpdateWorldTransform()
{
    // Reset to object space box
    mWorldBox = mObjectBox;
    // Scale
    mWorldBox.mMin *= mOwner->GetScale();
    mWorldBox.mMax *= mOwner->GetScale();
    // Rotate
    if (mOwner->Rotate())
    {
        mWorldBox.Rotate(mOwner->GetRotation());
    }
    // Translate
    mWorldBox.mMin += mOwner->GetPosition();
    mWorldBox.mMax += mOwner->GetPosition();
}
```