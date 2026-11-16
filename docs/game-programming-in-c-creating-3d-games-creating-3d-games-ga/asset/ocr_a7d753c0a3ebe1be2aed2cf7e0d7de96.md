```
mGBuffer = new GBuffer();
int width = static_cast<int>(mScreenWidth);
int height = static_cast<int>(mScreenHeight);
if (!mGBuffer->Create(width, height))
{
    SDL_Log("Failed to create G-buffer.");
    return false;
}
```