
## 6.1 程序化模型——构建球体

某些类型的对象（例如球体、圆锥体等）具有便于算法生成的数学定义。以半径为 R 的圆为例；其圆周上各点的坐标是明确定义的（图 6.1）。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_154_0.png)

**图 6.1**  
圆上的点。

我们可以系统地利用关于圆几何性质的知识，以算法方式构建球体模型。策略如下：

- 1. 选择一个*精度*，表示球体被划分成的圆形区域数量。在图 6.2 左侧，球体被切成四个区域。
- 2. 将每个圆形切片的圆周细分为若干点。见图 6.2 右侧。更多的点和水平切片会生成更精确、更平滑的球体模型。在我们的模型中，*每个切片将具有相同数量的点，包括最顶部和最底部（在这些位置，这些点是重合的）。*

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_154_1.png)

**图 6.2**  
为球体构建顶点。

- 3. 将顶点组织成三角形。一种方法是遍历顶点，在每一步构建两个三角形。例如，当我们沿着图 6.3 中球体上五个彩色顶点所在的行移动时，对于这五个顶点中的每一个，我们构建以对应颜色显示的两个三角形（具体步骤将在下文更详细地描述）。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_155_0.png)

- 4. 根据纹理图像的性质选择纹理坐标。对于球体，存在许多地形纹理图像，例如图 6.4 [VE21] 所示的地球纹理图像。如果我们采用这类纹理图像，那么通过想象该图像如图 6.5 所示“包裹”在球体上，我们就可以根据图像中纹素最终对应的位置，为每个顶点分配纹理坐标。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_155_1.png)

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_155_2.png)

- 5. 通常还希望为每个顶点生成*法向量*——即*垂直于模型表面*的向量。我们将在第 7 章中很快把它们用于*光照*。

确定法向量可能很棘手，但对于球体而言，从球心指向某个顶点的向量恰好等于该顶点的法向量！图 6.6 说明了这一性质（球心用“星号”标出）。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_156_0.png)

**图 6.6**  
球体顶点法向量。

一些模型使用*索引*来定义三角形。请注意，在图 6.3 中，每个顶点会出现在多个三角形中，这会导致每个顶点被多次指定。我们不必这样做，而是只存储每个顶点一次，然后为三角形的每个角指定索引，以引用所需的顶点。由于我们将存储顶点的位置、纹理坐标和法向量，因此对于大型模型而言，这有助于节省内存。

顶点存储在一维数组中，从最底部的水平切片中的顶点开始。使用索引时，关联的索引数组包含每个三角形角的一个条目。其内容是顶点数组的整数引用（具体而言是下标）。假设每个切片包含 *n* 个顶点，则顶点数组将如图 6.7 所示，同时图中还给出了对应索引数组的示例部分。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_157_0.png)

图 6.7  
顶点数组及对应的索引数组。

然后，我们可以从球体底部开始，以环形方式遍历每个水平切片上的顶点。当我们访问每个顶点时，构建两个三角形，形成一个位于该顶点上方和右侧的正方形区域，如图 6.3 所示。因此，处理过程被组织为如下嵌套循环：

```
for each horizontal slice i in the sphere (i ranges from 0 through all the slices in the sphere)
{
    for each vertex j in slice i (j ranges from 0 through all the vertices in the slice)
    {
        calculate indices for two triangles which point to neighboring vertices to the right,
        above, and to the above-right of vertex j
    }
}
```

例如，考虑图 6.3 中的“红色”顶点（图 6.8 中再次给出）。所讨论的顶点位于图 6.8 所示黄色三角形的左下角；按照刚才描述的循环，它的索引将是 `i*n+j`，其中 i 是当前正在处理的切片（外层循环），j 是该切片内当前正在处理的顶点（内层循环），n 是每个切片的顶点数。图 6.8 显示了该顶点（红色）及其三个相关相邻顶点，并给出了它们各自如何被索引的公式。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_157_1.png)

图 6.8  
为第 i 个切片中的第 j 个顶点生成的索引（n = 每个切片的顶点数）。

