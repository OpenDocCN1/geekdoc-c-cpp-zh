
## 11.5 USER-DEFINED CLIPPING PLANES

OpenGL includes the capability to specify clipping planes beyond those defined by the view frustum. One use for a user-defined clipping plane is to slice a model. This makes it possible to create complex shapes by starting with a simple model and slicing sections off of it.

A clipping plane is defined according to the standard mathematical definition of a plane:

$$ax + by + cz + d = 0$$

where a, b, c, and d are parameters defining a particular plane in 3D space with X, Y, and Z axes. The parameters represent a vector (a,b,c) normal to the plane, and a distance d from the origin to the plane. Such a plane can be specified in the vertex shader using a vec4, as follows:

```glsl
vec4 clip_plane = vec4(0.0, 0.0, -1.0, 0.2);
```

This would correspond to the plane:

$$(0.0) x + (0.0) y + (-1.0) z + 0.2 = 0$$

The clipping can then be achieved, also in the vertex shader, by using the built-in GLSL variable gl_ClipDistance[ ], as in the following example:

```glsl
gl_ClipDistance[0] = dot(clip_plane.xyz, vertPos) + clip_plane.w;
```

In this example, vertPos refers to the vertex position coming into the vertex shader in a vertex attribute (such as from a VBO); clip_plane was defined above. We then compute the signed distance from the clipping plane to the incoming vertex (shown in Chapter 3), which is either 0 if the vertex is on the plane, or is negative or positive depending on which side of the plane the vertex lies. The subscript on the gl_ClipDistance array enables multiple clipping distances (i.e., multiple planes) to be defined. The maximum number of user clipping planes that can be defined depends on the graphics card’s OpenGL implementation.

User-defined clipping must then be *enabled* in the C++/OpenGL application. There are built-in OpenGL identifiers GL_CLIP_DISTANCE0, GL_CLIP_DISTANCE1, and so on, corresponding to each gl_ClipDistance[ ] array element. The 0th user-defined clipping plane can be enabled, for example, as follows:

```cpp
glEnable(GL_CLIP_DISTANCE0);
```

![](img/1695de1bc7486362f86c143285f3fb40_341_0.png)

**Figure 14.6**<br>Clipping a torus.

![](img/1695de1bc7486362f86c143285f3fb40_341_1.png)

**Figure 14.7**<br>Clipping with back faces.

Applying the previous steps to our lighted torus results in the output shown in Figure 14.6, in which the front half of the torus has been clipped. (A rotation has also been applied to provide a clearer view.)

It may appear that the bottom portion of the torus has also been clipped, but that is because the inside faces of the torus were not rendered. When clipping reveals the inside surfaces of a shape, it is necessary to render them as well, or the model will appear incomplete (as it does in Figure 14.6).

Rendering the inner surfaces requires making a second call to `glDrawArrays()`, with the winding order reversed. Additionally, it is necessary to reverse the surface normal vector when rendering the back-facing triangles (as was done in the previous section). The relevant modifications to the C++ application and the vertex shader are shown in Program 14.3, with the output shown in Figure 14.7.

### Program 14.3 Clipping with Back Faces

C++ / OpenGL application:

```cpp
void display(GLFWwindow* window, double currentTime) {
    ...
    flipLoc = glGetUniformLocation(renderingProgram, "flipNormal");
    ...
    glEnable(GL_CLIP_DISTANCE0);

    // normal drawing of external faces
    glUniform1f(flipLoc, 0);
    glFrontFace(GL_CW);
    glDrawElements(GL_TRIANGLES, numTorusIndices, GL_UNSIGNED_INT, 0);
```

- 4. deciding on appropriate 3D texture coordinates for the object vertices
- 5. texturing the object in the fragment shader using an appropriate sampler

Texture coordinates for 3D textures range from 0 to 1, in the same manner as for 2D textures.

