without knowing anything other than the signature to look for. The rest of the data is information you need to reconstruct the mesh data from the file.

After the header is the main data section of the file. In this case, there are three main things to store: the filenames for associated textures, the vertex buffer data, and the index buffer data.

With the file format decided on, you can then create the SaveBinary function, as shown in Listing 14.15. This function takes in a lot of parameters because there's a lot of information needed to create the binary file. In total, you need the filename, a pointer to the vertex buffer, the number of vertices, the layout of these vertices, a pointer to the index buffer, the number of indices, a vector of the texture names, the bounding box of the mesh, and the radius of the mesh. With all these parameters, you can save the file.

# Listing 14.15 Mesh::SaveBinary Implementation

Click here to view code image

```
void Mesh::SaveBinary(const std::string& fileName, co
uint32_t numVerts, VertexArray::Layout,
const uint32_t* indices, uint32_t numIndices,
const std::vector<std::string>& textureNames,
const AABB& box, float radius)
{
```