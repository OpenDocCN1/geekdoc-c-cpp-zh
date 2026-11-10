
有些顶点会参与不止一个三角形，在这些情况下可能会使用不同的纹理坐标。

绿色（以“vn”开头）的值是各种法向量。这个列表通常也比顶点列表长（尽管本例中并非如此），同样是因为有些顶点参与不止一个三角形，在这些情况下可能会使用不同的法向量。

文件底部附近紫色（以“f”开头）的值指定三角形（即“面”）。在本例中，每个面（三角形）有三个元素，每个元素包含三个用“/”分隔的值（OBJ 也允许其他格式）。每个元素的值分别是指向顶点列表、纹理坐标列表和法向量列表的索引。例如，第三个面是

```
f 2/7/3 5/8/3 3/9/3
```

这表示顶点列表（蓝色部分）中的第二个、第五个和第三个顶点组成一个三角形（注意 OBJ 索引从 1 开始）。对应的纹理坐标是红色部分纹理坐标列表中的第七个、第八个和第九个。三个顶点具有相同的法向量，即绿色部分法向量列表中的第三个。

OBJ 格式的模型不要求包含法向量，甚至不要求包含纹理坐标。如果模型没有纹理坐标或法向量，面值将只指定顶点索引：

```
f 2 5 3
```

如果模型有纹理坐标但没有法向量，格式将如下：

```
f 2/7 5/8 3/9
```

并且，如果模型有法向量但没有纹理坐标，格式将是

```
f 2//3 5//3 3//3
```

一个模型拥有数万个顶点并不罕见。互联网上有数百个此类模型可供下载，几乎涵盖所有能想到的应用，包括动物、建筑、汽车、飞机、神话生物、人物等模型。

互联网上有各种复杂程度的程序可以导入 OBJ 模型。另外，编写一个非常简单的 OBJ 加载器函数也相对容易，它可以处理我们已经见过的基本标签（v、vt、vn 和 f）。程序6.3 展示了一个这样的加载器，尽管它*非常*受限。它包含一个用于保存任意导入模型的类，该类又调用导入器。

在描述这个简单 OBJ 导入器的代码之前，我们必须提醒读者它的局限性：

-   它仅支持包含*全部三种*面属性字段的模型。也就是说，顶点位置、纹理坐标和法向量*必须全部*存在，并且格式为 f ###/###/###。
-   材质标签通常用于指定纹理文件，这里会被忽略——纹理化必须使用第5章所述的方法完成。
-   仅支持由单个三角形网格组成的 OBJ 模型（OBJ 格式支持由多个网格组成的模型，但我们这个简单导入器不支持）。
-   它假设每一行上的元素之间恰好用一个空格分隔。

如果你有一个不满足上述所有条件的 OBJ 模型，并且希望使用程序6.3 中的简单加载器导入它，这样做*可能*仍然可行。通常可以将此类模型加载到 Blender 中，然后将其导出为另一个符合该加载器限制的 OBJ 文件。例如，如果模型不包含法向量，可以让 Blender 在导出修改后的 OBJ 文件时生成法向量。

我们 OBJ 加载器的另一个局限与索引有关。观察前面的描述，“face”标签允许混合匹配顶点位置、纹理坐标和法向量。例如，两个不同的“face”行可能包含指向同一条 v 条目但不同 vt 条目的索引。不幸的是，OpenGL 的索引机制不支持这种程度的灵活性——OpenGL 中的索引条目只能指向某个特定顶点*及其属性*。这使编写 OBJ 模型加载器稍微复杂一些，因为我们不能简单地将三角形面条目中的引用复制到索引数组中。相反，使用 OpenGL 索引需要确保一个面条目中的 v、vt 和 vn 值的整个*组合*在索引数组中都有各自的引用。一个更简单但效率较低的替代方案是为每个三角形面条目创建一个新顶点。为了清晰起见，我们在这里选择这种更简单的方法，尽管使用 OpenGL 索引具有节省空间的优势（尤其是在加载较大模型时）。

ModelImporter 类包含一个 parseOBJ() 函数，它逐行读取 OBJ 文件的每一行，分别处理 v、vt、vn 和 f 四种情况。在每种情况下，都会提取该行中后续的数字：首先使用 substring() 跳过开头的 v、vt、vn 或 f 字符，然后使用 split() 函数返回的迭代器提取每个后续参数值，并将它们存储到 ArrayList 中。处理面（f）条目时，会构建顶点，并在并行数组中为顶点位置、纹理坐标和法向量保存对应条目。

ModelImporter 类嵌入在 ImportedModel 类中，后者通过将导入的顶点放入 Vector3f 和 Vector2f 对象数组，简化了 OBJ 文件顶点的加载和访问。回想一下，这些是 JOML 类；我们在这里用它们存储顶点位置、纹理坐标和法向量。然后，ImportedModel 类中的访问器以与 Sphere 和 Torus 类中大致相同的方式，使这些数据可供 Java/JOGL 应用程序使用。

在 ModelImporter 和 ImportedModel 类之后，是一段示例调用序列，用于加载 OBJ 文件，然后将顶点信息传输到一组 VBO 中以便后续渲染。

图6.16 展示了一个渲染后的航天飞机模型，该模型以 OBJ 文件形式从 NASA 网站 [NA21] 下载，使用程序6.3 中的代码导入，并使用程序5.1 中的代码配合相关的 NASA 纹理图像文件进行纹理化，且启用了各向异性过滤。这个纹理图像是*UV映射*应用的一个示例，其中模型中的纹理坐标被仔细映射到纹理图像的特定区域。（正如*第5章*所述，*UV映射*的细节超出了本书范围。）

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_174_0.png)

**图6.16**
带纹理的 NASA 航天飞机模型。

## 程序6.3 简单（受限）OBJ 加载器

### ImportedModel 类

```java
public class ImportedModel
{
  private Vector3f[] vertices;
  private Vector2f[] texCoords;
  private Vector3f[] normals;
  private int numVertices;

  public ImportedModel(String filename)
  {
    ModelImporter modelImporter = new ModelImporter();
    try
    {
      modelImporter.parseOBJ(filename);    // uses modelImporter to get vertex information
      numVertices = modelImporter.getNumVertices();
      float[] verts = modelImporter.getVertices();
      float[] tcs = modelImporter.getTextureCoordinates();
      float[] norms = modelImporter.getNormals();

      vertices = new Vector3f[numVertices];
      texCoords = new Vector2f[numVertices];
      normals = new Vector3f[numVertices];

      for(int i=0; i<vertices.length; i++)
      {
        vertices[i] = new Vector3f();
        vertices[i].set(verts[i*3], verts[i*3+1], verts[i*3+2]);
        texCoords[i] = new Vector2f();
        texCoords[i].set(tcs[i*2], tcs[i*2+1]);
        normals[i] = new Vector3f();
        normals[i].set(norms[i*3], norms[i*3+1], norms[i*3+2]);
      }
    } catch (IOException e)
    {
      e.printStackTrace();
    }
  }

  public int getNumVertices() { return numVertices; }    // accessors
  public Vector3f[] getVertices() { return vertices; }
  public Vector2f[] getTexCoords() { return texCoords; }
  public Vector3f[] getNormals() { return normals; }
}
```

### ModelImporter 嵌套类

```java
private class ModelImporter
{  // values as read in from OBJ file
   private ArrayList<Float> vertVals = new ArrayList<Float>();
   private ArrayList<Float> stVals = new ArrayList<Float>();
   private ArrayList<Float> normVals = new ArrayList<Float>();
```
