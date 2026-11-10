```
```glsl
shadowFactor += lookup(-1.5*swidth + offset.x, -0.5*swidth - offset.y);
shadowFactor += lookup(0.5*swidth + offset.x, 1.5*swidth - offset.y);
shadowFactor += lookup(0.5*swidth + offset.x, -0.5*swidth - offset.y);
shadowFactor = shadowFactor / 4.0;  // shadowFactor is an average of the four sampled points

// ----- this section, if un-commented, produces a 64-sample hi resolution soft shadow
// float swidth = 2.5;       // tunable amount of shadow spread
// float endp = swidth*3.0 + swidth/2.0;
// for (float m=-endp; m<=endp; m=m+swidth)
// {
//     for (float n=-endp; n<=endp; n=n+swidth)
//     {
//         shadowFactor += lookup(m,n);
//     }
// }
// shadowFactor = shadowFactor / 64.0;

vec4 shadowColor = globalAmbient * material.ambient + light.ambient * material.ambient;

vec4 lightedColor = light.diffuse * material.diffuse * max(dot(L,N),0.0)
                  + light.specular * material.specular
                  * pow(max(dot(H,N),0.0),material.shininess*3.0);

fragColor = vec4((shadowColor.xyz + shadowFactor*(lightedColor.xyz)),1.0);
}
```
```

The fragment shader shown in Program 8.2 contains code for both the 4-sample and 64-sample PCF soft shadows. First, a function lookup() is defined to make the sampling process more convenient. It makes a call to the GLSL function textureProj() that does a lookup in the shadow texture, but offset by a specified amount (ox,oy). The offset is multiplied by 1/windowSize, which here we have simply hardcoded to .001 assuming a window size of 1000×1000 pixels.²

The 4-sample dithered computation appears highlighted in main() and follows the algorithm described in the previous section. A scale factor swidth has been added that can be used to adjust the size of the “soft” region at the edge of the shadows.

The 64-sample code follows, and is commented out. It can be used instead of the 4-sample computation, by uncommenting it and instead commenting out the 4-sample code. The swidth scale factor in the 64-sample code is used as a step size in the nested loop that samples points at various distances from the

² We have also multiplied the offset by the w component of the shadow coordinate, because OpenGL automatically divides the input coordinate by w during texture lookup. This operation, called *perspective divide*, is one which we have ignored up to this point. It must be accounted for here. For more information on *perspective divide*, see [LO12].