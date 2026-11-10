```
```java
    gl.glClear(GL_DEPTH_BUFFER_BIT);
    gl.glEnable(GL_CULL_FACE);
    gl.glFrontFace(GL_CCW);
    gl.glEnable(GL_DEPTH_TEST);
    gl.glDepthFunc(GL_LEQUAL);

    gl.glBindBuffer(GL_ELEMENT_ARRAY_BUFFER, vbo[4]);    // vbo[4] contains torus indices
    gl.glDrawElements(GL_TRIANGLES, numTorusIndices, GL_UNSIGNED_INT, 0);

    // repeat for the pyramid (but don't clear the GL_DEPTH_BUFFER_BIT).
    // The pyramid is not indexed, so we use glDrawArrays() rather than glDrawElements()
    ...
    gl.glDrawArrays(GL_TRIANGLES, 0, numPyramidVertices);
}

public void passTwo()
{
    GL4 gl = (GL4) GLContext.getCurrentGL();

    // renderingProgram2 includes the pass two vertex and fragment shaders
    gl.glUseProgram(renderingProgram2);

    // draw the torus - this time we need to include lighting, materials, normals, etc.
    // We also need to provide MVP transforms for BOTH camera space and light space.
    mLoc = gl.glGetUniformLocation(renderingProgram2, "m_matrix");
    vLoc = gl.glGetUniformLocation(renderingProgram2, "v_matrix");
    pLoc = gl.glGetUniformLocation(renderingProgram2, "p_matrix");
    nLoc = gl.glGetUniformLocation(renderingProgram2, "norm_matrix");
    sLoc = gl.glGetUniformLocation(renderingProgram2, "shadowMVP");
    curAmb = bronzeMatAmb;        // the torus is bronze
    curDif = bronzeMatDif;
    curSpe = bronzeMatSpe;
    curShi = bronzeMatShi;

    vMat.identity().setTranslation(-cameraLoc.x(), -cameraLoc.y(), -cameraLoc.z());
    currentLightPos.set(lightLoc);
    installLights(renderingProgram2);

    mMat.identity();
    mMat.translate(torusLoc.x(), torusLoc.y(), torusLoc.z());
    mMat.rotateX((float)Math.toRadians(25.0f));        // slight rotation for visibility

    mMat.invert(invTrMat);
    invTrMat.transpose(invTrMat);

    // build the MVP matrix for the torus from the light's point of view
    shadowMVP2.identity();
```
```