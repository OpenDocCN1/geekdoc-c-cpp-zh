

```
TextureCoordinates="0,0 1,0 1,1 1,1 0,1 0,0 "
Positions="-0.5,-0.5,0.5 0.5,-0.5,0.5 0.5,0.5,0.5 0.5,0.5,0.5 0.5,0.5,0.5 -0.5,-0.5,0.5" />
</GeometryModel3D.Geometry>
<GeometryModel3D.Material>
<diffuseMaterial>
<diffuseMaterial.Brush>
<DrawingBrush Viewport="0,0.3,0.1,0.1"
TileMode="FlipXY">
<DrawingBrush.Drawing>
<drawingGroup>
<drawingGroup.Children>
<GeometryDrawing Geometry="M0,0.1 L0.1,0 1,0.9, 0.9,1z" Brush="Pink" />
<GeometryDrawing
Geometry="M0.25,0.25 L0.5,0.125 0.75,0.25 0.5,0.5z" Brush="Aqua" />
<GeometryDrawing
Geometry="M0.25,0.75 L0.5,0.875 0.75,0.75 0.5,0.5z" Brush="Salmon" />
<GeometryDrawing
Geometry="M0.25,0.75 L0.125,0.5 0.25,0.25 0.5,0.5z" Brush="Red" />
</DrawingGroup.Children>
</DrawingGroup>
</DrawingBrush.Drawing>
</DrawingBrush>
</diffuseMaterial.Brush>
</diffuseMaterial>
</GeometryModel3D.Material>
<GeometryModel3D.Transform>
<RotateTransform3D>
<RotateTransform3D.Rotation>
<AxisAngleRotation3D Axis="0,2,1" Angle="30" />
</RotateTransform3D.Rotation>
</RotateTransform3D>
</GeometryModel3D.Transform>
</GeometryModel3D>
</ModelVisual3D.Content>
</ModelVisual3D>
</Viewport3D.Children>
</Viewport3D>
</Canvas>
</Page>
```

在清单 12.15 中，创建了一个 3D 图案。3D 模型上的 Material 对象使用 DrawingBrush 类添加。在运行代码之前，您必须在 App.xaml 文件中将 StartupUri 属性设置为 Page1.xaml。当您通过按键盘上的 F5 键运行应用程序时，您会得到输出，如图 12.19 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_594_0.png)

图 12.19：使用 DrawingBrush 类添加材质

## 添加摄像机

您创建的 3-D 场景实际上是 3-D 对象的 2-D 表示。它根据观看者的视角而不同；因此，您必须指定视角。为此，在 WPF 中使用 Camera 类来指定 3-D 场景的视点。WPF 中有三种类型的摄像机可供使用，分别由 MatrixCamera、OrthographicCamera 和 PerspectiveCamera 类实现。在本节中，我们讨论 WPF 中两种最重要且最常用的摄像机类：

- OrthographicCamera
- PerspectiveCamera

## OrthographicCamera

OrthographicCamera 类描述的是与视角平行的点，而不是摄像机中各边汇聚于一点的点。您已在本章的 In Depth 部分详细了解过 OrthographicCamera 类。让我们学习 OrthographicCamera 类的使用方法。为此，创建一个名为 OrthographicCamera 的 WPF 应用程序（也在 CD 上提供）并将清单 12.16 中的代码添加到 MainWindow.xaml 文件中：

### 清单 12.16：使用 OrthographicCamera 类

```
<Window x:Class="OrthographicCamera.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="MainWindow" Height="300" Width="300">
<Grid>
    <Viewport3D>
        <Viewport3D.Camera>
            <OrthographicCamera LookDirection="7,-3,-4" UpDirection="1,1,100" Position="-5.5,2.5,3" />
        </Viewport3D.Camera>
        <ModelVisual3D>
            <ModelVisual3D.Content>
                <Model3DGroup>
                    <GeometryModel3D>
                        <GeometryModel3D.Geometry>
<MeshGeometry3D Positions="-1 -1 0 1 -1 0 -1 1 0 1 1 0" Normals="0 0 1 0 0 1 0 0 1 0 0 1" TextureCoordinates="1 0 1 1 0 0 1 0" TriangleIndices="0 1 2 1 3 2" />
                        </GeometryModel3D.Geometry>
                        <GeometryModel3D.Material>
                            <DiffuseMaterial>
                                <DiffuseMaterial.Brush>
                                    <LinearGradientBrush StartPoint="0,0.5" EndPoint="1,0.5" Opacity="0.9">
                                        <LinearGradientBrush.GradientStops>
                                            <GradientStop Color="wheat" Offset="0.1"/>
                                            <GradientStop Color="Pink" Offset="0.75"/>
                                        </LinearGradientBrush.GradientStops>
                                    </LinearGradientBrush>
                                </DiffuseMaterial.Brush>
                            </DiffuseMaterial>
                        </GeometryModel3D.Material>
                    </GeometryModel3D>
                </Model3DGroup>
            </ModelVisual3D.Content>
        </ModelVisual3D>
    </Viewport3D>
</Grid>
</Window>
```

