```
vec4 pos = vec4(inPosition, 1.0);

// Transform position to world space, then clip sp
gl_Position = pos * uWorldTransform * uViewProj;

// Pass along the texture coordinate to frag shade
fragTexCoord = inTexCoord;
}
```

# The Sprite.frag Shader

As a rule, any out variables in the vertex shader should have a corresponding in in the fragment shader. The name and type of the in variable in the fragment shader must have the same name and type as the corresponding out variable in the vertex shader:

```
in vec4 fragTexCoord;
```

Next, you need to add a uniform for a texture sampler (that can get the color from a texture given a texture coordinate):

```
uniform sampler2D uTexture;
```

The sampler2D type is a special type that can sample 2D textures. Unlike with the world transform and view-