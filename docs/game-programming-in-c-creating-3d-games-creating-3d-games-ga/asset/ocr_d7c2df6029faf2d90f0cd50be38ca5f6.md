We explore the idea of improving the quality of textures further in Chapter 13, “Intermediate Graphics.” For now, let’s enable bilinear filtering for all textures.

To use texture mapping in OpenGL, there are three things you need to do:

+   - Load image files (textures) and create OpenGL texture objects.
+   - Update the vertex format to include texture coordinates.
+   - Update the shaders to use the textures.

# Loading the Texture

Although you can use the SDL Image library to load images for OpenGL, the Simple OpenGL Image Library (SOIL) is a little easier to use. SOIL can read in several file formats, including PNG, BMP, JPG, TGA, and DDS. As it’s designed to work with OpenGL, it slots in easily with the other OpenGL code needed for creating a texture object.

Listing 5.14 gives the declaration of a Texture class that encapsulates loading in a texture file and using it with OpenGL. The names of the functions and member variables are mostly self-explanatory; for example, Load loads the texture from the file. For member variables, you have a width and height of the texture and an OpenGL texture ID.

# Listing 5.14 Texture Declaration

Click here to view code image