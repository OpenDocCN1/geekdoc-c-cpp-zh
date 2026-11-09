
```
    //The material is sort of blue-ish
    GLfloat theMaterial[] = { 0.25, 0.8, 1.0, 1.0 };
    glMaterialfv(GL_FRONT, GL_AMBIENT, theMaterial);
    glMaterialfv(GL_FRONT, GL_DIFFUSE, theMaterial);
    glMaterialfv(GL_FRONT, GL_SPECULAR, theMaterial);
    //Background color is black
    glClearColor (0.0, 0.0, 0.0, 1.0);
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
    //Set the projection view matrix
    glMatrixMode(GL_PROJECTION);
    glLoadIdentity();
    gluPerspective(fieldOfView, baseRect.size.width/baseRect.size.height,
        0.1, 10);
    //Set the model view matrix
    glMatrixMode(GL_MODELVIEW);
    glLoadIdentity();
    //'Eye' position - looking straight ahead
    gluLookAt(0.0, 0, zEye,
        0.0, 0, 0.0,
        0.0, 1, 0);
    //Position the light
    GLfloat lightPosition[] = { diffuseX, diffuseY, diffuseZ };
    glLightfv(GL_LIGHT0, GL_POSITION, lightPosition);
    /***Object drawing code***/
    //Center the drawing position
    glTranslatef(0.0, 0.0, 0.0);
    //Include some rotation
    glRotatef(rotationCount, 0, 1, 0);
    //Move one step to the right
    glTranslatef(1.0, 0.0, 0.0);
    //Draw the teapot
    glutSolidTeapot(1.0);
    //Render the scene
    glFinish();
    }
    - (void) reshape {
    //Resize the viewport to support the new view rect
    baseRect = [self convertRectToBase:[self bounds]];
    glViewport(0, 0, baseRect.size.width, baseRect.size.height);
    glMatrixMode(GL_PROJECTION);
    glLoadIdentity();
    gluPerspective(fieldOfView, baseRect.size.width/baseRect.size.height,
        0.1, 10);
    }
```

完成的场景如图 17.7 所示。

**图 17.8**

使用单独的控制面板控制场景参数——控制 OpenGL 场景的众多可能方式之一。

![](img/2b293e29fc15b0797f113b85dd429b6e_484_0.png)

作为练习，你可以尝试改进该项目。在此版本中，当用户移动滑块时，计时器动画会停止。可以将计时器和 drawRect: 方法移到子线程，使它们独立于 UI 运行。第 11 章提供了一些关于线程管理的提示。

你还可以通过添加额外光源、自定义纹理以及改进深度剔除（控制可见表面的绘制顺序）来创建更复杂的 OpenGL 视图。

> **提示**
> 
> 在 http://nehe.gamedev.net 上有一系列有用的非官方教程。这些项目的 Cocoa 版本现在已过时，但你可以从网站示例中提取代码，并将其复制到 OpenGL 项目示例代码中。官方文档可在 www.opengl.org 获取。

## 总结

在本章中，你学习了如何通过使用计时器方法更新属性值来创建简单的计时器驱动属性动画。你了解了动画器对象，并看到了它们如何用极少的代码添加简单的动画效果。

接下来，你发现了如何通过用自己创建和定义的动画对象替换默认动画对象来自定义动画器。作为自然的下一步，你学习了如何用图层对象替换动画器，并发现了如何创建可应用于 Core Image 滤镜的更复杂动画效果。

最后，你了解了 OpenGL，并学习了 OpenGL 场景动画的基础知识。你探索了 NSOpenGLView 视图类，并使用它创建了一个简单的动画场景，其可变参数由关联的控制面板设置。

## 18 调试、优化和管理代码

Xcode 包含一套强大的工具，用于性能分析、测试和调试代码。你可以通过三种方式测试应用程序：

- 将消息记录到控制台。
- 设置断点、单步执行代码并在调试窗口中检查属性值。
- 使用 *instruments*——一组测试工具，可以报告内存使用、线程状态、应用性能、对象分配和内存泄漏。

默认情况下，Xcode 为 OS X 和 iPhone OS 项目支持两种不同的构建配置选项：Release 和 Debug。你可以使用 Xcode 窗口左上角的构建下拉菜单选择这些选项，如图 18.1 所示。

