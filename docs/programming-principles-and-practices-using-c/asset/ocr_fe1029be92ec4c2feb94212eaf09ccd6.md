We can select part of that image and add a photo of Rita as seen from space (rita.jpg):

```
Image rita {Point(0,0),"rita.jpg"};
Image path {Point(0,0),"rita_path.gif"};
path.set_mask(Point(50,250),600,400);  // select likely landfall
win.attach(path);
win.attach(rita);
```

![](bbox=[0.17, 0.3, 0.72, 0.65])

The set_mask() operation selects a sub-picture of an image to be displayed. Here, we selected a (600,400)-pixel image from rita_path.gif (loaded as path) with its top leftmost point at path’s point (50,250). Selecting only part of an image for display is so common that we chose to support it directly.

Shapes are laid down in the order they are attached, like pieces of paper on a desk, so we got path “on the bottom” simply by attaching it before rita.

Images can be encoded in a bewildering variety of formats. Here we deal with only two of the most common, JPEG and GIF:

```
enum class Suffix { none, jpg, gif };
```