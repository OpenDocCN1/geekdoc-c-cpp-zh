

```cpp
    {
        closest = c.t;
        closest_collision = c;
        closest_collision.object_index = i;
    }
}
return closest_collision;
}
...
void process_stack_element(int index)
{
    // ... phases 1-4 remain unchanged
    // PHASE 5 - Mixing to produce the final color – generalized for any combination of these objects
    if(stack[index].phase == 5)
    {
        if (c.object_index > 0) // we collided with something, and it is not a room box
        {
            // first get texture color if applicable
            vec3 texColor = vec3(0.0);
            if (objects[c.object_index].hasTexture)
                texColor = getTextureColor(c.object_index, c.t);

            // next, get object color if applicable
            vec3 objColor = vec3(0.0);
            if (objects[c.object_index].hasColor)
                objColor = objects[c.object_index].color;

            // then get reflected and refractive colors, if they are needed later
            vec3 reflected_color = stack[index].reflected_color;
            vec3 refracted_color = stack[index].refracted_color;

            // Now build the mix of colors – if it is the last color, just return it without blending
            vec3 mixed_color = objColor + texColor;
            if ((objects[c.object_index].isReflective) && (stack[index].depth<max_depth))
                mixed_color = mix(mixed_color, reflected_color, objects[c.object_index].reflectivity);
            if ((objects[c.object_index].isTransparent) && (stack[index].depth<max_depth))
                mixed_color = mix(mixed_color, refracted_color, objects[c.object_index].index_of_refraction);
            stack[index].final_color = mixed_color * stack[index].phong_color;
        }

        if (c.object_index == 0)        // room box object is unique because it might have six textures
        {
            vec3 lightFactor = vec3(1.0);        // holds the lighting value if isReflective is true
            if (objects[c.object_index].isReflective) lightFactor = stack[index].phong_color;

            if (objects[c.object_index].hasColor) // here, roomboxes have color or texture (not both)
                stack[index].final_color = lightFactor * objects[c.object_index].color;
            else
                if (c.face_index == 0) stack[index].final_color = lightFactor * getTextureColor(5, c.t);
                else if (c.face_index == 1) stack[index].final_color = lightFactor * getTextureColor(6, c.t);
                else if (c.face_index == 2) stack[index].final_color = lightFactor * getTextureColor(7, c.t);
                else if (c.face_index == 3) stack[index].final_color = lightFactor * getTextureColor(8, c.t);
                else if (c.face_index == 4) stack[index].final_color = lightFactor * getTextureColor(9, c.t);
                else if (c.face_index == 5) stack[index].final_color = lightFactor * getTextureColor(10, c.t);
        }
    }
    ... // other parts of this function are unchanged
}
```

程序 16.13 中 objects 数组的定义与之前程序 16.10 和 16.11 中构建的示例相对应，其输出与图 16.18 所示一致。请注意，程序中仍然有一些地方（除了 objects 数组的定义之外）可能需要根据场景稍作调整：相机位置、光源位置、每个带纹理对象所使用的纹理采样器（如果是程序化纹理，则是要使用的函数——这些都在 getTextureColor() 中指定）、递归深度，以及是否需要阴影（要禁用阴影，只需在 ads_phong_lighting() 函数中注释掉相关测试即可）。当然，还可以通过将光线求交和纹理化等任务封装到对象子类型中，进一步泛化该程序，这也会使其更容易扩展。

### 16.3.6 其他示例

现在光线追踪程序已经完成，并可用于我们基本对象的各种组合，让我们尝试第 16.3.4 节开头讨论的一些有趣情况。对于每种配置，我们需要设置适合特定场景的以下变量：

- 构成场景的对象（通过填充 objects 数组）
- 对象的数量（通过设置变量 numObjects）
- 沿 Z 轴的相机位置（通过设置变量 camera_pos）
- 最大递归深度（通过设置变量 max_depth）
- 递归栈的最大大小（通过设置变量 stack_size）
- 位置光源的位置（通过设置变量 pointLight_position）

