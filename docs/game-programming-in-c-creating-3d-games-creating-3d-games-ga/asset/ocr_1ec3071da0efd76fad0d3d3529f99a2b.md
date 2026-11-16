```
Matrix4 viewProj = Matrix4::CreateSimpleViewProj(1024.f, 768.f);
mShader.SetMatrixUniform("uViewProj", viewProj);
```