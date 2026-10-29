

Opaque Alpha 选项会导致哑膜材质出现在 alpha 通道中。这本质上是一个用于打开和关闭哑膜对象的开关。

你可以将大气效果（如雾和体积光）应用于哑膜材质。At Background Depth 选项会将雾应用于背景图像。At Object Depth 选项会像对象被渲染一样应用雾。

## Cross-Ref

了解有关大气效果的信息，请参阅第 46 章“使用大气和渲染效果。” ■

Receive Shadows 部分可启用在哑膜对象上投射阴影。你还可以指定 Shadow Brightness 和颜色。增加 Shadow Brightness 值会使阴影更透明。Affect Alpha 选项会使阴影成为 alpha 通道的一部分。

哑膜对象也可以具有反射。Amount 旋钮控制使用多少反射，Map 按钮打开 Material/Map Browser。

## Tutorial: Adding 3D objects to a scene

哑膜/阴影贴图的常见用途是将 3D 对象添加到背景图像中。例如，如果你添加一个与背景图像中地面平面对齐的 Plane 对象，并对其应用哑膜/阴影材质，那么 Plane 对象可以捕捉 3D 对象的阴影，但哑膜/阴影材质允许背景透过 Plane 对象看到。结果是 3D 对象看起来被添加到背景图像场景中。

要使用哑膜/阴影材质将对象添加到背景图像，请按照以下步骤操作：

- 1. 打开 DVD 上 Chap 30 目录中的 Xylophone on shadow matte.max 文件。
该文件包含在波士顿会议中心前拍摄的牛雕像背景图像。场景还包括放置在 Plane 对象上的木琴。Plane 对象具有 4 的 Scale multiplier，以便在场景渲染时形成完整的地面平面。
- 2. 通过按 M 键盘快捷键打开 Slate Material Editor。双击 Material/Map Browser 中的 Matte/Shadow 选项。命名材质为 Shadow plane，并将其应用于 Perspective 视口中的 Plane 对象。
- 3. 选择 Create▶Lights▶Standard Lights▶Omni 菜单并在 Top 视口中单击以创建灯光。在 General Parameters 展开面板中启用 Shadows 选项。然后在 Shadow Parameters 展开面板中，单击 Color 样本。 在打开的 Color Selector 中，选择 Sample Screen Color 吸管工具并单击牛的阴影颜色以选择它。然后将 Density 设置调整为 0.7 以使阴影略微透明。
- 4. 右键单击视口左上角 Perspective 视口的渲染标签并选择 Lighting and Shadows▶Enable Hardware Shading。然后选择 Lighting and Shadows▶Enable Shadows 选项。
这会使阴影在 Plane 对象上出现在视口中。
- 5. 在 Left 和 Top 视图中移动 Omni 灯，直到阴影沿着与牛阴影相同的路径投影。

## Tip

帮助对齐阴影的一种方法是使平行几何对象的阴影，如木琴的垂直腿和牛的腿，保持平行。 ■

6. 要查看最终结果，你需要渲染图像。为此，选择 Rendering→ Render（或按 F10）以打开 Render Scene 对话框。单击对话框底部的 Render 按钮，图像将在 Rendered Frame Window 中渲染，或按 F9 键。

Figure 30.1 显示了 resulting 渲染图像。

## FIGURE 30.1

由于其阴影投射到应用了哑膜/阴影材质的对象上，因此渲染的木琴完美融入场景。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_826_0.png)

## Using the Ink ‘n’ Paint Material

虽然看起来可能很傻，但许多不同的制作公司使用 Max 来创建 2D 手绘卡通。这是通过使用 Ink ‘n’ Paint 材质实现的。传统上，卡通是通过纸和笔手工绘制的。然后动画公司发现，使用计算机可以轻松填充卡通特征，但使用 Max 这样的 3D 程序，其能够使用关键帧进行动画，进一步简化了动画任务。区别在于对象的渲染方式；Ink ‘n’ Paint 材质控制这一点。

选择 Ink ‘n’ Paint 材质后，会出现多个展开面板，包括 Basic Material Extensions。该展开面板包括使材质 2-Sided、启用 Face Map 和使材质 Faceted 的选项。其他选项会导致在不绘制时背景变雾，并使 alpha 通道不透明。可用的贴图包括 Bump 和 Displacement。

## Controlling paint and ink

