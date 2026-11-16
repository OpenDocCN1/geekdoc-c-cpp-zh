requires several steps. First, you invert the view matrix. Given this inverted view matrix, the first three components of the fourth row (returned by GetTranslation) correspond to the world space position of the camera. The first three components of the third row (returned by GetZAxis) correspond to the forward vector, and the first three components of the second row (returned by GetYAxis) correspond to the up vector. You use VecToFMOD on all three of these vectors to convert them to the FMOD coordinate system.

# Listing 7.6 AudioSystem::SetListener Implementation

Click here to view code image

```
void AudioSystem::SetListener(const Matrix4& viewMatr
{
    // Invert the view matrix to get the correct vector
    Matrix4 invView = viewMatrix;
    invView.Invert();
    FMOD_3D_ATTRIBUTES listener;
    // Set position, forward, up
    listener.position = VecToFMOD(invView.GetTranslati
    // In the inverted view, third row is forward
    listener.forward = VecToFMOD(invView.GetZAxis()));
```