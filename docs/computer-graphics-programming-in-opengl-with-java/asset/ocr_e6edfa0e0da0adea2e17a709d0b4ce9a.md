```
gl.glTexImage2D(GL_TEXTURE_2D, 0, GL_DEPTH_COMPONENT24, myCanvas.getWidth(),
    myCanvas.getHeight(), 0, GL_DEPTH_COMPONENT, GL_FLOAT, null);
gl.glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR);
gl.glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_LINEAR);
gl.glFramebufferTexture2D(GL_FRAMEBUFFER, GL_DEPTH_ATTACHMENT, GL_TEXTURE_2D,
    bufferId[0], 0);
// initialize refraction framebuffer
gl.glGenFramebuffers(1, bufferId, 0);
refractFrameBuffer = bufferId[0];
gl.glBindFramebuffer(GL_FRAMEBUFFER, refractFrameBuffer);
(the remainder of this section is identical to the code above for the reflection buffer, but with
    “refractTextureID”)

. . .
}

private void prepForSkyBoxRender() {
    GL4 gl = (GL4) GLContext.getCurrentGL();
    gl.glUseProgram(renderingProgramCubeMap);

    vLoc = gl.glGetUniformLocation(renderingProgramCubeMap, "v_matrix");
    pLoc = gl.glGetUniformLocation(renderingProgramCubeMap, "p_matrix");

    gl.glUniformMatrix4fv(vLoc, 1, false, vMat.get(vals));
    gl.glUniformMatrix4fv(pLoc, 1, false, pMat.get(vals));

    // vbo[0] holds the skybox vertices
    gl.glBindBuffer(GL_ARRAY_BUFFER, vbo[0]);
    gl.glVertexAttribPointer(0, 3, GL_FLOAT, false, 0, 0);
    gl.glEnableVertexAttribArray(0);

    gl.glActiveTexture(GL_TEXTURE0);
    gl.glBindTexture(GL_TEXTURE_CUBE_MAP, skyboxTexture);
}

private void prepForTopSurfaceRender() {
    GL4 gl = (GL4) GLContext.getCurrentGL();
    gl.glUseProgram(renderingProgramSURFACE);

    mLoc = gl.glGetUniformLocation(renderingProgramSURFACE, "m_matrix");
    vLoc = gl.glGetUniformLocation(renderingProgramSURFACE, "v_matrix");
    pLoc = gl.glGetUniformLocation(renderingProgramSURFACE, "p_matrix");
    nLoc = gl.glGetUniformLocation(renderingProgramSURFACE, "norm_matrix");

    mMat.translation(0.0f, surfacePlaneHeight, 0.0f);

    mMat.invert(invTrMat);
    invTrMat.transpose(invTrMat);
```