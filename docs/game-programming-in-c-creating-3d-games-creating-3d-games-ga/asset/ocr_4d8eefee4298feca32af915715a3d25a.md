texture. You then multiply this by the owning actor's world transform matrix to create the desired world transform matrix for the sprite. Next, call SetMatrixUniform to set the uWorldTransform in the vertex shader program. Finally, you draw the triangles as before, with glDrawElements.

# Listing 5.13 Current Implementation of SpriteComponent :: Draw

Click here to view code image

```
void SpriteComponent::Draw(Shader* shader)
{
    // Scale the quad by the width/height of texture
    Matrix4 scaleMat = Matrix4::CreateScale(
        static_cast<float>(mTexWidth),
        static_cast<float>(mTexHeight),
        1.0f);

    Matrix4 world = scaleMat * mOwner->GetWorldTransform();

    // Set world transform
    shader->SetMatrixUniform("uWorldTransform", world);

    // Draw quad
    glDrawElements(GL_TRIANGLES, 6, GL_UNSIGNED_INT, r
```