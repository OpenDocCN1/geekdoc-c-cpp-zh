```
```java
// fill a byte array with RGB blue/yellow values corresponding to the pattern built by generate3Dpattern()
private void fillDataArray(byte data[])
{
    for (int i=0; i<texWidth; i++)
    {
        for (int j=0; j<texHeight; j++)
        {
            for (int k=0; k<texDepth; k++)
            {
                if (tex3Dpattern[i][j][k] == 1.0)
                { // yellow color
                    data[i*(texWidth*texHeight*4) + j*(texHeight*4)+ k*4+0] = (byte) 255;       // red
                    data[i*(texWidth*texHeight*4) + j*(texHeight*4)+ k*4+1] = (byte) 255;       // green
                    data[i*(texWidth*texHeight*4) + j*(texHeight*4)+ k*4+2] = (byte) 0;         // blue
                    data[i*(texWidth*texHeight*4) + j*(texHeight*4)+ k*4+3] = (byte) 255;       // alpha
                }
                else
                { // blue color
                    data[i*(texWidth*texHeight*4) + j*(texHeight*4)+ k*4+0] = (byte) 0;         // red
                    data[i*(texWidth*texHeight*4) + j*(texHeight*4)+ k*4+1] = (byte) 0;         // green
                    data[i*(texWidth*texHeight*4) + j*(texHeight*4)+ k*4+2] = (byte) 255;       // blue
                    data[i*(texWidth*texHeight*4) + j*(texHeight*4)+ k*4+3] = (byte) 255;       // alpha
                }
            } } } }
}

// build 3D pattern of stripes
void generate3Dpattern()
{
    for (int x=0; x<texWidth; x++)
    {
        for (int y=0; y<texHeight; y++)
        {
            for (int z=0; z<texDepth; z++)
            {
                if ((y/10)%2 == 0)
                    tex3Dpattern[x][y][z] = 0.0;
                else
                    tex3Dpattern[x][y][z] = 1.0;
            } } }
}

// load the sequential byte data array into a texture object
private int load3DTexture()
{
    GL4 gl = (GL4) GLContext.getCurrentGL();

    byte[] data = new byte[texWidth * texHeight * texDepth * 4];
    fillDataArray(data);
    ByteBuffer bb = Buffers.newDirectByteBuffer(data);

    int[] textureIDs = new int[1];
    gl.glGenTextures(1, textureIDs, 0);
    int textureID = textureIDs[0];

    gl.glBindTexture(GL_TEXTURE_3D, textureID);
    gl.glTexStorage3D(GL_TEXTURE_3D, 1, GL_RGBA8, texWidth, texHeight, texDepth);
    gl.glTexSubimage3D(GL_TEXTURE_3D, 0, 0, 0, 0, texWidth, texHeight, texDepth, GL_RGBA, GL_UNSIGNED_BYTE, bb);
}
```
```