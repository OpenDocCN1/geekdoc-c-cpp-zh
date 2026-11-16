
Item 4 is an issue because today's games often use very complex meshes for rendering, but a less detailed mesh might be used for collision detection. The difficulty is that the point of intersection that a ray cast returns might differ quite a bit from the location where the decal must be rendered.

### 20.2 The General Idea

The basic solution afforded by our technique is to project a decal onto a surface using a special fragment shader applied to the decal's bounding volume instead of rendering new decal polygons on top of the scene geometry. The only information required to achieve this consists of the position and orientation of the decal, the decal's size, and a texture containing depth values for the viewport being rendered. This information allows all computation to be done in the vertex and fragment shaders.

When rendering a decal, it is natural for us to work in "decal space", where the x- and y-axes lie in the tangent plane to the underlying surface at the decal's center, and the z-axis is parallel to the surface's normal vector at the decal's center. In order to move data into the decal's local coordinate system, the shader needs to be supplied with the inverse of the decal's transformation matrix.

The code in Listing 20.1 first fetches the depth from the G-buffer at the fragment position and uses it to reconstruct the 3D world-space position of the fragment. The `worldToDecal` constant is the inverse of the transformation matrix for the decal that we are currently rendering. With this matrix, we can transform the fragment's position into the local space of the decal. This local position can then be used to compute texture coordinates at which the decal texture is sampled. In this first version, we are using the (x,y) position only, which simply projects the decal along its local z-axis onto the underlying geometry, as shown in Figure 20.2.

![](img/7ba1225bb0e5a87be0fd35866408ffa7_436_0.png)

Figure 20.2: Using a simple projection onto the local x-y plane causes decals to be smeared in the direction of the local z-axis.

### Listing 20.1: This code determines the decal-space coordinates for the fragment being rendered and transforms them into texture coordinates for the decal. The RT_Depth texture contains depth values for the viewport, the worldToDecal constant is the inverse of the decal's 4x4 matrix transform from decal space to world space, and the recipDecalSize constant is 1/s, where s is the size of the decal in the scene.

```
// Sample the depth at the current fragment
float pixelDepth = texture2DRect(RT_Depth, gl_FragCoord);
// Compute the fragment's world-space position
vec3 worldPos = ComputeWorldSpacePosition(gl_FragCoord);
// Transform into decal space
vec3 decalPos = worldToDecal * worldPos;
// Use the xy position of the position for the text
vec2 texcoord = decalPos.xy * recipDecalSize * 0.5;
// Fetch the decal texture color
gl_FragColor = texture2D(diffuseDecalTexture, texcoord);
```

### 20.3 Geometry Rendering

Now that we have some code that calculates basic texture coordinates, we must consider what kind of geometry we actually need to render. Each fragment rendered with the decal shader acts like a "window" through which we can possibly see our decal. So we could just render a surface-aligned quad corresponding to the size and position of the decal. However, we want our decal to have depth, so we instead render a bounding cube as shown in Figure 20.3. This allows us to see the decal from any direction, and it will allow us to add a wrap-around feature later on.

![](img/7ba1225bb0e5a87be0fd35866408ffa7_437_0.png)

Figure 20.3: A bounding cube centered on a decal can be rendered to ensure that we capture the decal's influence from any viewpoint.

As an optimization for scenes containing a large number of decals, it can be advantageous to render decals through hardware instancing [7]. Therefore, it is a good idea to simply render a unit cube and transform it to the correct size and position in the vertex shader, as demonstrated in Listing 20.2. Note that we can easily extend the uniform constants decalSize and decalToWorld to arrays and use gl_InstanceID to render a batch of decals through instancing.

### Listing 20.2: This vertex shader scales a unit cube to the actual size of the decal and translates it to the decal's world-space position.

```
uniform float decalSize;
uniform mat4 decalToWorld;

// scale the unit cube and position it in world space
vec4 worldPos = decalToWorld *
    vec4(gl_Vertex.xyz * decalSize, gl_Vertex.w);

// output the position in homogeneous clip space
gl_Position = gl_ModelViewProjectionMatrix * worldPos;
```

For small decals, this technique works very well. However, when a cube is rendered with backface culling enabled and the depth test set to GL_LESS, the decal disappears the moment the camera enters the cube. One solution to this problem is to cull front faces and set the depth test to GL_GREATER. This way, only fragments whose world positions are actually behind surfaces are rendered, but it causes many fragments to be rendered unnecessarily when they are occluded by geometry closer to the camera.

Another solution is to find the corner of the cube that is closest to the camera and render a camera-aligned quad at that depth that is large enough to enclose the entire cube. If the closest corner is in front of the near plane, a full-screen quad should be rendered at the near plane instead.

### 20.4 Fade Out And Wrap-Around

We have a basic vertex shader and fragment shader in place, but our projection is infinite along the decal's z-axis, producing the smearing shown in Figure 20.2. There are two methods we can use to fix this problem. The simpler method is to use the distance from the fragment's position to the decal plane as a fade-out parameter. This distance is already available in `decalPos.z`, and we just have to scale it to the size of the decal as demonstrated in Listing 20.3.

### Listing 20.3: The absolute value of the decal-space z-coordinate of the fragment position is scaled to the size of the decal and used as a fade-out parameter for the decal color. As before, the `recipDecalSize` constant is 1/s, where s is the size of the decal in the scene.

```
// compute the distance of the fragment to the decal plane
float distance = abs(decalPos.z);

// scale the distance into the [0,1] range
// according to the size of the decal
float scaledDistance = min(distance * recipDecalSize, 1.0);

// somehow use that scaled distance to fade out
// here: simple linear fade out
float fadeOut = 1.0 - scaledDistance;

vec4 diffuseColor = texture2D(diffuseDecalTexture, texcoord);

gl_FragColor = vec4(diffuseColor.rgb, diffuseColor.a * fadeOut);
```

This method is useful when a decal is supposed to be flat without wrapping around geometry. The exact formula used to fade out a decal can be varied to produce the best look for different decals, and it is advisable to make this configurable within the engine.

A more interesting method for handling the smearing problem is to make a decal wrap around corners and follow the curvature of complex surfaces. This is especially useful for blood stains and other liquids that splatter because it is much more convincing if such a decal covers an entire surface independently of its curvature.

This is quite easy to achieve. All we need is the surface normal at the position of each fragment in the decal. If we rotate that normal into decal space, its (x y) components give us the gradient of the surface relative to the decal plane. We can use this gradient and the fragment's distance to the decal plane to modify the texture coordinates. In areas with no relative slope, the texture lookup remains unchanged, but in areas with a large slope (for example, at corners), the texture coordinates move outward according to the distance to the decal plane. This technique is illustrated in Listing 20.4, and the result is shown in Figure 20.4.

![](img/7ba1225bb0e5a87be0fd35866408ffa7_440_0.png)

Figure 20.4: The decals wrap around corners based on the surface normals, and they fade out based on the distance from the decal plane.

### Listing 20.4: This code demonstrates how the normal of the underlying surface can be used to adjust texture coordinates in such a way that a decal wraps around curves and corners. The RT_Normal texture contains normal vectors for the viewport encoded in the RGB channels.
