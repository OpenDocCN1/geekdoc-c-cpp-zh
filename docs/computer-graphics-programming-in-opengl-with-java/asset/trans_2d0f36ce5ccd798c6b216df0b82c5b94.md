

```java
// set up vertices buffer for cube (buffer for texture coordinates not necessary)
gl.glBindBuffer(GL_ARRAY_BUFFER, vbo[0]);
gl.glVertexAttribPointer(0, 3, GL_FLOAT, false, 0, 0);
gl.glEnableVertexAttribArray(0);

// make the cube map the active texture
gl.glActiveTexture(GL_TEXTURE0);
gl.glBindTexture(GL_TEXTURE_CUBE_MAP, skyboxTexture);

// disable depth testing, and then draw the cube map
gl.glEnable(GL_CULL_FACE);
gl.glFrontFace(GL_CCW);
gl.glDisable(GL_DEPTH_TEST);
gl.glDrawArrays(GL_TRIANGLES, 0, 36);
gl.glEnable(GL_DEPTH_TEST);

// draw remainder of the scene
...
}
```

```java
public int loadCubeMap(String dirName)
{  GL4 gl = (GL4) GLContext.getCurrentGL();

   // assumes that the six file names are xp, xn, yp, yn, zp, and zn and are JPG format
   String topFile = dirName + File.separator + "yp.jpg";
   String leftFile = dirName + File.separator + "xn.jpg";
   String backFile = dirName + File.separator + "zn.jpg";
   String rightFile = dirName + File.separator + "xp.jpg";
   String frontFile = dirName + File.separator + "zp.jpg";
   String bottomFile = dirName + File.separator + "yn.jpg";

   BufferedImage topImage = getBufferedImage(topFile);
   BufferedImage leftImage = getBufferedImage(leftFile);
   BufferedImage frontImage = getBufferedImage(frontFile);
   BufferedImage rightImage = getBufferedImage(rightFile);
   BufferedImage backImage = getBufferedImage(backFile);
   BufferedImage bottomImage = getBufferedImage(bottomFile);

   // getRGBAPixel is from Chapter 5. This time image NOT flipped because OpenGL does it for us
   byte[] topRGBA = getRGBAPixelData(topImage, false);
   byte[] leftRGBA = getRGBAPixelData(leftImage, false);
   byte[] frontRGBA = getRGBAPixelData(frontImage, false);
   byte[] rightRGBA = getRGBAPixelData(rightImage, false);
   byte[] backRGBA = getRGBAPixelData(backImage, false);
   byte[] bottomRGBA = getRGBAPixelData(bottomImage, false);

   ByteBuffer topWrappedRGBA = ByteBuffer.wrap(topRGBA);
   ByteBuffer leftWrappedRGBA = ByteBuffer.wrap(leftRGBA);
   ByteBuffer frontWrappedRGBA = ByteBuffer.wrap(frontRGBA);
   ByteBuffer rightWrappedRGBA = ByteBuffer.wrap(rightRGBA);
   ByteBuffer backWrappedRGBA = ByteBuffer.wrap(backRGBA);
   ByteBuffer bottomWrappedRGBA = ByteBuffer.wrap(bottomRGBA);

   int[] textureIDs = new int[1];
   gl.glGenTextures(1, textureIDs, 0);
   int textureID = textureIDs[0];

   gl.glBindTexture(GL_TEXTURE_CUBE_MAP, textureID);
   gl.glTexStorage2D(GL_TEXTURE_CUBE_MAP, 1, GL_RGBA8, 1024, 1024);

   // attach the image texture to each face of the currently active OpenGL texture ID
   gl.glTexSubImage2D(GL_TEXTURE_CUBE_MAP_POSITIVE_X, 0, 0, 0, 1024, 1024,
           GL_RGBA, GL.GL_UNSIGNED_BYTE, rightWrappedRGBA);
   gl.glTexSubImage2D(GL_TEXTURE_CUBE_MAP_NEGATIVE_X, 0, 0, 0, 1024, 1024,
           GL_RGBA, GL.GL_UNSIGNED_BYTE, leftWrappedRGBA);
   gl.glTexSubImage2D(GL_TEXTURE_CUBE_MAP_NEGATIVE_Y, 0, 0, 0, 1024, 1024,
           GL_RGBA, GL.GL_UNSIGNED_BYTE, bottomWrappedRGBA);
   gl.glTexSubImage2D(GL_TEXTURE_CUBE_MAP_POSITIVE_Y, 0, 0, 0, 1024, 1024,
           GL_RGBA, GL.GL_UNSIGNED_BYTE, topWrappedRGBA);
   gl.glTexSubImage2D(GL_TEXTURE_CUBE_MAP_POSITIVE_Z, 0, 0, 0, 1024, 1024,
           GL_RGBA, GL.GL_UNSIGNED_BYTE, frontWrappedRGBA);
   gl.glTexSubImage2D(GL_TEXTURE_CUBE_MAP_NEGATIVE_Z, 0, 0, 0, 1024, 1024,
           GL_RGBA, GL.GL_UNSIGNED_BYTE, backWrappedRGBA);

   // to help reduce seams
   gl.glTexParameteri(GL_TEXTURE_CUBE_MAP, GL_TEXTURE_WRAP_S, GL_CLAMP_TO_EDGE);
   gl.glTexParameteri(GL_TEXTURE_CUBE_MAP, GL_TEXTURE_WRAP_T, GL_CLAMP_TO_EDGE);
   gl.glTexParameteri(GL_TEXTURE_CUBE_MAP, GL_TEXTURE_WRAP_R, GL_CLAMP_TO_EDGE);

   return textureID;
}
```

