FIG 3.15 You Can Tell Unity iOS How to Deal with NPOT Textures in the Texture Importer Dialog for Textures

![](bbox=[0.34, 0.09, 0.965, 0.735])

you'll be using the correct image formats for PVRTC Compression. A great tool to use for all GUI creation is “EZ GUI” from Above and Beyond Software. We'll discuss the usage of texture atlases in Chapter 4. However, it's vital to note that if you use NPOT texture sizes such as 480 x 320, you run into some heavy RAM usage, and the iPhone and iPad are not very fast in processing big RGBA textures. Also, larger textures take more time to load into RAM.

One benefit for NPOT textures in regards to interface elements (GUI) is they can be perfectly sized to the aspect ratio of the iPhone or iPad devices.