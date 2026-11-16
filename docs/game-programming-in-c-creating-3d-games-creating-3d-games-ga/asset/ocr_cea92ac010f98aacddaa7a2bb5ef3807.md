This variable is called mSpriteShader because,
ultimately, you'll use it to draw sprites. The
LoadShaders function loads in the shader files and sets
the shader as active:

# Click here to view code image

```
bool Game::LoadShaders()
{
    mSpriteShader = new Shader();
    if (!mSpriteShader->Load("Shaders/Basic.vert", "Sh
    {
        return false;
    }
    mSpriteShader->SetActive();
}
```

You call LoadShaders in Game::Initialize
immediately after finishing initialization of OpenGL and
GLEW (and before you create the mSpriteVerts vertex
array object).

After you've created simple vertex and pixel shaders and
loaded in triangles, you can finally try to draw some
triangles.