# Generated Textures

The chart and graph shown in Figures 23-11 and 23-12 are attractive, but it's hard to see what values represent without any kind of labels. These use gradient textures to give you a sense of which values are large and which, but they would be a lot easier to read if the values were labeled.

The LabeledBarChart example program shown in Figure 23-13 displays a bar chart with labels on the rows and columns and a label on each of each bar, making it much easier to understand the data.

The following code shows the MakeLabelBarChart routine to draw its labels:

![](bbox=[0.558, 0.098, 0.865, 0.355])

```
// a horizontal label at the specified position.
private void MakeLabel(Model3Group chart_model, double wid, double hgt, string txt,
    string font_name, double font_size, FontWeight font_weight, Brush font_brush,
    double y, double x1, double y1, double x2, double y2) {
    Label lbl = new Label();
    lbl.Width = wid;
    lbl.Height = hgt;
    lbl.Content = txt;
    lbl.HorizontalAlignment = HorizontalAlignment.Center;
    lbl.VerticalAlignment = VerticalAlignment.Center;
    lbl.Foreground = font_brush;
    lbl.Background = Brushes.Transparent;
    lbl.FontFamily = new FontFamily(font_name);
    lbl.FontSize = font_size;
    lbl.FontWeight = font_weight;
    DiffuseuseMaterial label_material = new DiffuseMaterial(label_brush);
    MeshGeometry3D label_mesh = null;
    MakeRectangle(chart_model, ref label_mesh, label_material,
        Point3D(x1, y1, z2), Point3D(x2, y1, z2),
        Point3D(x2, y2, z2), Point3D(x1, y2, z2),
        Point3D(x1, y1, z1), Point3D(1, 1, 0), Point3D(0, 0, 0), Point3D(0, 0, 1));
}
```

FIGURE 23-13

This code is fairly straightforward. It first creates a Label, setting its properties to display the necessary text using the specified font. It uses the Label to create a VisualBrush and then uses the brush to create a DiffuseMaterial. Finally, it creates a rectangle using the new material.