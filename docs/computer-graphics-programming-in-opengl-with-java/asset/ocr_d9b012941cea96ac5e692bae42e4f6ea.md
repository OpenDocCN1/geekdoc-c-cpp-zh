```
```glsl
gl.glClear(GL_COLOR_BUFFER_BIT);
...
// draw water top (surface)
prepForTopSurfaceRender();
gl.glActiveTexture(GL_TEXTURE0);
gl.glBindTexture(GL_TEXTURE_2D, refractTextureId);
gl.glActiveTexture(GL_TEXTURE1);
gl.glBindTexture(GL_TEXTURE_2D, refractTextureId);

// the remainder of display() is identical to that shown in part one
...
}
```
```

# Vertex Shader (for top surface)

```
```glsl
...
out vec4 glp;
...
void main(void)
{
    ...
    glp = p_matrix * v_matrix * m_matrix * vec4(position,1.0);
    gl_Position = glp;
}
```
```

# Fragment Shader (for top surface)

```
```glsl
...
in vec4 glp;
uniform int isAbove;

void main(void)
{
    ... // lighting computations are unchanged from before
    vec4 mixColor, reflectColor, refractColor, blueColor;
    if (isAbove == 1)
    {
        refractColor = texture(refractTex, (vec2(glp.x,glp.y)/(2.0*glp.w)+0.5));
        reflectColor = texture(reflectTex, (vec2(glp.x,glp.y)/(2.0*glp.w)+0.5));
        mixColor = (0.2 * refractColor) + (1.0 * reflectColor);
    }
    else
    {
        refractColor = texture(refractTex, (vec2(glp.x,glp.y)/(2.0*glp.w)+0.5));
        blueColor = vec4(0.0, 0.25, 1.0, 1.0);
        mixColor = (0.5 * blueColor) + (0.6 * refractColor);
    }
    color = vec4((mixColor.xyz * (ambient + diffuse) + 0.75*specular), 1.0);
}
```
```