

```cpp
// draw water top (surface)
glUseProgram(renderingProgramSURFACE);
mMat.translation(0.0f, surfacePlaneHeight, 0.0f); // positions the top plane at the specified height

glBindBuffer(GL_ARRAY_BUFFER, vbo[3]); // also send normals for lighting
glVertexAttribPointer(2, 3, GL_FLOAT, GL_FALSE, 0, 0);
glEnableVertexAttribArray(2);
. . .
// render the top surface twice, so that it can be viewed from both above and below the surface
if (cameraHeight >= surfacePlaneHeight)
    glFrontFace(GL_CCW);
else
    glFrontFace(GL_CW);
glDrawArrays(GL_TRIANGLES, 0, 6);

// draw water bottom (floor)
glUseProgram(renderingProgramFLOOR);
mMat.translation(0.0f, floorPlaneHeight, 0.0f); // positions the bottom plane at the specified height
. . .
glBindBuffer(GL_ARRAY_BUFFER, vbo[3]); // also send normals for lighting
glVertexAttribPointer(2, 3, GL_FLOAT, GL_FALSE, 0, 0);
glEnableVertexAttribArray(2);
. . .
glFrontFace(GL_CCW); // since the previous setting might have been CW, we set it to CCW here
glDrawArrays(GL_TRIANGLES, 0, 6);
}
. . . // main() and other components as before
```

我们现在扩展了之前的程序，使其包含两个平面段：一个用于顶部表面，一个用于底部表面。我们加入了法线，以便在两个表面上都能使用 ADS 光照。我们有两个渲染程序，因为在这个版本中，顶部表面不使用纹理渲染，而底部表面使用棋盘格纹理渲染。此外，顶部表面的绕序设置取决于摄像机位于水面上方还是下方（因为需要渲染该平面的某一侧）。图 15.2 显示了摄像机位于水面上方和下方时的结果。两种情况都明显可见镜面高光。在水下情况下，远处浅色带是透过顶部表面平面可见的天空盒。这个问题将在我们添加“雾”效果后得到解决。

![](img/1695de1bc7486362f86c143285f3fb40_378_0.png)

**图 15.2** 水顶部表面和底部地板的几何结构：摄像机位于水面之上（左）和位于水面之下（右）

## 15.2 添加表面反射和折射

水是复杂的，要制作完全逼真的模拟，需要加入水体中通常可见的众多反射和折射。更复杂的是，根据摄像机位于水面上方还是下方，需要不同的效果。

我们将首先聚焦第一种情况：摄像机位于水面上方。在图 15.2（左图）中，我们可以看到目前有 (1) 一个实心蓝色表面，(2) 水面上方的天空盒，以及 (3) 表面上的光照。为了开始让这个看起来更像水，程序 15.3 添加了以下两项：

- *反射*，使得水面之上的物体（如天空盒）能反射到水面上
- *折射*，使视线从顶部表面穿透到底部地板，从而当从水面之上向下看时，能看到水面下的物体（如棋盘格地板）

我们将通过从不同观察点将场景渲染到多个帧缓冲来实现这些效果，然后使用生成的帧缓冲作为纹理，应用到带有 ADS 光照的蓝色水表面。这相当复杂，因此我们将程序 15.3 分为三部分介绍。在第一部分中，我们首先将 `display()` 中的代码重组为多个独立函数：(1) 一个用于准备渲染天空盒的函数，(2) 一个用于准备渲染顶部表面的函数，(3) 一个用于准备渲染地板的函数。然后我们像之前一样渲染每一个。稍后，在第二部分中，我们将这些项目渲染到称为*反射*和*折射*纹理的纹理中，并将它们都应用到顶部表面——但目前我们只是重组代码，以便为这一后续步骤提供便利。

（当摄像机位于水面以下时，这些相同的函数也会很有用。但就目前而言，我们将只专注于摄像机位于水面上方的情况。）

display() 函数的划分，以及反射和折射帧缓冲的创建（但尚未填充），如程序 15.3 所示。请注意，这两个帧缓冲还包括深度附件（我们在第 8 章学习阴影映射时已经见过），这些附件在后续会很有用。

### 程序 15.3——反射和折射（第 1 部分：准备）

C++/OpenGL 应用程序

