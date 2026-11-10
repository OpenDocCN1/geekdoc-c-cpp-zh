


```java
// values stored for later use as vertex attributes
private ArrayList<Float> triangleVerts = new ArrayList<Float>();
private ArrayList<Float> textureCoords = new ArrayList<Float>();
private ArrayList<Float> normals = new ArrayList<Float>();

public void parseOBJ(String filename) throws IOException
{
    InputStream input = new FileInputStream(new File(filename));
    BufferedReader br = new BufferedReader(new InputStreamReader(input));
    String line;
    while ((line = br.readLine()) != null)
    {
        if(line.startsWith("v"))                                      // vertex position ("v" case)
        {
            for(String s : (line.substring(2)).split(" "))
            {
                vertVals.add(Float.valueOf(s));                        // extract the vertex position values
            }
        }
        else if(line.startsWith("vt"))                                // texture coordinates ("vt" case)
        {
            for(String s : (line.substring(3)).split(" "))
            {
                stVals.add(Float.valueOf(s));                          // extract the texture coordinate values
            }
        }
        else if(line.startsWith("vn"))                                // vertex normals ("vn" case)
        {
            for(String s : (line.substring(3)).split(" "))
            {
                normalVals.add(Float.valueOf(s));                      // extract the normal vector values
            }
        }
        else if(line.startsWith("f"))                                 // triangle faces ("f" case)
        {
            for(String s : (line.substring(2)).split(" "))
            {
                String v = s.split("/")[0];                           // extract triangle face references
                String vt = s.split("/")[1];
                String vn = s.split("/")[2];

                int vertRef = (Integer.valueOf(v)-1)*3;
                int tcRef = (Integer.valueOf(vt)-1)*2;
                int normRef = (Integer.valueOf(vn)-1)*3;

                triangleVerts.add(vertVals.get(vertRef));              // build array of vertices
                triangleVerts.add(vertVals.get(vertRef+1));
                triangleVerts.add(vertVals.get(vertRef+2));

                textureCoords.add(stVals.get(tcRef));                  // build array of
                textureCoords.add(stVals.get(tcRef+1));                // texture coordinates.

                normals.add(normalVals.get(normRef));                    // ... and normals
                normals.add(normalVals.get(normRef+1));
                normals.add(normalVals.get(normRef+2));
            }
        }
    }
    input.close();
}

// accessors for retrieving the number of vertices, the vertices themselves,
// and the corresponding texture coordinates and normals (only called once per model)

public int getNumVertices() { return (triangleVerts.size()/3); }

public float[] getVertices()
{
    float[] p = new float[triangleVerts.size()];
    for(int i = 0; i < triangleVerts.size(); i++)
    {
        p[i] = triangleVerts.get(i);
    }
    return p;
}
// similar accessors for texture coordinates and normal vectors go here
}
```

## 使用模型导入器

```java
...
myModel = new ImportedModel("shuttle.obj");              // in init()
...
private void setupVertices()
{   GL4 gl = (GL4) GLContext.getCurrentGL();

    numObjVertices = myModel.getNumVertices();
    Vector3f[] vertices = myModel.getVertices();
    Vector2f[] texCoords = myModel.getTexCoords();
    Vector3f[] normals = myModel.getNormals();

    float[] pvalues = new float[numObjVertices*3];        // vertex positions
    float[] tvalues = new float[numObjVertices*2];        // texture coordinates
    float[] nvalues = new float[numObjVertices*3];        // normal vectors

    for (int i=0; i<numObjVertices; i++)
    {
        pvalues[i*3]   = (float) (vertices[i].x());
        pvalues[i*3+1] = (float) (vertices[i].y());
        pvalues[i*3+2] = (float) (vertices[i].z());
        tvalues[i*2]   = (float) (texCoords[i].x());
        tvalues[i*2+1] = (float) (texCoords[i].y());
        nvalues[i*3]   = (float) (normals[i].x());
        nvalues[i*3+1] = (float) (normals[i].y());
        nvalues[i*3+2] = (float) (normals[i].z());
    }
    gl.glGenVertexArrays(vao.length, vao, 0);
    gl.glBindVertexArray(vao[0]);
    gl.glGenBuffers(vbo.length, vbo, 0);
}
```

## 练习

- 6.1 修改程序4.4，使“太阳”“行星”和“月亮”成为带纹理的*球体*，例如图4.11所示的球体。

- 6.2 *（项目）* 修改练习6.1中的程序，使图6.16中导入的NASA航天飞机对象也绕“太阳”运行。你会希望尝试对航天飞机应用缩放和旋转，使其看起来更真实。

