You can find an example of this in the FixedLayout project in the companion content. This app draws a 4x3 grid of circles on a canvas, as shown in Figure 8-4, to match the 1024x768 layout size. On a 1366x768 display or larger with a 16:9 aspect ratio, we get letterboxing on the sides; in the 320px narrow view (as set in the manifest), we get letterboxing on the top.

![](bbox=[0.15, 0.26, 0.75, 0.58])

FIGURE 8-4 Fixed layout scaling with a simple CSS transform, showing letterboxing on a full-screen 16:9 ratio display (left) and in a narrow 320px view (right).

# Sidebar: Raster Graphics and Fixed Layouts

If you use raster graphics within a fixed layout, size them according to the maximum 2560x1440 resolution so that they'll look good on the largest screens and they'll still scale down to smaller ones (rather than being stretched up). Alternately, you can load different graphics (through different img.src URLs) that are better suited for the most common screen size.

Note that resolution scaling (discussed later in this chapter) will still be applicable. If you're running on a high-density 10.6" 2560x1440 display (180% scale), the app and thus the fixed content will still see smaller screen dimensions. But if you're supplying a graphic for the native device resolution, it will look sharp when rendered on the screen.

In contrast to a fixed layout, where you always see the same content, an adaptive layout is one in which a view shows more stuff when more screen space is available. Such a layout is most easily achieved with a CSS grid where proportional rows and columns will automatically scale up and down; elements within grid cells will then find themselves resized accordingly. This is demonstrated in the Visual Studio/Blend project templates, especially the Grid App project. On a typical 1366x768 display you'll see a few items on a screen, as shown at the top of Figure 8-5. Switch over to a 27" 2560x1440 and you'll see a lot more, as you can see at the bottom of the figure.