```cpp
void createReflectRefractBuffers(GLFWwindow* window) { // called once from init()
    GLuint bufferId[1];
    glGenBuffers(1, bufferId);
    glfwGetFramebufferSize(window, &width, &height);

    // initialize refraction framebuffer
    glGenFramebuffers(1, bufferId);
    refractFrameBuffer = bufferId[0];
    glBindFramebuffer(GL_FRAMEBUFFER, refractFrameBuffer);
    glGenTextures(1, bufferId);        // this is for the color buffer
    refractTextureId = bufferId[0];
    glBindTexture(GL_TEXTURE_2D, refractTextureId);
    glTexImage2D(GL_TEXTURE_2D, 0, GL_RGBA, width, height, 0, GL_RGBA, GL_UNSIGNED_BYTE, NULL);
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR);
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_LINEAR);
    glFramebufferTexture2D(GL_FRAMEBUFFER, GL_COLOR_ATTACHMENT0, GL_TEXTURE_2D, refractTextureId, 0);
    glDrawBuffer(GL_COLOR_ATTACHMENT0);
    glGenTextures(1, bufferId);        // this is for the depth buffer
    glBindTexture(GL_TEXTURE_2D, bufferId[0]);
    glTexImage2D(GL_TEXTURE_2D, 0, GL_DEPTH_COMPONENT24, width, height, 0, GL_DEPTH_COMPONENT, GL_FLOAT, NULL);
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR);
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_LINEAR);
    glFramebufferTexture2D(GL_FRAMEBUFFER, GL_DEPTH_ATTACHMENT, GL_TEXTURE_2D, bufferId[0], 0);

    // initialize reflection framebuffer
    glGenFramebuffers(1, bufferId);
    reflectFrameBuffer = bufferId[0];
    glBindFramebuffer(GL_FRAMEBUFFER, reflectFrameBuffer);
    // (the remainder of this section is identical to the code above for the refraction buffer, but with "reflectTextureID")
...
}

void prepForSkyBoxRender() {
    glUseProgram(renderingProgramCubeMap);

    vLoc = glGetUniformLocation(renderingProgramCubeMap, "v_matrix");
    projLoc = glGetUniformLocation(renderingProgramCubeMap, "p_matrix");

    glUniformMatrix4fv(vLoc, 1, GL_FALSE, glm::value_ptr(vMat));
    glUniformMatrix4fv(projLoc, 1, GL_FALSE, glm::value_ptr(pMat));

    // vbo[0] holds the skybox vertices
    glBindBuffer(GL_ARRAY_BUFFER, vbo[0]);
    glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 0, 0);
    glEnableVertexAttribArray(0);

    glActiveTexture(GL_TEXTURE0);
    glBindTexture(GL_TEXTURE_CUBE_MAP, skyboxTexture);
}

void prepForTopSurfaceRender() {
    glUseProgram(renderingProgramSURFACE);

    mvLoc = glGetUniformLocation(renderingProgramSURFACE, "mv_matrix");
    projLoc = glGetUniformLocation(renderingProgramSURFACE, "proj_matrix");
    nLoc = glGetUniformLocation(renderingProgramSURFACE, "norm_matrix");

    mMat = glm::translate(glm::mat4(1.0f), glm::vec3(0.0f, surfacePlaneHeight, 0.0f));
    mvMat = vMat * mMat;
    invTrMat = glm::transpose(glm::inverse(mvMat));

    currentLightPos = glm::vec3(lightLoc.x, lightLoc.y, lightLoc.z);
    installLights(vMat, renderingProgramSURFACE);

    // get references to uniform variables
    glUniformMatrix4fv(mvLoc, 1, GL_FALSE, glm::value_ptr(mvMat));
    glUniformMatrix4fv(projLoc, 1, GL_FALSE, glm::value_ptr(pMat));
    glUniformMatrix4fv(nLoc, 1, GL_FALSE, glm::value_ptr(invTrMat));
}
```

```cpp
glFrontFace(GL_CCW);
else
    glFrontFace(GL_CW);
glDrawArrays(GL_TRIANGLES, 0, 6);
// draw water bottom (floor) – most of the code moved to "prepForFloorRender()" function
prepForFloorRender();
glEnable(GL_DEPTH_TEST);
glDepthFunc(GL_LEQUAL);
glFrontFace(GL_CCW);
glDrawArrays(GL_TRIANGLES, 0, 6);
}
```

如前所述，程序 15.3 的代码分为三部分，从上面列出的第一部分开始。到目前为止，程序 15.3 实际上并没有产生任何与程序 15.2 不同的渲染输出。但是，它以一种对我们后续工作有用的方式重组了代码，因为我们 (1) 创建了两个自定义帧缓冲来保存反射和折射信息，(2) 隔离了 display() 中为渲染场景特定部分（天空盒、地板和表面）做准备的部分，从而便于多次渲染。

现在，在程序 15.3 的第二部分中，我们构建反射和折射纹理。我们通过重复 display() 中的一些操作，但使用不同的视图矩阵来实现这一点。该策略如图 15.3 所示。摄像机位于水面上方，略向下看。在摄像机正下方、水面之下，有第二个摄像机略向上看，称为“反射摄像机”。它用于渲染水面之上的物体（如天空盒）以构建反射纹理。它的位置深度等于摄像机在水面以上的高度，即 surfacePlaneHeight - cameraHeight。我们的摄像机旋转实现仅包含俯仰（绕 X 轴旋转），因此对于反射摄像机，我们只需将俯仰值取反。

由于反射摄像机的目的是生成包含从水面反射的物体的纹理，因此当从反射摄像机的视角渲染时，我们只渲染水面之上的物体。因此，在本例中，我们会渲染天空盒，但不会渲染地板、顶部表面或水中的任何物体（例如鱼）。

折射纹理由第三个摄像机生成，称为“折射摄像机”。它使用与主摄像机相同的视图矩阵。折射应渲染透过水看到的一切。也就是说，当主摄像机在

