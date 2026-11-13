

```cpp
const int ISIZE = 512; //image size
const int NSIZE = 64; //noise texture size
const int NOISE = 32; //how many noise frames
const float NFSPOT = 4; //size of noise spots
const int NSOT = NSIZE/(NFSPOT-NSIZE);
GLuint frame[NOISE+1]; //noise and work textures
int texture = 0; //frame counter

float f(int t) //Periodic function
{ return (t>127)? 1 : 0; }

void advect() //Advect the work texture
{
for(int i=0;i<ISIZE;i++)
{
glBegin(GL_POLYGON);
for(int j=0;j<ISIZE;++j)
{
glTexCoord2f(xij, yij);
glVertex2f(xij + v(xij)*Dt, yij + v(yij)*Dt);
}
glEnd();
}
}

void inject() //Inject noise
{
glEnable(GL_BLEND);
glBindTexture(GL_TEXTURE_2D, tex[frame % NOISE]);
glBegin(GL_QUAD);
glTexCoord2f(0,0); glVertex2f(0,0);
glTexCoord2f(T,0); glVertex2f(1,0);
glTexCoord2f(T,T); glVertex2f(1,1);
glTexCoord2f(0,T); glVertex2f(0,1);
glEnd();
glDisable(GL_BLEND);
}

void init(float alpha)
{
glViewport(0,0,ISIZE,ISIZE); //Select a 1-to-1 mapping of
glMatrixMode(GL_PROJECTION); //the texture to the frame buffer
glLoadIdentity();
glScalef(2.2,1,-1,0);
glEnable(GL_TEXTURE_2D);
glBlendFunc(GL_SRC_ALPHA, GL_ONE_MINUS_SRC_ALPHA);
glGenTextures(NOISE+1, tex);

int phase[NSIZE][NSIZE];
float noise[NSIZE][NSIZE][2];
```

for (int i=0;i<NSIZE;i++) //Make spatial noise
for (int j=0;j<NSIZE;j++)
phase[i][j] = rand() % 256;

for (int k=0;k<NOISE;k++) //Make temporal noise
{
int t = k*256/NOISE;
for (int i=0;i<NSIZE;i++)
for (int j=0;j<NSIZE;j++)
{
noise[i][j][0] = f((t+phase[i][j]) % 256);
noise[i][j][1] = alpha;
}
}
glBindTexture(GL_TEXTURE_2D, tex[k]);
glTexImage2D(GL_TEXTURE_2D, 0, GL_LUMINANCE_ALPHA, NSIZE, NSIZE,
0, GL_LUMINANCE_ALPHA, GL_FLOAT, noise);
}