在清单 12.16 中，使用 OrthographicCamera 类创建了一个实体图形并在表面上查看。当您通过按键盘上的 F5 键运行应用程序时，您会得到输出，如图 12.20 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_596_0.png)

图 12.20：显示 OrthographicCamera 应用程序的输出

## PerspectiveCamera

PerspectiveCamera 类指定使场景变短的投影。它描述的是各边向地平线上的一个点收敛的区域。您已在本章的 In Depth 部分详细了解过 PerspectiveCamera 类。让我们学习 PerspectiveCamera 类的使用方法。为此，创建一个名为 PerspectiveCamera 的 WPF 应用程序（可在 CD 上获得）并将清单 12.17 中的代码添加到 MainWindow.xaml 文件中：

### 清单 12.17：使用 PerspectiveCamera 类

```
<Window x:Class="PerspectiveCamera.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="MainWindow" Height="300" Width="300">
<Grid>
<Viewport3D>
<Viewport3D.Camera>
<PerspectiveCamera LookDirection="6,-3,-4" upDirection="0,0,1" Position="-5,2.5,3" FieldOfView="30" />
</Viewport3D.Camera>
<ModelVisual3D>
<ModelVisual3D.Content>
<Model3DGroup>
<GeometryModel3D>
<GeometryModel3D.Geometry>
<MeshGeometry3D Positions="-1 -1 0 1 -1 0 -1 1 0 1 1" Normals="0 0 1 0 0 1 0 0 1 0 0 1" TextureCoordinates="1 0 1 1 0 0 1 0" TriangleIndices="0 1 2 1 3 2" />
</GeometryModel3D.Geometry>
<GeometryModel3D.Material>
<DiffuseMaterial>
<DiffuseMaterial.Brush>
<LinearGradientBrush StartPoint="0,0.5" EndPoint="1,0.5" Opacity="0.9">
<LinearGradientBrush.GradientStops>
<GradientStop Color="Wheat" Offset="0.1"/>
<GradientStop Color="Pink" Offset="0.75"/>
</LinearGradientBrush.GradientStops>
</LinearGradientBrush>
</DiffuseMaterial.Brush>
</DiffuseMaterial>
</GeometryModel3D.Material>
</GeometryModel3D>
```

```
</ModelVisual3D.Content>
</ModelVisual3D>
<ModelVisual3D>
    <ModelVisual3D.Content>
        <GeometryModel3D>
            <GeometryModel3D.Geometry>
                <MeshGeometry3D
                    TriangleIndices="0,1,2 3,4,5 "
                    Normals="0,0,1 0,0,1 0,0,1 0,0,1 0,0,1 0,0,1 "
                    TextureCoordinates="0,0 1,0 1,1 1,1 0,1 0,0 "
                    Positions="-0.5,-0.5,0.5 0.5,-0.5,0.5 0.5,0.5,0.5 0.5,0.5,0.5 -0.5,0.5,0.5 -0.5,-0.5,0.5 " />
            </GeometryModel3D.Geometry>
            <GeometryModel3D.Material>
                <MaterialGroup>
                    <DiffuseMaterial>
                        <DiffuseMaterial.Brush>
                            <LinearGradientBrush StartPoint="0,0" EndPoint="1,1">
                                <LinearGradientBrush.GradientStops>
                                    <GradientStop Color="Blue" offset="0" />
                                    <GradientStop Color="White" Offset="0.25" />
                                    <GradientStop Color="Red" Offset="0.75" />
                                </LinearGradientBrush.GradientStops>
                            </LinearGradientBrush>
                        </DiffuseMaterial.Brush>
                    </DiffuseMaterial>
                </MaterialGroup>
            </GeometryModel3D.Material>
            <GeometryModel3D.Transform>
                <RotateTransform3D>
                    <RotateTransform3D.Rotation>
                        <AxisAngleRotation3D Axis="0,2,1" Angle="40" />
                    </RotateTransform3D.Rotation>
                </RotateTransform3D>
            </GeometryModel3D.Transform>
        </GeometryModel3D>
    </ModelVisual3D.Content>
</ModelVisual3D>
</Viewport3D.Children>
</Viewport3D>
<Viewport3D ClipToBounds="True" Width="100" Height="100" Canvas.Right="100" Canvas.Top="1">
    <Viewport3D.Camera>
        <PerspectiveCamera Position="0,0,2" LookDirection="0,0,-1" FieldOfView="40" />
    </Viewport3D.Camera>
    <Viewport3D.Children>
        <ModelVisual3D>
            <ModelVisual3D.Content>
                <AmbientLight Color="Pink" />
            </ModelVisual3D.Content>
        </ModelVisual3D>
        <ModelVisual3D>
            <ModelVisual3D.Content>
                <GeometryModel3D>
```

