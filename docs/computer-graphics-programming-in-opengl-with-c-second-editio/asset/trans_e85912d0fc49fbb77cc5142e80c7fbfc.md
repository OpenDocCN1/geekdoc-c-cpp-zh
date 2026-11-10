
|  |  |
| --- | --- |
| **设置** | • 实例化矩阵栈。 |
| **相机** | • 将一个新矩阵压入栈中（这会实例化一个空的 VIEW 矩阵）。<br><br>• 对栈顶的视图矩阵应用变换。 |
| **父对象** | • 将一个新矩阵压入栈中（这将是父 MV 矩阵——对于第一个父对象，它会复制视图矩阵）。<br><br>• 应用变换，将父对象的 M 矩阵并入复制得到的视图矩阵中。<br><br>• 将最顶部的矩阵（即使用 `glm::value_ptr()`）发送到顶点着色器中的 MV uniform 变量。<br><br>• 绘制父对象。 |
| **子对象** | • 将一个新矩阵压入栈中。这将是子对象的 MV 矩阵，复制父 MV 矩阵。<br><br>• 应用变换，将子对象的 M 矩阵并入复制得到的父 MV 矩阵中。<br><br>• 将最顶部的矩阵（即使用 `glm::value_ptr()`）发送到顶点着色器中的 MV uniform 变量。<br><br>• 绘制子对象。 |
| **清理** | • 从栈中弹出子对象的 MV 矩阵。<br><br>• 从栈中弹出父对象的 MV 矩阵。<br><br>• 从栈中弹出 VIEW 矩阵。 |

请注意，金字塔（“太阳”）绕其轴线的旋转是在其自身的局部坐标空间中进行的，不应允许它影响“子对象”（本例中为行星和月球）。因此，太阳的旋转（如下图所示）会被压入栈中，但在绘制太阳之后，必须将其从栈中移除（弹出）。

![](img/1695de1bc7486362f86c143285f3fb40_109_0.png)

大立方体（行星）绕太阳的公转（下图左图）会影响月球的运动，因此它被压入栈中，并且在绘制月球时也保留在栈中。相比之下，行星绕其轴线的自转（下图右图）是局部变换，不会影响月球，因此在绘制月球之前会将其从栈中弹出。

![](img/1695de1bc7486362f86c143285f3fb40_109_1.png)

![](img/1695de1bc7486362f86c143285f3fb40_109_2.png)

同样，我们会为月球的旋转（绕行星旋转以及绕其自身轴线旋转）将变换压入栈中，如下图所示。

![](img/1695de1bc7486362f86c143285f3fb40_109_3.png)

![](img/1695de1bc7486362f86c143285f3fb40_109_4.png)

以下是“行星”的步骤序列：

- `push()` 这将是行星 MV 矩阵中也会影响子对象的那一部分。
- `translate(...)` 将行星绕太阳的运动并入行星的 MV 矩阵。在此示例中，我们使用三角函数将行星运动计算为平移。
- `push()` 这将是行星完整的 MV 矩阵，也包括其轴线旋转。
- `rotate(...)` 将行星的轴线旋转并入其中（稍后会将其弹出，不影响子对象）。
- `glm::value_ptr(mvStack.top())` 获取 MV 矩阵，然后将其发送到 MV uniform。
- 绘制行星。
- `pop()` 这将从栈中移除行星 MV 矩阵，露出其下方较早的行星 MV 矩阵副本，该副本不包含行星的轴线旋转（因此只有行星的平移会影响月球）。

现在我们可以编写完整的 display() 例程，如程序 4.4 所示。

### 程序 4.4 使用矩阵栈的简单太阳系