### 顶点着色器

```glsl
#version 430
layout (location = 0) in vec3 position;
out vec3 tc;

uniform mat4 v_matrix;
uniform mat4 p_matrix;
layout (binding = 0) uniform samplerCube samp;

void main(void)
{
    tc = position;                               // texture coordinates are simply the vertex coordinates
    mat4 rot_mat = mat4(v_matrix);               // removes translation from view matrix
    gl_Position = p_matrix * rot_mat * vec4(position, 1.0);
}
```

### *片段着色器*

```glsl
#version 430
in vec3 tc;
out vec4 fragColor;

uniform mat4 v_matrix;
uniform mat4 p_matrix;
layout (binding = 0) uniform samplerCube samp;

void main(void)
{ fragColor = texture(samp,tc);
}
```

## 9.4 环境映射

在讨论光照和材质时，我们考虑了物体的“光泽度”。然而，我们从未模拟过*非常*光滑的物体，例如镜子或铬合金制成的物品。这类物体不仅仅具有小的镜面高光；它们实际上会反射周围的环境。当我们看向它们时，我们会看到房间里的东西，有时甚至看到自己的倒影。ADS 光照模型无法提供模拟这种效果的方法。

不过，纹理立方体贴图提供了一种相对简单的方法来模拟反射表面——至少是部分模拟。诀窍在于*使用立方体贴图来为反射物体本身进行纹理贴图*！要实现逼真的效果，需要找到与环境中的特定部分相对应的纹理坐标，而这些部分正是我们从观察点应当在物体中反射出来的周围环境。

图 9.9 展示了使用视线向量和法向量的组合来计算*反射向量*的策略，然后使用该反射向量从立方体贴图中查找纹素。因此，反射向量可以直接用于访问纹理立方体贴图。当立方体贴图执行此功能时，它被称为*环境贴图*。

1 同样的技巧也适用于使用天空穹顶代替天空盒的情况，只需用天空穹顶的纹理图像对反射物体进行纹理贴图即可。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_255_0.png)

我们之前在研究 Blinn-Phong 光照时已经计算过反射向量。这里的概念类似，只不过现在我们使用反射向量来从纹理贴图中查找值。这种技术被称为*环境映射*或*反射映射*。如果立方体贴图使用我们描述过的第二种方法（在第 9.3.2 节中——即作为 OpenGL 的 `GL_TEXTURE_CUBE_MAP`）实现，那么 OpenGL 可以以与对立方体贴图本身进行纹理贴图相同的方式来执行环境映射查找。我们使用视线向量和表面法线来计算视线向量在物体表面上的反射。随后，反射向量可用于直接采样纹理立方体贴图图像。该查找过程由 OpenGL 的 `samplerCube` 简化；请回顾前一节，`samplerCube` 是通过视线方向向量进行索引的。因此，反射向量非常适合用于查找所需的纹素。

该实现只需要相对较少的额外代码。程序 9.3 展示了为使用环境映射渲染“反射”圆环而对 `display()` 和 `init()` 函数及相关着色器所做的修改。修改部分已突出显示。值得注意的是，如果存在 Phong 光照，这些新增内容中的许多可能已经存在。唯一真正新增的代码段位于片段着色器（在 `main()` 方法中）。

实际上，乍一看，程序 9.3 中突出显示的代码（即黄色部分）似乎并不算什么新内容。确实，我们在研究光照时已经见过几乎相同的代码。然而，在这种情况下，法向量和反射向量被用于完全不同的目的。此前，它们被用于

```java
// build the MODEL-VIEW matrix, as before
mvMat.identity();
mvMat.mul(vMat);
mvMat.mul(mMat);
mMat.invert(invTrMat);
invTrMat.transpose(invTrMat);

// the normals transform is now included in the uniforms:
gl.glUniformMatrix4fv(mvLoc, 1, false, mvMat.get(vals));
gl.glUniformMatrix4fv(pLoc, 1, false, pMat.get(vals));
gl.glUniformMatrix4fv(nLoc, 1, false, invTrMat.get(vals));

// activate the torus vertices buffer, as before
gl.glBindBuffer(GL_ARRAY_BUFFER, vbo[1]);
gl.glVertexAttribPointer(0, 3, GL_FLOAT, false, 0, 0);
gl.glEnableVertexAttribArray(0);

// we need to activate the torus normals buffer:
gl.glBindBuffer(GL_ARRAY_BUFFER, vbo[2]);
gl.glVertexAttribPointer(1, 3, GL_FLOAT, false, 0, 0);
gl.glEnableVertexAttribArray(1);

// the torus texture is now the cube map
gl.glActiveTexture(GL_TEXTURE0);
gl.glBindTexture(GL_TEXTURE_CUBE_MAP, skyboxTexture);

// drawing the torus is otherwise unchanged
gl.glClear(GL_DEPTH_BUFFER_BIT);
gl.glEnable(GL_CULL_FACE);
gl.glFrontFace(GL_CCW);
gl.glDepthFunc(GL_LEQUAL);

gl.glBindBuffer(GL_ELEMENT_ARRAY_BUFFER, vbo[3]);
gl.glDrawElements(GL_TRIANGLES, numTorusIndices, GL_UNSIGNED_INT, 0);
}
```

### 顶点着色器

```glsl
#version 430
layout (location = 0) in vec3 position;
layout (location = 1) in vec3 normal;
out vec3 varyingNormal;
out vec3 varyingVertPos;
uniform mat4 mv_matrix;
uniform mat4 p_matrix;
uniform mat4 norm_matrix;
layout (binding = 0) uniform samplerCube tex_map;
```