void run()
{
init(0.10);
for(;; frame++)
{
advect();
inject();
//Copy frame buffer to work texture
glBindTexture(GL_TEXTURE_2D, tex[NOISE]);
glCopyTexImage2D(GL_TEXTURE_2D, 0, GL_RGB, 0, 0, ISIZE, ISIZE, 0);
}
}
```

清单 6.2. 续。

## 6.6.3 IBFV 示例

图 6.28 展示了使用 IBFV 方法可视化的两个二维流场数据集示例。在左图中，生成的流场纹理被编码在亮度通道中，而色调则通过从蓝到红的颜色映射显示矢量大小。在右图中，流场纹理的亮度直接由矢量大小调制，因此亮区域表示高速区域。可以看到，这些 IBFV 动画的静态快照与 LIC 方法的结果（参见图 6.25(b)）具有非常相似的外观。

此示例还说明了基于纹理的可视化的更多可能性。除了灰色噪声纹理本身之外，三个红、绿、蓝色的圆盘状“墨迹源”在流场中被平流。如果我们使用

![](img/1274306e378c42ed8a0ad5669902d2a1_244_0.png)

图 6.28. (a) 使用颜色编码速度大小的基于纹理的可视化。(b) 使用亮度编码速度大小和三个墨迹源的基于纹理的可视化。

IBFV 方法实现可视化，墨迹源的平流操作仅需在绘制噪声纹理后，将其绘制在每一帧之上（清单 6.2 中的步骤 77）。墨迹源的位置在图像中以白色圆圈表示。平流的彩色墨迹留下的痕迹是基于纹理的等效物，相当于在墨迹源处播种的一组密集流线。然而，存在两点差异。从有限点种子集进行流线追踪将产生一组密集但各不相同的、不透明度恒定的几何原语。相比之下，基于纹理的墨迹平流会产生一幅连续且逐渐褪色的图像。

两种方法各有其特定的优势和侧重点。流线常用于精确的工程应用，其中需要准确确定从精确指定的种子位置出发的点的轨迹。墨迹平流有助于了解给定种子区域的流动如何在更大的域中扩散。在高正散度点（参见第 6.1 节）放置不同颜色的墨迹源，并让它们平流直到过程在视觉上收敛，将生成一幅图像，显示流域被分解为多个空间分量，这些分量根据其对应的源以不同颜色着色。分隔这些区域的曲线称为分叉线，是向量场研究中的重要高级概念。

曲面上的 IBFV。基于纹理的可视化并不局限于二维平面域。图 6.29(a) 显示了在三维表面上的基于纹理的可视化。实际表面是本节前面介绍的三维流场数据集的矢量大小等值面（例如，参见图 6.19）。在这个等值面上，我们

![](img/1274306e378c42ed8a0ad5669902d2a1_245_0.png)

图 6.29. 基于图像的流场可视化，用于 (a) 三维表面和 (b) 体数据集。

首先将矢量场投影，然后使用与二维情况相同类型的基于纹理的矢量可视化。在表面上的纹理中添加了阴影，以传达关于对象几何的空间线索。由于这是速度大小的等值面，像我们在二维情况中那样对矢量大小进行颜色编码将是无用的（参见图 6.28）。然而，在实践中，其他可用的标量属性可以通过颜色显示，例如压力、温度、涡度或散度。

三维体积上的 IBFV。最后，我们指出，基于纹理的矢量场可视化也可以应用于体数据集。图 6.29(b) 使用先前为二维图像讨论过的 IBFV 基于纹理方法的三维等效方法（Telea and van Wijk 03）来可视化一个简单的三维螺旋流。与图 6.28(b) 所示的二维可视化类似，使用多个彩色墨迹源来补充灰度噪声。三维 IBFV 方法遵循与二维平面和三维曲面方法类似的平流-注入原则，但存在一些显著差异。首先，生成密集的基于纹理的可视化需要使用三维纹理（其在显卡上的支持仍不如二维纹理广泛）或二维纹理堆栈。其次，平流步骤在 OpenGL 中通过为二维情况绘制变形和贴图的多边形直接支持，但在三维中没有对应物。事实上，目前 OpenGL 中没有三维（体积）绘制原语，这种情况可能还会持续一段时间。在三维中实现平流步骤可以通过将其归约为二维原语渲染的堆栈来完成（Telea and van Wijk 03）。最后，为了能够看到三维密集流场纹理内部，三维情况下的注入步骤通过向灰度噪声添加 alpha（透明度）噪声进行了修改

到灰度噪声中。alpha 噪声扮演着注入到流体积中的“擦除器”的角色，产生稀疏填充的可视化，使人能够看到流域内部（参见图 6.29(b)）。

要可视化三维 IBFV 方法的结果，我们需要渲染生成的纹理体积，该体积包含颜色和 alpha（透明度）值。这可以使用一种称为 *基于纹理的体积渲染* 的可视化技术来完成，该技术将在单独的第 10.4 节中描述。

## 6.7 向量场的简化表示

在前一节中，我们看到了许多用于向量场的可视化技术，从基于种子的方法（如矢量符号和流线）到产生密集表示的方法（如基于纹理的技术）。所有这些方法的有效性很大程度上取决于它们传达对给定数据集所需洞察的能力。在许多应用中，这并不意味着以相同的方式可视化所有数据点。对于应用领域具有重要特征的区域，例如涡旋、速度极值或层流区域之间的分离线，应以不同于不太重要区域的方式进行可视化，以帮助用户在数据集中检测它们的存在。这些区域也称为向量场的 *特征*。

这种对向量场进行选择性可视化的主要原因之一是数据的巨大规模。正如我们在三维场的情况中所见，由于遮挡，密集的可视化可能很难解释。如果简化保留（并强调）感兴趣的特征并移除大量不感兴趣的数据，那么为大型数据集设计使用向量场 *简化* 版本的可视化是有益的。此外，如果我们事先知道这些特征在数据集中的位置，可以在这些位置放置可视化原语，例如矢量符号或流对象，而不是对整个域进行密集采样。存在几种采用这种方法的可视化方法，将在以下各节中描述。

### 6.7.1 向量场拓扑

考虑图 6.30(a) 中使用 IBFV 技术显示的二维向量场。该向量场是通过合并两个源（红色显示）和两个汇（蓝色显示）的效果合成生成的。类似于图 6.28(b) 所示的应用，我们问自己：二维流域中的哪些区域的流动被汇收集，分别哪些