Paint Controls 展开面板包括有关油漆（或墨水轮廓内的颜色）如何应用的设置。你可以为 Lighted、Shaded 和 Highlight 颜色指定颜色。Lighted 颜色用于面向场景灯光的材质部分，Shaded 颜色用于处于阴影中的部分，而 Highlight 颜色用于高光。对于每种颜色，你还可以选择一个具有 amount 值的贴图。Paint Levels 值设置用于为材质着色的颜色数量。Glossiness 值决定高光的大小。Figure 30.2 显示了 Paint Level 值为 2–6 的材质。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_827_0.png)

Ink Controls 展开面板包括一个 Ink 选项，可用于完全关闭轮廓墨水。你还可以将 Ink Quality 设置为 1 到 3 之间的值。质量越高，边缘描绘越好，但完成所需时间更长。墨水笔划的宽度可以设置为 Variable Width 或 Clamped 宽度。对于每个选项，你可以选择 Minimum ink width，如果启用 Variable Width，你还可以选择 Maximum ink width。对于 Variable Width 选项，笔划会发生变化，以便在光照区域使用最小设置，在阴影区域使用最大宽度。这有助于强调光照。你还可以将墨水宽度作为贴图应用。Figure 30.3 显示了 Ink ’n’ Paint 材质应用于立方体。第一张图像显示标准材质；第二张图像已禁用 Ink 选项。最后三张图像的 Width 值分别为 1、10 和 30。

## Tip

在 Ink Width 属性上放置一个 noise 贴图是让墨水轮廓呈现手绘外观的好方法。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_827_1.png)

Ink Controls 展开面板中的其余选项用于控制墨水应用于对象的何处。选项包括 Outline、Overlap、Underlap、Smoothing Group 和 Material ID。对于这些选项中的每一个（Smoothing Group 除外），你可以更改 Bias 值以调整相交边缘。这些选项中的每一个都可以作为贴图应用。

## Tutorial: Cartooning a turtle

作为 Ink ’n’ Paint 材质的示例，你将渲染一个由 Zygote Media 创建的卡通风格乌龟模型，使其成为适合周日版报纸的卡通。

要将 Ink ’n’ Paint 材质应用于乌龟模型，请按照以下步骤操作：

- 1. 打开 DVD 上 Chap 30 目录中的 Cartoon turtle.max 文件。
该文件包含一个简单的乌龟模型。
- 2. 选择乌龟模型后，通过选择 Rendering > Material Editor > Slate Material Editor 菜单命令打开 Material Editor（或按 M 键）。
- 3. 在 Utility 面板中，选择 Color Clipboard 按钮，并在 Color Clipboard 展开面板中单击 New Floater 按钮。调色板打开。将 Material Editor 中每个当前材质的 Diffuse 颜色拖到 Color Clipboard。Max 会询问你是否要 Swap、Copy 或 Cancel 材质。选择 Copy 选项。保持 Color Clipboard 窗口打开。
- 4. 选择第一个样本槽，并单击 Material Type 按钮以打开 Material/Map Browser。从列表中双击 Ink ’n’ Paint 材质类型。然后从 Color Clipboard 拖动相应的颜色并将其复制到 Paint Controls 展开面板的 Lighted 颜色样本中。对每个五个材质重复此操作。
- 5. 使用 Render Scene 对话框打开并渲染 Perspective 视口。

Figure 30.4 显示了 resulting 卡通。

## FIGURE 30.4

使用 Ink ‘n’ Paint 材质轻松制作卡通

![](img/ebbb4844f027f7d1c580e48108d2b6cb_828_0.png)

## Using Architectural Materials

如果你查看 Material/Map Browser，你会注意到一个 Architectural 材质。该材质专门设计用于创建逼真的材质，可应用于建筑物和室内。Architectural 材质使用预定义模板来创建建筑物中几乎任何类型的材质，包括陶瓷、织物、金属、玻璃、石头、木材和水。使用 Architectural 材质的好处在于它们与真实世界灯光的交互。使用 Photometric 灯光和 Radiosity 可产生逼真效果。

## Cross-Ref

> 如果你已选择 mental ray 渲染器，则 Arch & Design 材质和各种 ProMaterials 将可用。这些材质是更强大、更全面的建筑材质集。你可以在本章后面了解有关此和其他 mental ray 材质的更多信息。

## Part VII: Advanced Materials

## Chapter 30: Using Specialized Material Types

