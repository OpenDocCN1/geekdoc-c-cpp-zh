```
```glsl
glp = proj_matrix * mv_matrix * vec4(position,1.0);
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
    // ... / lighting computations are unchanged from before
    vec4 mixColor, reflectColor, refractColor, blueColor;
    if (isAbove == 1)
    {
        refractColor = texture(refractTex, (vec2(glp.x,glp.y)/(2.0*glp.w))+0.5);
        reflectColor = texture(reflectTex, (vec2(glp.x,-glp.y)/(2.0*glp.w))+0.5);
        mixColor = (0.2 * refractColor) + (1.0 * reflectColor);
    }
    else
    {
        refractColor = texture(refractTex, (vec2(glp.x,glp.y)/(2.0*glp.w))+0.5);
        blueColor = vec4(0.0, 0.25, 1.0, 1.0);
        mixColor = (0.5 * blueColor) + (0.6 * refractColor);
    }
    color = vec4((mixColor.xyz * (ambient + diffuse) + 0.75*specular), 1.0);
}
```
```

![](bbox=[0.144, 0.588, 0.854, 0.879])

**Figure 15.5**
Reflection and Refraction - camera above the water’s surface (left), and below the water’s surface (right)