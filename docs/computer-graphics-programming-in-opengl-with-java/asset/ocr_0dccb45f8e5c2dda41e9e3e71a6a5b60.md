+   - a vertex attribute for passing the texture coordinates down the pipeline
+   - a *texture unit* on the graphics card

A texture image can be a picture of anything. It can be a picture of something man-made or occurring in nature, such as cloth, grass, or a planetary surface, or it could be a geometric pattern, such as the checkerboard in Figure 5.1. In videogames and animated movies, texture images are commonly used to paint faces and clothing on characters or skin on creatures such as on the dolphin in Figure 5.1.

Images are typically stored in image files, such as .jpg, .png, .gif, or .tiff. In order to make a texture image available to shaders in the OpenGL pipeline, we need to extract the colors from the image and put them into an OpenGL *texture object* (a built-in OpenGL structure for holding a texture image).

Java has some useful image file tools in its imageio and awt packages that can be used to read texture images. The steps are as follows: (a) read the image data into a ByteBuffer, using the JOGL buffer tools we saw in Chapter 4, (b) use glGenTextures() to instantiate a texture object and assign it an integer ID, (c) call glBindTexture() to make the newly created texture object active, (d) load the previously read-in image data into the texture object with the glTexImage2D() command, and (e) adjust the texture settings using the glTexParameter() function. The result is an integer ID referencing the now available OpenGL texture object. We will walk through these steps at the end of this chapter.

However, JOGL includes its own tools for working with textures that make it considerably simpler to load a texture image file into an OpenGL texture object. Those tools are found in the JOGL classes Texture, TextureIO, and TextureData.

Texturing an object starts by declaring a variable of type Texture. This is a JOGL class; a JOGL Texture object serves as a wrapper for an OpenGL texture object. Next, we call newTexture()—a static method in the TextureIO class—to actually generate the texture object. The newTexture() function accepts an image file name as one of its parameters (several standard image file types are supported, including the four mentioned above). These steps are implemented in the following function:

```
```java
public static int loadTexture(String textureFileName)
{
    Texture tex = null;
    try { tex = TextureIO.newTexture(new File(textureFileName), false); }
    catch (Exception e) { e.printStackTrace(); }
    int textureID = tex.getTextureObject();
    return textureID;
}
```
```