然后，这四个顶点用于构建为该（红色）顶点生成的两个三角形（以黄色显示）。这两个三角形在索引表中的六个条目在图中按数字 1 到 6 所示的顺序标出。注意，条目 3 和 6 都指向同一个顶点，条目 2 和 4 也是如此。因此，当我们处理到以红色高亮的顶点（即 `vertex[i*n+j]`）时，所定义的两个三角形由这六个顶点构建而成——一个三角形的条目标记为 1、2、3，引用顶点 `vertex[i*n+j]`、`vertex[i*n+j+1]` 和 `vertex[(i+1)*n+j]`；另一个三角形的条目标记为 4、5、6，引用三个顶点 `vertex[i*n+j+1]`、`vertex[(i+1)*n+j+1]` 和 `vertex[(i+1)*n+j]`。

程序 6.1 将我们的球体模型实现为一个名为 Sphere 的类。所得球体的中心位于原点。还展示了使用 Sphere 的代码。注意，每个顶点都存储为一组 JOML 类 Vector2f 和 Vector3f 的实例（这与之前的示例不同，之前顶点存储在 float 数组中）。Vector2f 和 Vector3f 包含以 float 值获取顶点 x、y、z 分量的方法，然后像以前一样将这些值放入 float 缓冲区。

注意 Sphere 类中三角形索引的计算，如前文图 6.8 所述。变量“prec”指“精度”，在此既用于球体切片数，也用于每个切片的顶点数。由于纹理映射会完全环绕球体，因此在纹理图左右边缘相接的每个位置，我们都需要一个额外的重合顶点。因此，顶点总数为 `(prec+1)*(prec+1)`。由于每个顶点生成六个三角形索引，所以索引总数为 `prec*prec*6`。

### 程序 6.1 程序化生成的球体

#### Sphere 类

```java
import org.joml.*;
import static java.lang.Math.*;

public class Sphere
{
    private int numVertices, numIndices, prec;   // prec = precision
    private int[] indices;
    private Vector3f[] vertices;
    private Vector2f[] texCoords;
    private Vector3f[] normals;

    public Sphere(int p)
    {
        prec = p;
        initSphere();
    }

    private void initSphere()
    {
        numVertices = (prec+1) * (prec+1);
        numIndices = prec * prec * 6;
        indices = new int[numIndices];
        vertices = new Vector3f[numVertices];
        texCoords = new Vector2f[numVertices];
        normals = new Vector3f[numVertices];
        for (int i=0; i<numVertices; i++) {
            vertices[i] = new Vector3f();
            texCoords[i] = new Vector2f();
            normals[i] = new Vector3f();
        }

        // calculate triangle vertices
        for (int i=0; i<=prec; i++) {
            for (int j=0; j<=prec; j++) {
                float y = (float)Math.cos(toRadians(180-i*180/prec));
                float x = -(float)Math.cos(toRadians(360/(float)prec)*j) * (float)Math.abs(Math.asin(y));
                float z = (float)Math.sin(toRadians(360/(float)prec)*j) * (float)Math.abs(Math.asin(y));
                vertices[i*(prec+1)+j].set(x,y,z);
                texCoords[i*(prec+1)+j].set((float)j/prec, (float)i/prec);
                normals[i*(prec+1)+j].set(x,y,z);
            }
        }

        // calculate triangle indices
        for(int i=0; i<prec; i++) {
            for(int j=0; j<prec; j++) {
                indices[6*(i*prec+j)+0] = i*(prec+1)+j;
                indices[6*(i*prec+j)+1] = i*(prec+1)+j+1;
                indices[6*(i*prec+j)+2] = (i+1)*(prec+1)+j;
                indices[6*(i*prec+j)+3] = i*(prec+1)+j+1;
                indices[6*(i*prec+j)+4] = (i+1)*(prec+1)+j+1;
                indices[6*(i*prec+j)+5] = (i+1)*(prec+1)+j;
            }
        }
    }

    public int getNumIndices() { return numIndices; }
    public int getNumVertices() { return numVertices; }
    public int[] getIndices() { return indices; }
    public Vector3f[] getVertices() { return vertices; }
    public Vector2f[] getTexCoords() { return texCoords; }
    public Vector3f[] getNormals() { return normals; }
}
```