Debug 选项会创建支持符号表。Release 构建不创建此表，因此生成的二进制文件小得多。

在 OS X 上，你可以将 Release 构建用作最终分发版本。在 iPhone 上，默认的 Release 设置不会创建用于 App Store 的构建；它们只是移除符号表。有关创建有效的 App Store 发布构建的信息，请参见第 19 章。

### 本章内容

- 使用控制台和 `NSLog`
- 使用断点和调试器窗口进行调试
- 使用 *instruments*
- 使用快照和源代码管理管理代码

**图 18.1**

在 Xcode 中选择 Debug 和 Release 构建。你可以使用默认的 Debug 构建设置进行基本调试。对于更高级的技术，你可能需要手动修改 Debug 配置。

![](img/2b293e29fc15b0797f113b85dd429b6e_487_0.png)

### 使用控制台和 NSLog

你将通过第 8 章的计数器应用程序学习调试：它易于修改，但又足够复杂，可以介绍性能分析和调试的理论与实践。将该应用程序重新载入 Xcode，并单击 CounterAppDelegate.m。你将使用此代码作为 Xcode 内置调试和性能报告工具的测试平台。

#### 开始使用 NSLog

你已经使用过 NSLog，但在本章中，你将结构化地使用它作为调试辅助工具。NSLog 将字符串写入应用程序的控制台。在大多数 Cocoa 应用程序中，控制台是隐藏的，但你可以在 Xcode 中测试应用程序时显示它，并且可以在代码中生成 NSLog 字符串来报告变量值和应用程序事件。

控制台是附加到 `stdout` 的终端，你也可以使用 `printf` 的多种变体及其相关格式选项向其写入内容。`NSLog` 经过优化以支持 Cocoa 对象。`printf` 更适合记录 C 语言字符串和值。你可以在应用程序中使用其中任意一种或同时使用两者。

要显示控制台窗口，请在 Xcode 中选择“运行 ➤ 控制台”。该窗口包含 Xcode 标准工具栏的子集，以及一个用于删除当前日志的“清除日志”按钮。单击“构建并运行”按钮以常规方式构建并运行应用程序，单击“重新启动”按钮以在崩溃后重新启动应用程序。你还可以单击“暂停”按钮临时暂停应用程序。这会显示命令行提示符，你可以使用它进行调试和日志记录的命令行控制。

控制台窗口和调试器窗口（本章后面会介绍）都是底层 `gdb`（GNU Project Debugger）调试环境的封装。如果你是 `gdb` 专家，可以在控制台窗口中使用 `gdb` 的命令行选项来访问 `gdb` 的高级功能。

`gdb` 是一个复杂而强大的工具，具有一些非常精密的功能。Xcode 的调试功能仅触及了它能做的事情的表面。但它是一个面向命令行的环境，并不是非常友好或易于访问。你可以在不直接访问它的情况下成功调试大多数应用程序。

对 `gdb` 功能的完整讨论超出了本书的范围。Apple 的 `gdb` 手册可在 http://developer.apple.com/mac/library/documentation/DeveloperTools/gdb/gdb/gdb_toc.html 获取。

#### 使用 NSLog 报告事件

事件日志记录是所有可能的调试选项中最简单的一种，但即使在复杂应用程序中，它也可以强大而有用。`NSLog` 简单易用。只需少量编辑，你就可以自动生成应用程序事件列表，并创建正在被触发的方法记录。使用它来测试方法是否在应该被触发时被触发。例如，你可以检查正确的方法是否由用户操作触发。通常，日志消息会添加到方法的顶部，但也可以嵌入条件代码中，以实现更有选择性的报告。

为了演示第一个选项，请在应用委托中编辑 `applicationDidFinishLaunching:` 方法，以包含一条 `NSLog` 语句：

```
- (void)applicationDidFinishLaunching:
    (NSNotification *)aNotification {
    NSLog(@"Application launched");
    TimerCount = 0;
}
```

构建并运行该应用程序。图 18.2 显示了结果。当 `applicationDidFinishLaunching:` 被触发时，代码会记录一条消息。在本章的示例应用程序中，已为所有方法添加日志记录，以便你可以监视它们何时被触发。日期/时间字符串和十六进制地址是自动生成的。