Interestingly, step #4 (determining 3D texture coordinates) is usually a lot simpler than one might initially suspect. In fact, it is usually simpler than for 2D textures! This is because (in the case of 2D textures) since a 3D object was being textured with a 2D image, we needed to decide how to “flatten” the 3D object’s vertices (such as by UV-mapping) to create texture coordinates. But when 3D texturing, both the object and the texture are of the same dimensionality (three). In most cases, we want the object to reflect the texture pattern, as if it were “carved” out of it (or dipped into it). So the vertex locations themselves serve as the texture coordinates! Usually all that is necessary is to apply some simple scaling to ensure that the object’s vertices’ location coordinates map to the 3D texture coordinates’ range [0..1].

Since we are generating the 3D texture procedurally, we need a way of constructing an OpenGL texture map out of generated data. The process for loading data into a texture is similar to what we saw earlier in Section 5.12. In this case, we fill a 3D array with color values, then copy them into a texture object.

Program 14.4 shows the various components for achieving all of the previous steps in order to texture an object with blue and yellow horizontal stripes from a procedurally built 3D texture. The desired pattern is built in the generate3Dpattern() function, which stores the pattern in an array named “tex3Dpattern”. The “image” data is then built in the function fillDataArray(), which fills a 3D array with byte data corresponding to the RGB colors R, G, B, and A, each in the range [0..255], according to the pattern. Those values are then copied into a texture object in the load3DTexture() function.

### Program 14.4 3D Texturing: Striped Pattern

C++ / OpenGL application:

```cpp
...
const int texWidth = 200;
const int texHeight = 200;
const int texDepth = 200;
double tex3Dpattern[texWidth][texHeight][texDepth];
...

// fill a byte array with RGB blue/yellow values corresponding to the pattern built by generate3Dpattern()
void fillDataArray(GLubyte data[]) {
    for (int i=0; i<texWidth; i++) {
        for (int j=0; j<texHeight; j++) {
            for (int k=0; k<texDepth; k++) {
                if (tex3Dpattern[i][j][k] == 1.0) {
                    // yellow color
                    data[i*(texWidth*texHeight*4) + j*(texHeight*4) + k*4+0] = (GLubyte) 255;  // red
                    data[i*(texWidth*texHeight*4) + j*(texHeight*4) + k*4+1] = (GLubyte) 255;  // green
                    data[i*(texWidth*texHeight*4) + j*(texHeight*4) + k*4+2] = (GLubyte) 0;    // blue
                    data[i*(texWidth*texHeight*4) + j*(texHeight*4) + k*4+3] = (GLubyte) 255;  // alpha
                }
                else {
                    // blue color
                    data[i*(texWidth*texHeight*4) + j*(texHeight*4) + k*4+0] = (GLubyte) 0;    // red
                    data[i*(texWidth*texHeight*4) + j*(texHeight*4) + k*4+1] = (GLubyte) 0;    // green
                    data[i*(texWidth*texHeight*4) + j*(texHeight*4) + k*4+2] = (GLubyte) 255;  // blue
                    data[i*(texWidth*texHeight*4) + j*(texHeight*4) + k*4+3] = (GLubyte) 255;  // alpha
                }
            }
        }
    }
}

// build 3D pattern of stripes
void generate3Dpattern() {
    for (int x=0; x<texWidth; x++) {
        for (int y=0; y<texHeight; y++) {
            for (int z=0; z<texDepth; z++) {
                if ((y%10)%2 == 0)
                    tex3Dpattern[x][y][z] = 0.0;
                else
                    tex3Dpattern[x][y][z] = 1.0;
            }
        }
    }
}

// load the sequential byte data array into a texture object
int load3DTexture() {
    GLuint textureID;
    GLubyte* data = new GLubyte[texWidth*texHeight*texDepth*4];

    fillDataArray(data);

    glGenTextures(1, &textureID);
    glBindTexture(GL_TEXTURE_3D, textureID);
    glTexParameteri(GL_TEXTURE_3D, GL_TEXTURE_MIN_FILTER, GL_LINEAR);
    glTexStorage3D(GL_TEXTURE_3D, 1, GL_RGBA8, texWidth, texHeight, texDepth);
    glTexSubImage3D(GL_TEXTURE_3D, 0, 0, 0, 0, texWidth, texHeight, texDepth,
                    GL_RGBA, GL_UNSIGNED_INT_8_8_8_8_REV, data);
    delete[] data; return textureID;
}
```
