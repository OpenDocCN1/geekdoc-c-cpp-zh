
```java
outer = 0.2f;
initTorus();
}

public Torus(float innerRadius, float outerRadius, int precision)
{
    inner = innerRadius; outer = outerRadius; prec = precision;
    initTorus();
}

private void initTorus()
{
    numVertices = (prec+1) * (prec+1);
    numIndices = prec * prec * 6;
    indices = new int[numIndices];
    vertices = new Vector3f[numVertices];
    texCoords = new Vector2f[numVertices];
    normals = new Vector3f[numVertices];
    sTangents = new Vector3f[numVertices];
    tTangents = new Vector3f[numVertices];

    for (int i=0; i<numVertices; i++)
    {
        vertices[i] = new Vector3f();
        texCoords[i] = new Vector2f();
        normals[i] = new Vector3f();
        sTangents[i] = new Vector3f();
        tTangents[i] = new Vector3f();
    }

    // calculate first ring.
    for (int i=0; i<prec+1; i++)
    {
        float amt = (float) toRadians(i * 360.0f / prec);

        // build the ring by rotating points around the origin, then moving them outward
        Vector3f ringPos = new Vector3f(0.0f, outer, 0.0f);
        ringPos.rotateAxis(amt, 0.0f, 0.0f, 1.0f);
        ringPos.add(new Vector3f(inner, 0.0f, 0.0f));
        vertices[i].set(ringPos);

        // compute texture coordinates for each vertex in the ring
        texCoords[i].set(0.0f, ((float)i/(float)prec));

        // compute tangents and normal vectors for each vertex in the ring
        tTangents[i] = new Vector3f(0.0f, -1.0f, 0.0f);    // The first tangent vector starts as the -Y axis,
        tTangents[i].rotateAxis(amt+(3.14159f/2.0f), 0.0f, 0.0f, 1.0f);
                                                            // and is then rotated around the Z axis.
        sTangents[i].set(0.0f, 0.0f, -1.0f);               // The second tangent is -Z in each case.
        normals[i] = tTangents[i].cross(sTangents[i]);     // The cross product produces the normal
    }

    // rotate the first ring about the Y axis to get the other rings
    for (int ring=1; ring<prec+1; ring++)
    {
        for (int vert=0; vert<prec+1; vert++)
        {
            // rotate the vertex positions of the original ring around the Y axis
            float amt = (float)toRadians((float)ring*360.0f/prec);
            Vector3f vp = new Vector3f(vertices[vert]);
            vp.rotateAxis(amt, 0.0f, 1.0f, 0.0f);
            vertices[ring*(prec+1)+vert].set(vp);

            // compute the texture coordinates for the vertices in the new rings
            texCoords[ring*(prec+1)+vert].set((float)ring*2.0f/(float)prec, texCoords[vert].y());

            // rotate the tangent and bitangent vectors around the Y axis
            sTangents[ring*(prec+1)+vert].set(sTangents[vert]);
            sTangents[ring*(prec+1)+vert].rotateAxis(amt, 0.0f, 1.0f, 0.0f);
            tTangents[ring*(prec+1)+vert].set(tTangents[vert]);
            tTangents[ring*(prec+1)+vert].rotateAxis(amt, 0.0f, 1.0f, 0.0f);

            // rotate the normal vector around the Y axis
            normals[ring*(prec+1)+vert].set(normals[vert]);
            normals[ring*(prec+1)+vert].rotateAxis(amt, 0.0f, 1.0f, 0.0f);
        }
    }

    // calculate triangle indices corresponding to the two triangles built per vertex
    for(int ring=0; ring<prec; ring++)
    {
        for(int vert=0; vert<prec; vert++)
        {
            indices[((ring*prec+vert)*2) *3+0]= ring*(prec+1)+vert;
            indices[((ring*prec+vert)*2) *3+1]=(ring+1)*(prec+1)+vert;
            indices[((ring*prec+vert)*2) *3+2]= ring*(prec+1)+vert+1;
            indices[((ring*prec+vert)*2+1)*3+0]= ring*(prec+1)+vert+1;
            indices[((ring*prec+vert)*2+1)*3+1]=(ring+1)*(prec+1)+vert;
            indices[((ring*prec+vert)*2+1)*3+2]=(ring+1)*(prec+1)+vert+1;
        }
    }
}

// accessors for the torus indices and vertices
int getNumIndices() { return numIndices; }
public int[] getIndices() { return indices; }
public int getNumVertices() { return numVertices; }
public Vector3f[] getVertices() { return vertices; }
public Vector2f[] getTexCoords() { return texCoords; }
public Vector3f[] getNormals() { return normals; }
public Vector3f[] getSTangents() { return sTangents; }
public Vector3f[] getTTangents() { return tTangents; }
}
```

