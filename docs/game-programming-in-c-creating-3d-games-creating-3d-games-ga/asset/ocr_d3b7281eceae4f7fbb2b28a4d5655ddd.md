```
public:
VertexArray(const float* verts, unsigned int numVe
const unsigned int* indices, unsigned int numIr
~VertexArray();

// Activate this vertex array (so we can draw it)
void SetActive();

unsigned int GetNumIndices() const { return mNumIr
unsigned int GetNumVerts() const { return mNumVert

private:

// How many vertices in the vertex buffer?

unsigned int mNumVerts;

// How many indices in the index buffer

unsigned int mNumIndices;

// OpenGL ID of the vertex buffer

unsigned int mVertexBuffer;

// OpenGL ID of the index buffer

unsigned int mIndexBuffer;

// OpenGL ID of the vertex array object
```