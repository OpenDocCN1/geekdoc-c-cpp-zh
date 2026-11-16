```
void SpriteComponent::Draw(Shader* shader)
{
    // Scale the quad by the width/height of texture
    Matrix4x4 scaleMat = Matrix4x4::CreateScale(
        static_cast<float>(mTexWidth),
        static_cast<float>(mTexHeight),
        1.0f);
    Matrix4x4 world = scaleMat * mOwner->GetWorldTransform();
    // Set world transform
    shader->SetMatrixUniform("mWorldTransform", world);
    // Draw quad
    glDrawElements(GL_TRIANGLES, 6, GL_UNSIGNED_INT, nullptr);
}
```