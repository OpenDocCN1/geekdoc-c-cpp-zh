
## Chapter 12: Precomputed 3D Velocity Field for Simulating Fluid Dynamics

- Listing 12.1: Pseudocode of the full solver.
- Listing 12.2: Pseudocode of the obstacle heuristic.

## Chapter 17: Motion Blur and the Velocity-Depth-Gradient Buffer

Listing 17.1: This GLSL vertex shader first transforms the vertex position for the current frame to homogeneous clip-space coordinates in the ordinary manner using the model-view-projection (MVP) matrix. The shader then transforms the vertex position into screen space for both the preceding frame using the matrix motionA and the current frame using the matrix motionB. The resulting positions are output as texture coordinates that will be read by the fragment shader.

Listing 17.2: This GLSL fragment shader calculates the screen-space velocity and writes it to the red and green components of the output color. The velocityScale parameter holds the value of s/rmax shown in Equation (17.6). The depth is taken directly from the w-coordinate of the current position and is written to the blue component of the output color. The gradient of the depth is calculated using the hardware derivative functions, and the larger of its components is written to the alpha component of the output color.

Listing 17.3: This GLSL fragment shader applies the motion blur effect in the post-processing pass. The nine color samples are accumulated in the x, y, and z components of the color vector, and the number of valid samples is stored in the w component of the color vector. The value of minDepth is calculated using Equation (17.9), and only samples having a depth at least this far from the camera plane are used to generate the final blurred pixel.

## Chapter 18: Fast Screen-Space Ambient Occlusion and Indirect Lighting

Listing 18.1: This fragment shader implements the algorithm discussed in this gem.

## Chapter 19: Real-Time Character Dismemberment

Listing 19.1: The damage zone class definition.

## Chapter 20: A Deferred Decal Rendering Technique

Listing 20.1: This code determines the decal-space coordinates for the fragment being rendered and transforms them into texture coordinates for the decal. The RT_Depth texture contains depth values for the viewport, the worldToDecal constant is the inverse of the decal's 4x4 matrix transform from decal space to world space, and the recipDecalSize constant is 1/s, where s is the size of the decal in the scene.

Listing 20.2: This vertex shader scales a unit cube to the actual size of the decal and translates it to the decal's world-space position.

Listing 20.3: The absolute value of the decal-space z-coordinate of the fragment position is scaled to the size of the decal and used as a fade-out parameter for the decal color. As before, the recipDecalSize constant is 1/s, where s is the size of the decal in the scene.

Listing 20.4: This code demonstrates how the normal of the underlying surface can be used to adjust texture coordinates in such a way that a decal wraps around curves and corners. The RT_Normal texture contains normal vectors for the viewport encoded in the RGB channels.

## Chapter 23: Dynamic Code Execution Hierarchies

- Listing 23.1: Example base class.
- Listing 23.2: Example game code.

## Chapter 26: The Game State Observer Pattern

- Listing 26.1: GameState class implementation in C#.
- Listing 26.2: The IObservable and INotifiable interfaces.
- Listing 26.3: The Subscribe() and Unsubscribe() methods of the GameState class.
- Listing 26.4: The _NotifySubscribers() method of the GameState class.
- Listing 26.5: The set implementation for the currentState member of the GameState class.
- Listing 26.6: A sample observer implementation.
- Listing 26.7: Accessing an observer by its native type.
- Listing 26.8: Supporting multiple subject types.

## Chapter 27: Fast Trigonometric Operations Using Cordic Methods

- Listing 27.1: Rotation and vectoring mode implementations.
- Listing 27.2: Normalizing the input range.
- Listing 27.3: Angle table generation.
- Listing 27.4: Computation of C.
- Listing 27.5: Sine and cosine implementation.
- Listing 27.6: Arctangent implementation.
- Listing 27.7: Vector rotation implementation.
- Listing 27.8: Vector length implementation.

## Chapter 28: Inter-Process Communication Based on Your Own RPC Subsystem

Listing 28.1: Example stub functions for the client and server.
