```
```java
// values stored for later use as vertex attributes
private ArrayList<Float> triangleVerts = new ArrayList<Float>();
private ArrayList<Float> textureCoords = new ArrayList<Float>();
private ArrayList<Float> normals = new ArrayList<Float>();

public void parseOBJ(String filename) throws IOException
{
    InputStream input = new FileInputStream(new File(filename));
    BufferedReader br = new BufferedReader(new InputStreamReader(input));
    String line;
    while ((line = br.readLine()) != null)
    {
        if(line.startsWith("v"))                                      // vertex position ("v" case)
        {
            for(String s : (line.substring(2)).split(" "))
            {
                vertVals.add(Float.valueOf(s));                        // extract the vertex position values
            }
        }
        else if(line.startsWith("vt"))                                // texture coordinates ("vt" case)
        {
            for(String s : (line.substring(3)).split(" "))
            {
                stVals.add(Float.valueOf(s));                          // extract the texture coordinate values
            }
        }
        else if(line.startsWith("vn"))                                // vertex normals ("vn" case)
        {
            for(String s : (line.substring(3)).split(" "))
            {
                normalVals.add(Float.valueOf(s));                      // extract the normal vector values
            }
        }
        else if(line.startsWith("f"))                                 // triangle faces ("f" case)
        {
            for(String s : (line.substring(2)).split(" "))
            {
                String v = s.split("/")[0];                           // extract triangle face references
                String vt = s.split("/")[1];
                String vn = s.split("/")[2];

                int vertRef = (Integer.valueOf(v)-1)*3;
                int tcRef = (Integer.valueOf(vt)-1)*2;
                int normRef = (Integer.valueOf(vn)-1)*3;

                triangleVerts.add(vertVals.get(vertRef));              // build array of vertices
                triangleVerts.add(vertVals.get(vertRef+1));
                triangleVerts.add(vertVals.get(vertRef+2));

                textureCoords.add(stVals.get(tcRef));                  // build array of
                textureCoords.add(stVals.get(tcRef+1));                // texture coordinates.

                normals.add(normVals.get(normRef));                    // ... and normals
                normals.add(normVals.get(normRef+1));
                normals.add(normVals.get(normRef+2));
            }
        }
    }
    input.close();
}
```
```