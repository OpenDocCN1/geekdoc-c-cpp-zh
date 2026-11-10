```
private int workGroupsY = rayTraceRenderHeight;
private int workGroupsZ = 1;

private int[] screenTextureID = new int[1];        // The texture ID for the render area
private byte[] screenTexture = new byte[rayTraceRenderWidth * rayTraceRenderHeight * 16];

// other variable declarations for VAOs, VBOs, etc., as before
. . .

public void init(GLAutoDrawable drawable)
{  GL4 gl = (GL4) GLContext.getCurrentGL();

   // set the initial texture pixel colors to pink – if pink appears, there might be an error at that pixel
   for (int i=0; i<rayTraceRenderHeight; i++)
   {  for (int j=0; j<rayTraceRenderHeight; j++)
      {  screenTexture[i*rayTraceRenderWidth * 4 + j * 4 + 0] = (byte) 250;
         screenTexture[i*rayTraceRenderWidth * 4 + j * 4 + 1] = (byte) 128;
         screenTexture[i*rayTraceRenderWidth * 4 + j * 4 + 2] = (byte) 255;
         screenTexture[i*rayTraceRenderWidth * 4 + j * 4 + 3] = (byte) 255;
      }
   }
   ByteBuffer screenTextureBuffer = Buffers.newDirectByteBuffer(screenTexture);

   // create the OpenGL Texture on which to ray cast the scene
   gl.glGenTextures(1, screenTextureID, 0);
   gl.glBindTexture(GL_TEXTURE_2D, screenTextureID[0]);
   gl.glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_NEAREST);
   gl.glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_NEAREST);
   gl.glTexImage2D(GL_TEXTURE_2D, 0, GL_RGBA, rayTraceRenderWidth, rayTraceRenderHeight,
      0, GL_RGBA, GL_UNSIGNED_BYTE, screenTextureBuffer);

   // create quad vertices and texture coordinates for rendering the finished texture to the window
   float[] fullscreenQuadVerts =
   {  -1.0f, 1.0f, 0.0f, -1.0f, -1.0f, 0.0f, 1.0f, -1.0f, 0.0f,
      1.0f, -1.0f, 0.0f, 1.0f, 1.0f, 0.0f, -1.0f, 1.0f, 0.0f
   };

   float[] fullscreenQuadUVs =
   {  0.0f, 1.0f, 0.0f, 0.0f, 1.0f, 0.0f,
      1.0f, 0.0f, 1.0f, 1.0f, 0.0f, 1.0f
   };

   gl.glGenVertexArrays(vao.length, vao, 0);
   gl.glBindVertexArray(vao[0]);
   gl.glGenBuffers(vbo.length, vbo, 0);

   gl.glBindBuffer(GL_ARRAY_BUFFER, vbo[0]); // vertex positions
   FloatBuffer quadVertsBuf = Buffers.newDirectFloatBuffer(fullscreenQuadVerts);
   gl.glBufferData(GL_ARRAY_BUFFER, quadVertsBuf.limit()*4, quadVertsBuf, GL_STATIC_DRAW);
```