
## 5.7 TEXTURE MAPPING: EXAMPLE PROGRAM

![](img/1695de1bc7486362f86c143285f3fb40_132_0.png)

**Figure 5.4**  
Pyramid texture mapped with brick image.

Program 5.1 combines the previous steps into a single program. The result, showing the pyramid textured with the brick image, appears in Figure 5.4. Two rotations (not shown in the code listing) were added to the pyramid’s model matrix to expose the underside of the pyramid.

It is now a simple matter to replace the brick texture image with other texture images, as desired, simply by changing the filename in the loadTexture() call. For example, if we replace “brick1.jpg” with the image file “ice.jpg” [LU16], we get the result shown in Figure 5.5.

![](img/1695de1bc7486362f86c143285f3fb40_132_1.png)

**Figure 5.5**  
Pyramid texture mapped with “ice” image.

### Program 5.1 Pyramid with Brick Texture

C++/OpenGL Application

```cpp
#include <SOIL2/SOIL2.h>
// other includes as before
...
#define numVAOs 1
#define numVBOs 2

// variables for camera and object location, rendering program, VAOs and VBOs as before
...
// variable allocation for display function same as before
...
GLuint brickTexture;

void setupVertices(void) {
    float pyramidPositions[54] = { /* data as listed previously in Program 4.2 */ }

    float pyrTexCoords[36] = {
        0.0f, 0.0f, 1.0f, 0.0f, 0.5f, 1.0f,      0.0f, 0.0f, 1.0f, 0.0f, 0.5f, 1.0f,
        0.0f, 0.0f, 1.0f, 0.0f, 0.5f, 1.0f,      0.0f, 0.0f, 1.0f, 0.0f, 0.5f, 1.0f,
        0.0f, 0.0f, 1.0f, 0.0f, 0.5f, 1.0f,      1.0f, 1.0f, 0.0f, 0.0f, 1.0f, 0.0f
    };

    // . . . generate the VAO as before, and at least two VBOs, then load the two buffers as follows:
    glBindBuffer(GL_ARRAY_BUFFER, vbo[0]);
    glBufferData(GL_ARRAY_BUFFER, sizeof(pyramidPositions), pyramidPositions, GL_STATIC_DRAW);

    glBindBuffer(GL_ARRAY_BUFFER, vbo[1]);
    glBufferData(GL_ARRAY_BUFFER, sizeof(pyrTexCoords), pyrTexCoords, GL_STATIC_DRAW);
}

void init(GLFWwindow* window) {
    // setup of rendering program, camera and object location unchanged
    . . .
    brickTexture = Utils::loadTexture("brick1.jpg");
}

void display(GLFWwindow* window, double currentTime) {
    . . .
    // setup of background color, depth buffer, rendering program, M, V, MV, and PROJ matrices unchanged
    . . .
    glBindBuffer(GL_ARRAY_BUFFER, vbo[0]);
    glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 0, 0);
    glEnableVertexAttribArray(0);

    glBindBuffer(GL_ARRAY_BUFFER, vbo[1]);
    glVertexAttribPointer(1, 2, GL_FLOAT, GL_FALSE, 0, 0);
    glEnableVertexAttribArray(1);

    glActiveTexture(GL_TEXTURE0);
    glBindTexture(GL_TEXTURE_2D, brickTexture);

    glEnable(GL_DEPTH_TEST);
    glDepthFunc(GL_LEQUAL);

    glDrawArrays(GL_TRIANGLES, 0, 18);
}

// main() same as before
```

### Vertex shader

```glsl
#version 430
layout(location=0) in vec3 pos;
layout(location=1) in vec2 texCoord;
out vec2 tc;          // texture coordinate output to rasterizer for interpolation
uniform mat4 mv_matrix;
uniform mat4 proj_matrix;
layout(binding=0) uniform sampler2D samp;    // not used in vertex shader

void main(void)
{ gl_Position = proj_matrix * mv_matrix * vec4(pos,1.0);
  tc = texCoord;
}
```

### Fragment shader

```glsl
#version 430
in vec2 tc;          // interpolated incoming texture coordinate
out vec4 color;
uniform mat4 mv_matrix;
uniform mat4 proj_matrix;
layout(binding=0) uniform sampler2D samp;

void main(void)
{ color = texture(samp, tc);
}
```

## 5.8 MIPMAPPING