例如，我们的光线追踪器现在能否看到一个位于另外两个透明物体之后的对象？我们可以通过定义 objects 数组来测试：其中包含两个薄折射盒和一个放在它们后面的实心红球，如程序 16.14 所示。红球和透明盒都位于正 Z 轴上，距离分别为 2.0、3.0、4.0 和 5.0，相机也位于正 Z 轴上，距离为 5.0。

**程序 16.14 透过多个透明物体观察**

计算着色器

```cpp
...
Object[] objects =
{
    // object #0 is the room box – this time the room box is white (or grey depending on the lighting)
    { 0, 0, vec3(-20, -20, -20), vec3(20, 20, 20), 0, 0, 0, vec3(0), true, false, true, false, vec3(1.0, 1.0, 1.0),
      0, 0, 0, vec4(0.2, 0.2, 0.2, 1.0), vec4(0.9, 0.9, 0.9, 1.0), vec4(1.0, 1.0, 1.0, 1.0), 50.0
    },
    // red sphere
    { 1, 0.25, vec3(0), vec3(0), 0, 0, 0, vec3(0, 0, 2), true, false, false, false, vec3(1.0, 0.0, 0.0), 0.0, 0.0, 0.0,
      vec4(0.3, 0.3, 0.3, 1.0), vec4(0.7, 0.7, 0.7, 1.0), vec4(1.0, 1.0, 1.0, 1.0), 50.0
    },
    // transparent box with no texture
    { 2, 0, vec3(-0.5, -0.5, -0.1), vec3(0.5, 0.5, 0.01), 0, 0, 0, vec3(0, 0, 0.4), true, false, false, true,
      vec3(0.9, 0.9, 0.9), 0.0, 0.95, 1.1, vec4(0.8, 0.8, 0.8, 1.0), vec4(1.0, 1.0, 1.0, 1.0), vec4(1.0,
      1.0, 1.0, 1.0), 50.0
    },
    // transparent box with no texture
    { 2, 0, vec3(-0.5, -0.5, -0.1), vec3(0.5, 0.5, 0.01), 0, 0, 0, vec3(0, 0, 0.3), true, false, false, true,
      vec3(0.9, 0.9, 0.9), 0.0, 0.95, 1.1, vec4(0.8, 0.8, 0.8, 1.0), vec4(1.0, 1.0, 1.0, 1.0), vec4(1.0,
      1.0, 1.0, 1.0), 50.0
    }
};
int numObjects = 4;
float camera_pos = 5.0;
const int max_depth = 5;
const int stack_size = 100;
vec3 pointLight_position = vec3(-1,1,3);
...
```

程序 16.14 的输出如图 16.20 所示。请注意，当递归深度为 3 时，红球不可见，因为光线序列不足以穿过两个盒子的两侧并到达球体。然而，当递归深度为 5 时，球体变得可见。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_472_0.png)

**图 16.20**
程序 16.14 的输出，显示红球透过两个薄透明盒。左图的递归深度为 3，右图的递归深度为 5。

第 16.3.4 节中讨论的另一个示例是两面镜子相对的情况。如图 16.18 所示，当两面镜子与观察者之间的相对角度恰好合适时，会出现一种“递归隧道”。我们的光线追踪器能复现这种效果吗？

我们通过创建两个反射平面（用作镜子），并在它们之间放置一个红球和相机来测试这一点。图 16.21 显示了这些对象的布局，它们都沿 Z 轴放置（某些情况下略有偏移），相机朝负 Z 方向观察。尽管相机（以绿色显示）无法看到位于其后面的平面，但它应该能够看到前方的镜子、红球，以及当反射在两面镜子之间来回反弹时红球的额外影像。程序 16.15 设置了这些对象如此朝向的场景。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_472_1.png)

**图 16.21**
构建两面相对的镜子。

