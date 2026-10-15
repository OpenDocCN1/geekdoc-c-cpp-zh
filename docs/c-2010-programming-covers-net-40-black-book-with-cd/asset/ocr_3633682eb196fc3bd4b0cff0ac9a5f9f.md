# Chapter 12: Using Graphics and Multimedia in Windows Forms and WPF

```
```xml
<PerspectiveCamera x:Name="myPerspectiveCamera" Position="0,0,2"
    LookDirection="0,0,-1" FieldOfView="60" />
</Viewport3D.Camera>
<Viewport3D.Children>
    <ModelVisual3D>
        <ModelVisual3D.Content>
            <DirectionalLight Color="White" Direction="-0.612372,-0.5,-
                0.612372" />
        </ModelVisual3D.Content>
    </ModelVisual3D>
    <ModelVisual3D>
        <ModelVisual3D.Content>
            <DirectionalLight Color="White" Direction="0.612372,-0.5,-
                0.612372" />
        </ModelVisual3D.Content>
    </ModelVisual3D>
    <ModelVisual3D>
        <ModelVisual3D.Content>
            <GeometryModel3D>
                <GeometryModel3D.Geometry>
                    <MeshGeometry3D TriangleIndices="0,1,2 3,4,5
Normals="0,0,1 0,0,1 0,0,1 0,0,1 0,0,1 0,0,1" TextureCoordinates="0,1 1,1 1,0 0,0"
Positions="-0.5,-0.5,0.5 0.5,-0.5,0.5 0.5,0.5,0.5 0.5,0.5,0.5 -0.5,0.5,0.5 -0.5,-0.5,0.5" />
                </GeometryModel3D.Geometry>
                <GeometryModel3D.Material>
                    <MaterialGroup>
                        <DiffuseMaterial>
                            <DiffuseMaterial.Brush>
                                <RadialGradientBrush>
                                    <RadialGradientBrush.GradientStops>
                                        <GradientStop Color="Yellow" Offset="0" />
                                        <GradientStop Color="Red" Offset="0.25" />
                                        <GradientStop Color="Blue" Offset="0.75" />
                                        <GradientStop Color="LimeGreen"
                                            Offset="1" />
                                    </RadialGradientBrush.GradientStops>
                                </RadialGradientBrush>
                            </DiffuseMaterial.Brush>
                        </DiffuseMaterial>
                    </MaterialGroup>
                </GeometryModel3D.Material>
                <GeometryModel3D.Transform>
                    <RotateTransform3D>
                        <RotateTransform3D.Rotation>
                            <AxisAngleRotation3D Axis="0,2,1" Angle="45" />
                        </RotateTransform3D.Rotation>
                    </RotateTransform3D>
                </GeometryModel3D.Transform>
            </GeometryModel3D>
        </ModelVisual3D.Content>
    </ModelVisual3D>
</Viewport3D.Children>
</Viewport3D>
</Canvas>
</DockPanel>
</Window>
```
```

In Listing 12.21, the 3-D model is rotated by specifying the Axis and Angle properties of the RotateTransform3D class. When you run the application by pressing the F5 key on the keyboard, you get the output, as shown in Figure 12.25.