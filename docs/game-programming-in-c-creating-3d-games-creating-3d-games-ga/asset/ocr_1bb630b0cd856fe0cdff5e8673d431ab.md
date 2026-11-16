are three float values.

Next, you define the skinning bones and weight attributes. For the bones, you use glVertexAttribIPointer, which is for values that are integers in the shader. Because the definition of inSkinBones uses four unsigned integers, you must use the AttribI function instead of the regular Attrib version. Here, you specify that each integer is an unsigned byte (from 0 to 255). For the weights, you specify that each is stored in memory as an unsigned byte, but you want to convert these unsigned bytes to a normalized float value from 0.0 to 1.0.

Finally, the declaration of the texture coordinates is the same as in Chapter 6, except that they have a different offset because they appear later in the vertex layout.

Once you have defined the vertex attributes, the next step is to update the Mesh file loading code to load in a gpmesh file with skinning vertex attributes. (This chapter omits the code for file loading in the interest of brevity. But as always, the source code is available in this chapter's corresponding game project.)

Next, you declare a SkeletalMeshComponent class that inherits from MeshComponent, as in Listing 12.3. For now, the class does not override any behavior from the base MeshComponent. So, the Draw function for now simply calls MeshComponent::Draw. This will change when you begin playing animations.