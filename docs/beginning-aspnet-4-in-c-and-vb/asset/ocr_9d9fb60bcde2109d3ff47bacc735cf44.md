to define the light to show the model. SpecularMaterial adds illuminated highlight reflections when specular highlight reflections occur. The example code makes use of DiffuseMaterial and references a brush from the resource named mainCover:

```
<GeometryModel3D.Material>
    <DiffuseMaterial Brush="{StaticResource mainCover}" />
</GeometryModel3D.Material>
</GeometryModel3D>
```

The brush for the main cover is a VisualBrush. The VisualBrush has a Border with a Grid that consists of two Label elements. One Label element defines the text Professional C# 4 and is written to the cover:

```
<VisualBrush x:Key="mainCover">
    <VisualBrush.Visual>
        <Border Background="Red">
            <Grid>
                <Grid.RowDefinitions>
                    <RowDefinition Height="30" />
                    <RowDefinition Height="*" />
                </Grid.RowDefinitions>
                <Label Grid.Row="0" HorizontalAlignment="Center">
                    Professional C# 4</Label>
                <Label Grid.Row="1"></Label>
            </Grid>
        </Border>
    </VisualBrush.Visual>
</VisualBrush>
```

Because a brush is defined by a 2-D coordinate system and the model has a 3-D coordinate system, a translation between them needs to be done. This translation is done by the TextureCoordinates property of the MeshGeometry3D. The TextureCoordinates specify every point of the triangle and shows how it maps to 2-D. The first point 0 0 0 maps to 0 1, the second point 10 0 0 maps to 1 1, and so on. Be aware that y has a different direction in the 3-D and 2-D coordinate systems. Figure 35-36 shows the coordinate system for 2-D:

```
<MeshGeometry3D
Positions="0 0 0, 10 0 0, 0 10 0, 10 10 0, 10 0 0"
TriangleIndices="0, 1, 2, 2, 4, 3"
TextureCoordinates="0 1, 1 1, 0 0, 1 0, 1 1"
/>
```

![](bbox=[0.15, 0.8, 0.45, 0.97])

FIGURE 35-36