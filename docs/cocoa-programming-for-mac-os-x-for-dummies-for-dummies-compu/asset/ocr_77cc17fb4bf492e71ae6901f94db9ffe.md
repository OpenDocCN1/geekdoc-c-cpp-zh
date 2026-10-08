# Icon Composer

Icon Composer is a tool for constructing ICNS icon files. You can use it to gather, in one ICNS file, all the possible sizes for a particular icon. You can find Icon Composer here:

```
/Developer/Applications/Icon Composer
```

To create your own ICNS file, you need an image-editing application, such as Adobe Photoshop, Photoshop Elements, Pixelmator, GIMP, or Graphic Converter. Then follow these steps:

+   1. In your image-editing application, create a new RGB (red, green, blue) document with dimensions of 512 x 512 pixels.

This is the document you'll use to create an icon image.
2. With the various graphics tools in the application, create the image that you want to use as your icon.
3. If the image doesn't consume the entire 512 x 512 pixels, delete the unposed portions.
4. Save the result as a PNG transparency.

![](bbox=[0.133, 0.466, 0.198, 0.535])

Leave unused portions of the image blank because icons can be transparent. Also, deactivate any background layer to maintain transparency.

The PNG format supports transparency. Figure 5-12 shows a sample Photoshop image for use in an icon. Note the checkerboard pattern that appears in the background. It represents the transparent portion of the image. It will also be transparent when added to an icon in Icon Composer.

When you complete the design and creation of your icon artwork, you can use Icon Composer to build an icon file:

+   1. Launch Icon Composer by double-clicking its icon in Finder.
An empty icon template opens, as shown in Figure 5-13.
2. Drag the PNG image from Finder to the 512 x 512 square in Icon Composer.
Icon Composer displays a sheet asking if you want to use this PNG image for all the other image components in the icon, as shown in Figure 5-14.