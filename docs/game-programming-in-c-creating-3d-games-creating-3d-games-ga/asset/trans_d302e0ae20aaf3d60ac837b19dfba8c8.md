

将其附加到当前帧缓冲对象。这样，在为镜面渲染时，你仍然有一个深度缓冲，以确保更远的对象出现在更近的对象后面。

然后你创建镜面纹理，宽度和高度均为屏幕尺寸的四分之一。你不使用全屏尺寸，因为你希望镜面只占据屏幕的一部分。你为纹理请求GL_RGB格式，因为镜面将包含从镜面视角渲染的场景颜色输出。

接下来，glFramebufferTexture调用将镜面纹理与帧缓冲对象关联。注意你如何将GL_COLOR_ATTACHMENT0指定为第二个参数。这表示镜面纹理对应于片段着色器的第一个颜色输出。目前，你的片段着色器只写入一个输出，但如你在本章后面将看到的，从片段着色器写入多个输出是可能的。

然后，glDrawBuffers调用表示对于这个帧缓冲对象，你希望能够绘制到GL_COLOR_ATTACHMENT0插槽中的纹理（即镜面纹理）。最后，glCheckFramebufferStatus调用验证一切是否正常工作。如果出现问题，你删除帧缓冲对象和镜面纹理并返回false。

### 列表 13.2 创建镜面帧缓冲

单击此处查看代码图像

```cpp
bool Renderer::CreateMirrorTarget()
{
    int width = static_cast<int>(mScreenWidth) / 4;
    int height = static_cast<int>(mScreenHeight) / 4;

    // Generate a framebuffer for the mirror texture
    glGenFramebuffers(1, &mMirrorBuffer);
    glBindFramebuffer(GL_FRAMEBUFFER, mMirrorBuffer);

    // Create the texture we'll use for rendering
    mMirrorTexture = new Texture();
    mMirrorTexture->CreateForRendering(width, height);

    // Add a depth buffer to this target
    GLuint depthBuffer;
    glGenRenderbuffers(1, &depthBuffer);
    glBindRenderbuffer(GL_RENDERBUFFER, depthBuffer);
    glRenderbufferStorage(GL_RENDERBUFFER, GL_DEPTH_COMPONENT, width, height);
    glFramebufferRenderbuffer(GL_FRAMEBUFFER, GL_DEPTH_ATTACHMENT, GL_RENDERBUFFER, depthBuffer);

    // Attach mirror texture as the output target for
    glFramebufferTexture(GL_FRAMEBUFFER, GL_COLOR_ATTACHMENT0,
        mMirrorTexture->GetTextureID(), 0);

    // Set the list of buffers to draw to for this frame
    GLenum drawBuffers[] = { GL_COLOR_ATTACHMENT0 };
    glDrawBuffers(1, drawBuffers);

    // Make sure everything worked
    if (glCheckFramebufferStatus(GL_FRAMEBUFFER) != GL_FRAMEBUFFER_COMPLETE)
    {
        // If it didn't work, delete the framebuffer,
        // unload/delete the texture and return false
        glDeleteFramebuffers(1, &mMirrorBuffer);
        mMirrorTexture->Unload();
        delete mMirrorTexture;
        mMirrorTexture = nullptr;
        return false;
    }

    return true;
}
```

在`Renderer::Initialize`中，你添加对`CreateMirrorTarget`的调用并验证函数返回`true`。同样，在`Renderer::Shutdown`中，你删除镜面帧缓冲和镜面纹理（使用与`glCheckFramebufferStatus`调用表示帧缓冲不完整时运行的相同代码）。

## 将内容渲染到帧缓冲对象

为了支持镜面，你需要渲染两次3D场景：一次从镜面的视角，一次从普通摄像机的视角。每次渲染场景都是一个渲染**通道**。为了辅助多次绘制3D场景，你可以创建一个`Draw3DScene`函数，其骨架在列表 13.3中。

`Draw3DScene`函数接收帧缓冲ID、视图矩阵、投影矩阵和视口缩放比例。视口尺寸让OpenGL知道它正在写入的帧缓冲目标的实际大小。因此，你在这里需要一个视口缩放参数，以便普通帧缓冲可以使用全屏宽度和高度，而镜面可以使用其四分之一的尺寸。你使用`glViewport`调用根据屏幕宽度/高度和缩放比例将视口设置为正确的大小。

