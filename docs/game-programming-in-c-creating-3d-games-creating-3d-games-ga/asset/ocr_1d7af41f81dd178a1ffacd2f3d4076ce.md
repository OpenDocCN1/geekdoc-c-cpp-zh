```
```cpp
void Game::GenerateOutput()
{
    // Set the clear color to gray
    glClearColor(0.86f, 0.86f, 0.86f, 1.0f);

    // Clear the color buffer
    glClear(GL_COLOR_BUFFER_BIT);

    // Set sprite shader and vertex array objects active
    mSpriteShader->SetActive();
    mSpriteVerts->SetActive();

    // Draw all sprites
    for (auto sprite : mSprites)
        sprite->Draw(mSpriteShader);
    }

    // Swap the buffers
    SDL_GL_SwapWindow(mWindow);

    return true;
}
```
```