```cpp
stack<glm::mat4> mvStack;
void display(GLFWwindow* window, double currentTime) {
    // setup of background, depth buffer, rendering program, and proj matrices unchanged
    ...
    // push view matrix onto the stack
    vMat = glm::translate(glm::mat4(1.0f), glm::vec3(-cameraX, -cameraY, -cameraZ));
    mvStack.push(vMat);

    // ---------------------- pyramid == sun ----------------------------------
    mvStack.push(mvStack.top());
    mvStack.top() *= glm::translate(glm::mat4(1.0f), glm::vec3(0.0f, 0.0f, 0.0f));  // sun position
    mvStack.push(mvStack.top());
    mvStack.top() *= glm::rotate(glm::mat4(1.0f), (float)currentTime, glm::vec3(1.0f, 0.0f, 0.0f));  // sun rotation
    glUniformMatrix4fv(mvLoc, 1, GL_FALSE, glm::value_ptr(mvStack.top()));
    glBindBuffer(GL_ARRAY_BUFFER, vbo[1]);
    glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 0, 0);
    glEnableVertexAttribArray(0);
    glEnable(GL_DEPTH_TEST);
    glDepthFunc(GL_LEQUAL);
    glDrawArrays(GL_TRIANGLES, 0, 18);        // draw the sun
    mvStack.pop();                           // remove the sun's axial rotation from the stack

    //--------------- cube == planet -----------------------------
    mvStack.push(mvStack.top());
    mvStack.top() *=
        glm::translate(glm::mat4(1.0f), glm::vec3(sin((float)currentTime)*4.0, 0.0, cos((float)currentTime)*4.0));
    mvStack.push(mvStack.top());
    mvStack.top() *= glm::rotate(glm::mat4(1.0f), (float)currentTime, glm::vec3(0.0, 1.0, 0.0));
                                                              // planet rotation
    glUniformMatrix4fv(mvLoc, 1, GL_FALSE, glm::value_ptr(mvStack.top()));
    glBindBuffer(GL_ARRAY_BUFFER, vbo[0]);
    glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 0, 0);
    glEnableVertexAttribArray(0);
    glDrawArrays(GL_TRIANGLES, 0, 36);        // draw the planet
    mvStack.pop();                            // remove the planet's axial rotation from the stack

    //--------------- smaller cube == moon -----------------------
    mvStack.push(mvStack.top());
    mvStack.top() *=
        glm::translate(glm::mat4(1.0f), glm::vec3(0.0, sin((float)currentTime)*2.0,
                      cos((float)currentTime)*2.0));
    mvStack.top() *= glm::rotate(glm::mat4(1.0f), (float)currentTime, glm::vec3(0.0, 0.0, 1.0));
                                                              // moon rotation
    mvStack.top() *= glm::scale(glm::mat4(1.0f), glm::vec3(0.25f, 0.25f, 0.25f)); // make the moon smaller
    glUniformMatrix4fv(mvLoc, 1, GL_FALSE, glm::value_ptr(mvStack.top()));
    glBindBuffer(GL_ARRAY_BUFFER, vbo[0]);
    glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 0, 0);
    glEnableVertexAttribArray(0);
    glDrawArrays(GL_TRIANGLES, 0, 36);        // draw the moon

    // remove moon scale/rotation/position, planet position, sun position, and view matrices from stack
    mvStack.pop(); mvStack.pop(); mvStack.pop(); mvStack.pop();
}
```

矩阵栈操作已高亮显示。有几个细节值得注意：

- 我们在模型矩阵中引入了*缩放*操作。我们希望月球是比行星更小的立方体，因此在为月球构建 MV 矩阵时调用 `scale()`。

这种情况在创建地形或阴影时经常出现。在此类情况下，有时可以预测 Z-fighting，而常见的纠正方法是稍微移动一个对象，使表面不再共面。我们将在第 8 章看到一个示例。

Z-fighting 也可能由于深度缓冲区中数值的精度有限而发生。对于 Z 缓冲区算法处理的每个像素，其深度信息的精度受深度缓冲区中可用于存储该信息的位数限制。用于构建透视矩阵的近裁剪平面和远裁剪平面之间的范围越大，两个对象具有相似（但不相等）实际深度的点就越有可能在深度缓冲区中用相同的数值表示。因此，程序员需要选择近裁剪平面和远裁剪平面的值，以最小化两个平面之间的距离，同时仍确保场景中所有必需的对象都位于视锥体内。

同样重要的是要理解，由于透视变换的效果，改变近裁剪平面值对 Z-fighting 伪影出现可能性的影响，可能比在远裁剪平面上做同等改变更大。因此，建议避免选择离眼睛太近的近裁剪平面。

本书前面的示例只是在调用 `perspective()` 时为近裁剪平面和远裁剪平面使用了 0.1 和 1000 的值。这些值可能需要根据你的场景进行调整。

## 4.10 图元的其他选项

OpenGL 支持多种图元类型——到目前为止我们已经看到两种：`GL_TRIANGLES` 和 `GL_POINTS`。事实上，还有其他几种。OpenGL 支持的所有可用图元类型都属于*三角形、线、点和面片*这几类。以下是完整列表：

### 三角形图元

![](img/1695de1bc7486362f86c143285f3fb40_113_0.png)

这是本书中最常见的图元类型。经过管线的顶点会构成不同的三角形：

| 顶点： | 0 1 2 | **3 4 5** | 6 7 8 | 等。 |
| --- | --- | --- | --- | --- |
| 三角形： | ✓ | ✓ | ✓ |  |

