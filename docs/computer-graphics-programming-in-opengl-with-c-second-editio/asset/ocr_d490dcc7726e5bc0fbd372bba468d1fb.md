# 5.7 TEXTURE MAPPING: EXAMPLE PROGRAM

![](bbox=[0.141, 0.144, 0.483, 0.323])

**Figure 5.4**  
Pyramid texture mapped with brick image.

Program 5.1 combines the previous steps into a single program. The result, showing the pyramid textured with the brick image, appears in Figure 5.4. Two rotations (not shown in the code listing) were added to the pyramid’s model matrix to expose the underside of the pyramid.

It is now a simple matter to replace the brick texture image with other texture images, as desired, simply by changing the filename in the loadTexture() call. For example, if we replace “brick1.jpg” with the image file “ice.jpg” [LU16], we get the result shown in Figure 5.5.

![](bbox=[0.273, 0.456, 0.727, 0.631])

**Figure 5.5**  
Pyramid texture mapped with “ice” image.

# Program 5.1 Pyramid with Brick Texture

C++/OpenGL Application

```
```cpp
#include <SOIL2/soil2.h>
// other includes as before
...
#define numVAOs 1
#define numVBOs 2

// variables for camera and object location, rendering program, VAOs and VBOs as before
...
```
```