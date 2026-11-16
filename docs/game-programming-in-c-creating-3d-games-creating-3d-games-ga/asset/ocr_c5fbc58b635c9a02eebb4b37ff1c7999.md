Then, you modify the `VertexArray` constructor so that it takes in a `Layout` as a parameter. Then, in the code for the constructor you check the layout to determine how to define the vertex array attributes. For the case of `PosNormTex`, you use the previously written vertex attribute code. Otherwise, if the layout is `PosNormSkinTex`, you define the layout as in Listing 12.2.

# Listing 12.2 Declaring Vertex Attributes in the VertexArray Constructor

Click here to view code image

```
```cpp
if (layout == PosNormTex)
{
    /* From Chapter 6... */
}
else if (layout == PosNormSkinTex)
{
    // Position is 3 floats
    glEnableVertexAttribArray(0);
    glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, ve
    // Normal is 3 floats
    glEnableVertexAttribArray(1);
    glVertexAttribPointer(1, 3, GL_FLOAT, GL_FALSE, ve
    reinterpret_cast<void*>(sizeof(float) * 3));
}
```
```