绘制网格的代码与第6章“3D图形”中的相同，绘制骨骼网格的代码与第12章“骨骼动画”中的相同。除了视口代码外，唯一的其他区别是，在绘制任何内容之前，glBindFramebuffer调用将活动帧缓冲设置为请求的那个。

### 列表 13.3 Renderer::Draw3DScene 辅助函数

单击此处查看代码图像

```cpp
void Renderer::Draw3DScene(unsigned int framebuffer,
const Matrix4& view, const Matrix4& proj,
float viewportScale)
{
    // Set the current framebuffer
    glBindFramebuffer(GL_FRAMEBUFFER, framebuffer);

    // Set viewport size based on scale
    glViewport(0, 0,
    static_cast<int>(mScreenWidth * viewportScale),
    static_cast<int>(mScreenHeight * viewportScale)
    );

    // Clear color buffer/depth buffer
    glClearColor(0.0f, 0.0f, 0.0f, 1.0f);
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);

    // Draw mesh components
    // ((Same code as Chapter 6))
    // ...

    // Draw any skinned meshes now
    // ((Same code as Chapter 12))
    // ...
}
```

然后你修改`Renderer::Draw`中的代码以调用两次`Draw3DScene`，如**列表 13.4**所示。首先，你使用镜面的视图并渲染到镜面帧缓冲进行绘制，然后你使用普通摄像机的视图并渲染到默认帧缓冲进行绘制。最后，你使用第6章和第12章中的代码绘制精灵和UI屏幕。

### 列表 13.4 `Renderer::Draw` 已更新以同时渲染镜面和默认通道

单击此处查看代码图像

```cpp
void Renderer::Draw()
{
    // Draw to the mirror texture first (viewport scale)
    Draw3DScene(mMirrorBuffer, mMirrorView, mProjection);
    // Now draw the normal 3D scene to the default framebuffer
    Draw3DScene(0, mView, mProjection);
    // Draw all sprite components
    // (Same code as Chapter 6)
    // ...
    // Draw any UI screens
    // (Same code as Chapter 12)
    // ...
    // Swap the buffers
    SDL_GL_SwapWindow(mWindow);
}
```

这里，mMirrorView是镜面的单独视图矩阵。镜面视图的具体内容并无新意。你可以创建一个`MirrorCamera`类，它使用基本跟随摄像机，如第9章“摄像机”中所示。然而，镜面摄像机位于角色前方，面向角色后方。这个`MirrorCamera`随后附加到玩家角色并更新mMirrorView。

## 在HUD中绘制镜面纹理

既然绘制代码正在向镜面纹理写入，你可以像使用任何其他纹理一样使用它并将其绘制到屏幕上。由于在这种情况下镜面只是一个HUD元素，你可以利用`UIScreen`中现有的`DrawTexture`功能。

然而，使用现有代码绘制会导致镜面的y值与预期相反。这是因为，在内部，OpenGL将UV原点放置在图像的左下角，而不是左上角（这更为典型）。幸运的是，这很容易修复：在绘制纹理时，你已经创建了一个缩放矩阵。如果你对该缩放矩阵的y轴取反，它将在y方向上翻转纹理。为了支持这一点，你将一个新的`flipY`布尔值作为可选参数添加到`UIScreen::DrawTexture`中，如列表 13.5所示。你将`flipY`默认设置为`false`，因为现有的UI纹理不需要翻转其y轴。

### 列表 13.5 向`UIScreen::DrawTexture`添加`flipY`选项

单击此处查看代码图像

```cpp
void UIScreen::DrawTexture(class Shader* shader, class Texture* texture,
const Vector2& offset, float scale, bool flipY)
{
    // Scale the quad by the width/height of texture
    // and flip the y if we need to
    float yScale = static_cast<float>(texture->GetHeight());
    if (flipY) { yScale *= -1.0f; }

    Matrix4 scaleMat = Matrix4::CreateScale(
    static_cast<float>(texture->GetWidth()) * scale,
    yScale,
    1.0f);

    // Translate to position on screen
    Matrix4 transMat = Matrix4::CreateTranslation(
    Vector3(offset.x, offset.y, 0.0f));

    // Set world transform
    Matrix4 world = scaleMat * transMat;
}
```

