```
// Call parent update (doesn't do anything right r
CameraComponent::Update(deltaTime);
// Camera position is owner position
Vector3 cameraPos = mOwner->GetPosition();

// Update pitch based on pitch speed
mPitch += mPitchSpeed * deltaTime;
// Clamp pitch to [-max, +max]
mPitch = Math::Clamp(mPitch, -mMaxPitch, mMaxPitch
// Make a quaternion representing pitch rotation,
// which is about owner's right vector
Quaternion q(mOwner->GetRight(), mPitch);

// Rotate owner forward by pitch quaternion
Vector3 viewForward = Vector3::Transform(
    mOwner->GetForward(), q);
// Target position 100 units in front of view for
Vector3 target = cameraPos + viewForward * 100.0f;
// Also rotate up by pitch quaternion
Vector3 up = Vector3::Transform(Vector3::UnitZ, q
```