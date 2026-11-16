```
// For texture sampling

uniform sampler2D uTexture;

void main()
{
    // Sample color from texture
    outColor = texture(uTexture, fragTexCoord);
}
```

You then change the code in Game::LoadShaders to now load Sprite.vert and Sprite.frag. The previous code inside the various actors that set textures on SpriteComponents now also successfully loads the textures with SOIL. With this code, you can now draw sprites with texture mapping, as shown in Figure 5.12. Unfortunately, there's still one last issue to fix. Right now, the code is drawing black for pixels that should be transparent.