```java
IntBuffer idxBuf = Buffers.newDirectIntBuffer(indices);
gl.glBufferData(GL_ELEMENT_ARRAY_BUFFER, idxBuf.limit()*4, idxBuf, GL_STATIC_DRAW);
}

in display()
...
gl.glBindBuffer(GL_ELEMENT_ARRAY_BUFFER, vbo[3]);
gl.glDrawElements(GL_TRIANGLES, numTorusIndices, GL_UNSIGNED_INT, 0);
```

注意，在使用 Torus 类的代码中，setupVertices() 里的循环现在对每个顶点关联的数据只存储一次，而不是像球体示例那样为每个索引条目各存储一次。这种差异也反映在要输入 VBO 的数据所声明的数组大小上。另请注意，在圆环体示例中，检索顶点数据时并没有使用索引值，而是直接将它们加载到 VBO #3 中。由于该 VBO 被指定为 GL_ELEMENT_ARRAY_BUFFER，OpenGL 知道该 VBO 包含顶点索引。

图 6.12 展示了实例化一个圆环体并用砖块纹理对其进行贴图的结果。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_168_0.png)

**图 6.12** 程序化生成的圆环体。

### 6.3 加载外部生成的模型

复杂的三维模型（例如视频游戏或计算机生成电影中的角色）通常使用建模工具制作。此类“DCC”（数字内容创作）工具使人们（例如艺术家）能够在三维空间中构建任意形状，并自动生成顶点、纹理坐标、顶点法线等。这类工具多得不胜枚举，但一些例子包括 Maya、Blender、Lightwave 和 Cinema4D 等。Blender 是免费且开源的。图 6.13 展示了编辑三维模型时 Blender 界面的一个示例。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_169_0.png)

为了让我们能在 OpenGL 场景中使用由 DCC 创建的模型，该模型需要以我们能够读取（导入）到程序中的格式保存（导出）。有几种标准的三维模型文件格式；同样，数量太多无法一一列举，但几个例子包括 Wavefront（.obj）、3D Studio Max（.3ds）、Stanford Scanning Repository（.ply）和 Ogre3D（.mesh）等。可以说最简单的是 Wavefront（通常称为 OBJ），因此我们将研究这一种。

OBJ 文件足够简单，因此我们可以相对容易地开发一个基本的导入器。在 OBJ 文件中，文本行指定顶点几何数据、纹理坐标、法线和其他信息。它有一些限制——例如，OBJ 文件无法指定模型动画。

OBJ 文件中的行以一个字符标签开头，指示该行上是什么类型的数据。一些常见标签包括

- v – 几何（顶点位置）数据
- vt – 纹理坐标
- `vn` – 顶点法线
- `f` – 面（通常是三角形中的顶点）

其他标签可以存储对象名称、其使用的材质、曲线、阴影以及许多其他细节。我们将讨论限制在上面列出的四个标签上，它们足以导入各种复杂模型。

假设我们使用 Blender 构建一个简单的金字塔，就像我们为程序 4.3 开发的那个一样。图 6.14 是在 Blender 中创建类似金字塔的截图。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_170_0.png)

**图 6.14** 在 Blender 中构建的金字塔。

在 Blender 中，如果我们现在*导出*金字塔模型，指定 .obj 格式，并设置 Blender 输出纹理坐标和顶点法线，就会创建一个包含所有这些信息的 OBJ 文件。生成的 OBJ 文件如图 6.15 所示。（纹理坐标的实际值可能因模型的构建方式而异。）

我们对 OBJ 文件的重要部分进行了颜色编码，以供参考。顶部以“#”开头的行是 Blender 放置在那里的注释，我们的导入器会忽略它们。其后是一行以“o”开头的内容，给出对象名称。我们的导入器也可以忽略这一行。再往后，有一行