Texture mapping commonly produces a variety of undesirable artifacts in the rendered image. This is because the resolution or aspect ratio of the texture image rarely matches that of the region in the scene being textured.

A very common artifact occurs when the image resolution is *less than* that of the region being drawn. In this case, the image would need to be stretched to cover the region, becoming blurry (and possibly distorted). This can sometimes be combated, depending on the nature of the texture, by assigning the texture coordinates differently so that applying the texture requires less stretching. Another solution is to use a higher resolution texture image.

The reverse situation is when the resolution of the image texture is *greater than* that of the region being drawn. It is probably not at all obvious why this would pose a problem, but it does! In this case, noticeable *aliasing* artifacts can occur, giving rise to strange-looking false patterns, or “shimmering” effects in moving objects.

Aliasing is caused by *sampling errors*. It is most often associated with signal processing, where an inadequately sampled signal appears to have different properties (such as wavelength) than it actually does when it is reconstructed. An example is shown in Figure 5.6. The original waveform is shown in red. The yellow dots along the waveform represent the samples. If they are used to reconstruct the wave, and if there aren't enough of them, they can define a different wave (shown in blue).

![](img/1695de1bc7486362f86c143285f3fb40_135_0.png)

**Figure 5.6**  
Alias due to inadequate sampling.

Similarly, in texture-mapping, when a high-resolution (and highly detailed) image is sparsely sampled (such as when using a uniform sampler variable), the colors retrieved will be inadequate to reflect the actual detail in the image, and may instead seem random. If the texture image has a repeated pattern, aliasing can result in a *different* pattern being produced than the one in the original image. If the object being textured is moving, rounding errors in texel lookup can result in constant changes in the sampled pixel at a given texture coordinate, producing an unwanted sparkling effect across the surface of the object being drawn.

Figure 5.7 shows a tilted, close-up rendering of the top of a cube which has been textured by a large, high-resolution image of a checkerboard.

![](img/1695de1bc7486362f86c143285f3fb40_135_1.png)

**Figure 5.7**  
Aliasing in a texture map.

![](img/1695de1bc7486362f86c143285f3fb40_136_0.png)

Aliasing is evident near the top of the image, where the under-sampling of the checkerboard has produced a “striped” effect. Although we can't show it here in a still image, if this were an animated scene, the patterns would likely undulate between various incorrect patterns such as this one.

**Figure 5.8**  
'Sparkling' in a texture map.

Another example appears in Figure 5.8, in which the cube has been textured with an image of the surface of the moon [HT12].

At first glance, this image appears sharp and full of detail. However, some of the detail at the upper right of the image is false and causes “sparkling” as the cube object (or the camera) moves. (Unfortunately, we can't show the sparkling effect clearly in a still image.)

These and similar sampling error artifacts can be largely corrected by a technique called *mipmapping*, in which different versions of the texture image are created at various resolutions. OpenGL then uses the texture image that most closely matches the resolution at the point being textured. Even better, colors can be averaged between the images closest in resolution to that of the region being textured. Results of applying mipmapping to the images in Figure 5.7 and Figure 5.8 are shown in Figure 5.9.

![](img/1695de1bc7486362f86c143285f3fb40_136_1.png)

**Figure 5.9**  
Mipmapped results.

Mipmapping works by a clever mechanism for storing a series of successively lower-resolution copies of the same image in a texture image one-third larger than the original image. This is achieved by storing the R, G, and B components of the image separately in three-quarters of the texture image space, then repeating the process in the remaining one-quarter of the image space for the same image at one-quarter the original resolution. This subdividing repeats until the remaining quadrant is too small to contain any useful image data. An example image and a visualization of the resulting mipmap is shown in Figure 5.10.

![](img/1695de1bc7486362f86c143285f3fb40_137_0.png)

**Figure 5.10**  
Mipmapping an image.

This method of stuffing several images into a small space (well, just a bit bigger than the space needed to store the original image) is how mipmapping got its name. MIP stands for *Multum In Parvo* [Wl83], which is Latin for “much in a small space.”

When actually texturing an object, the mipmap can be sampled in several ways. In OpenGL, the manner in which the mipmap is sampled can be chosen by setting the GL_TEXTURE_MIN_FILTER parameter to the desired *minification* technique, which is one of the following:

- **GL_NEAREST_MIPMAP_NEAREST** chooses the mipmap with the resolution most similar to that of the region of pixels being textured. It then obtains the nearest texel to the desired texture coordinates.
