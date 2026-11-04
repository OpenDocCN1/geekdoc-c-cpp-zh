+   - Display-only controls
+   - Basic input controls
+   - List-based controls

All the controls in this section are bindable to data (see Chapter 3 in this minibook) and modifiable through code.

# Display only controls

Four main controls focus on displaying information to the user:

+   - Image: The Image control displays images (of type .bmp, .gif, .ico, .jpg, .png, .wdp, and .tiff). To preserve the image's aspect ratio, set the Width or Height, but not both. Additionally, the DecodePixelWidth should be set to the same size as the Width. This will cause the rendering engine to scale the image appropriately, potentially saving a significant amount of memory.

Note, by the way, that you can put images almost anywhere in WPF — for example, how about an image on a button, in a label, or inline in a paragraph of text. And it's quite easy. I don't get so fancy here, but I want you to know about this possibility.

Listing 2-13 shows the XAML to load an image that shows a color wheel. Only the Width and DecodePixelWidth are set. The resulting window is shown in Figure 2-15.

# Listing 2-13: Image Control

```
```xml
<Image Grid.Row="0" Grid.Column="0" Width="256" >
    <Image.Source>
        <BitmapImage DecodePixelWidth="256" UriSource="/Images/1460_
PaintPalette_256x256.png"/>
    </Image.Source>
</Image>
```
```

![](bbox=[0.257, 0.739, 0.439, 0.872])

**Figure 2-15:**
Image control.