- 6.3 *（研究与项目）* 学习如何使用Blender创建自己的3D对象的基础知识。要在OpenGL应用程序中充分利用Blender，你会希望学习如何使用Blender的UV展开工具生成纹理坐标和关联的纹理图像。然后可以将对象导出为OBJ文件，并使用程序6.3中的代码加载它。

## 参考文献

- **[BL21]** Blender，Blender基金会，访问于2021年3月，https://www.blender.org/

- **[CH11]** A. Chopin，*3D艺术基础：3D建模、纹理与动画基础*（Focal Press，2011）。

- **[CH21]** 计算机历史博物馆，访问于2021年3月，http://www.computerhistory.org/revolution/computer-graphics-music-and-art/15/206

- **[GL21]** GLUT与OpenGL实用库，访问于2021年3月，https://www.opengl.org/resources/libraries/

- **[NA21]** NASA 3D资源，访问于2021年3月，http://nasa3d.arc.nasa.gov/

- **[PP07]** P. Baker，*保罗的项目*，2007，访问于2021年3月，www.paulsprojects.net

- **[VA12]** V. Vaughan，*数字建模*（New Riders，2012）。

- **[VE21]** Visible Earth，NASA戈达德太空飞行中心图像，访问于2021年3月，http://visibleearth.nasa.gov

光照模型有时被称为*着色模型*，尽管在有着色器编程的情况下，这可能有点令人困惑。有时会使用*反射模型*这一术语，使术语更加复杂。我们将尽量坚持使用最简单、最实用的术语。

当今最常见的光照模型被称为“ADS”模型，因为它们基于标记为A、D和S的三类反射：

- 环境反射模拟一种低强度照明，它同等地影响场景中的所有物体。

- 漫反射根据光的入射角以不同程度照亮物体。

- 镜面反射通过在物体表面将大小合适的高光策略性地放置在光线最直接反射向观察者眼睛的位置，来表现物体的光泽度。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_182_0.png)

图7.1
ADS光照贡献。

ADS模型可用于模拟不同的光照效果和多种材质。

图7.1展示了位置光对一个闪亮金色圆环的环境、漫反射和镜面反射贡献。

回想一下，场景最终是通过片段着色器为屏幕上的每个像素输出颜色来绘制的。使用ADS光照模型需要指定光照对像素RGBA输出值的贡献。影响因素包括：

- 光源类型及其环境、漫反射和镜面反射特性

- 物体材质的环境、漫反射和镜面反射特性

- 物体材质指定的“光泽度”

- 光线照射到物体的角度

- 场景被观察的角度

### 5.2.2 光源

光源有许多类型，每种类型具有不同特性，并且模拟其效果需要不同的步骤。一些类型包括：

- 全局光（通常称为“全局环境光”），因为它只包含环境分量

- 定向光（或“远距离光”）

- 位置光（或“点光源”）

- 聚光灯

*全局环境光*是最容易建模的光源类型。全局环境光没有光源位置——无论物体位于何处，场景中每个物体的每个像素处的光都相同。全局环境光模拟现实世界中的一种现象：光经过多次反弹后，其来源和方向无法确定。全局环境光只有环境分量，以RGBA值指定；它没有漫反射或镜面反射分量。例如，全局环境光可以定义如下：

```java
float[] globalAmbient = new float[] { 0.6f, 0.6f, 0.6f, 1.0f };
```

RGBA值的范围是0到1，因此全局环境光通常建模为暗白光，其中每个RGB值都设置为0到1之间的相同小数值，alpha设置为1。

*定向光*或*远距离光*也没有光源位置，但它有一个*方向*。它适用于光源距离很远、光线实际上平行的情况，例如来自太阳的光。在许多此类情况下，我们可能只对光源建模感兴趣，而不对产生光的物体建模。定向光对物体的影响取决于光的照射角度；物体面向定向光的一侧比切向或相反的一侧更亮。对定向光建模需要指定其方向（作为向量）及其环境、漫反射和镜面反射特性（作为RGBA值）。一个指向负Z轴方向的红色定向光可以如下指定：

```java
float[] dirLightAmbient = new float[] { 0.1f, 0.0f, 0.0f, 1.0f };
float[] dirLightDiffuse = new float[] { 1.0f, 0.0f, 0.0f, 1.0f };
float[] dirLightSpecular = new float[] { 1.0f, 0.0f, 0.0f, 1.0f };
float[] dirLightDirection = new float[] { 0.0f, 0.0f, -1.0f };
```


