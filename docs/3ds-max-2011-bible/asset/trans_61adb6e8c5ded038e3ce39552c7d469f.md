

## 动画恐龙

测试渲染完成后，场景看起来不错，我们可以进入动画阶段。此阶段涉及使用 Character Animation Toolkit (CAT) 工具为恐龙添加骨骼绑定。骨骼可以轻松动画化，从而使恐龙网格蒙皮跟随。

## 教程：添加预设 CAT 绑定

为角色动画化的第一步是添加与恐龙网格相匹配的底层骨骼绑定。完成此操作后，动画任务会变得迅速。

要为恐龙添加预设 CAT 绑定，请按照以下步骤操作：

- 1. 点击界面右下角的最大化视口切换按钮，切换回四个视口。然后放大 Top 视口，以便可以看到整个场景。
- 2. 选择恐龙对象，并选择 Edit ⇨ Select Invert 菜单；然后在视口中右键单击，并在弹出四菜单中选择 Hide Selected 选项。这会隐藏恐龙以外的所有内容。
- 3. 打开 Create 面板，并选择 Helpers 类别。然后选择 CAT Objects 子类别。点击 CAT Parent 按钮，选择 Allosaurus 预设，并在 Top 视口中拖动，直到 CAT 绑定与脚对齐，并且在 Left 视口中与恐龙背部一样高。
- 4. 使用主工具栏中的 Move 工具，在 Front 视口中选择左侧绑定脚并向左拖动，使其与蒙皮网格脚对齐。然后在 Left 视口中向前移动上部和下部左侧腿骨以匹配蒙皮网格腿。
- 5. 使用 Front 和 Left 视口移动绑定臂的骨骼，使其与蒙皮网格的臂匹配，仅限左侧臂。
- 6. 打开 Modify 面板，并选择左侧上腿骨，然后点击 Ankle Setup 展开区中的 Copy Bone Settings 按钮。然后选择右侧脚踝骨，并选择 Mirror Bone Settings 按钮。这会使左侧腿的骨骼更改应用于右侧。然后对臂重复此步骤。
- 7. 在 Left 视口中向前拖动头部骨骼以与蒙皮网格的头部对齐。选择其中一个尾骨，并在 Tail Setup 展开区中将 Num Links 设置为 5；然后移动并定向骨骼以匹配蒙皮网格。
- 8. 当绑定与蒙皮网格对齐时，选择蒙皮网格并选择 Modifiers ⇨ Animation ⇨ Skin 菜单命令以将 Skin 网格应用于恐龙。点击 Parameters 展开区中的 Add 按钮，并在 Select Bones 对话框中选择除 Allosaurus 辅助对象和两个腿部平台辅助对象之外的所有对象，然后点击 Select 按钮。图 QS.6 显示了与蒙皮网格对齐的 CAT 绑定的恐龙。

### Tip

如果发现自己选择蒙皮网格太频繁，可以右键单击它并选择 Freeze Selection 以冻结它，使其无法被选择。完成后使用 Unfreeze All 选项将其解冻。

## FIGURE QS.6

CAT 绑定与恐龙蒙皮网格下方对齐。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_58_0.png)

## 教程：创建行走运动路径

绑定和蒙皮应用后，您就可以开始动画化恐龙行走。这就是应用 CAT 绑定显示其用处的地方。

要动画化恐龙行走，请按照以下步骤操作：

- 1. 在视口中右键单击，并选择 Unhide All 选项以使所有场景对象再次可见。
- 2. 选择 CAT Parent 对象，并在 Top 视口中将其拖动到平面对象的右上角；然后将其旋转以面向平面对象的中心。
- 3. 在底部边缘的主界面中，找到 Time Configuration 按钮并点击它。在 Time Configuration 对话框中，将 End Time 设置为 300 并关闭对话框。这会将帧范围增加到 300。
- 4. 选择 Create > Helpers > Dummy 菜单命令，并在 Top 视口中拖动以在恐龙位置附近创建一个虚拟对象。虚拟对象仍处于选中状态时，点击界面底部的 Auto Key 按钮，将 Time Slider 拖动到第 300 帧，并将虚拟对象在视口中移动到 Top 视口的左下角。然后关闭 Auto Key 按钮。

### Tip

记住在完成动画后关闭 Auto Key 按钮，否则在编辑场景时您会继续创建关键帧。

- 5. 选择 CAT Parent 对象，打开 Motion 面板，点击 Layer Manager 展开区中层列表下方的 Add Layers 按钮，并选择 CAT Motion 层选项。列表中会添加一个新层。
- 6. 点击 Layer Manager 展开区中列表上方的 Animation 模式按钮，然后点击列表下方的 CAT Motion Editor 按钮。在打开的对话框中，在左窗格中选择 Globals 面板，点击 Path Node 按钮，然后选择动画化的虚拟对象。暂时保持 CAT Motion 对话框打开。
- 7. 选择虚拟对象，并将其旋转，使恐龙直立并指向虚拟对象移动的方向。
- 8. 再次选择 CAT Parent 对象，并在 CAT Motion 对话框中选择 Limb Phases 面板。然后点击 Pick Ground 按钮，并在视口中选择地面平面对象。这会使 CAT 绑定的所有脚印跟随地面平面。
- 9. 放大并在 Perspective 视口中旋转视图，使恐龙从视野中走过。
- 10. 点击主工具栏中的 Select by Name 按钮，选择所有骨骼对象，在视口中右键单击并选择 Hide Selected 选项以隐藏所有骨骼。

点击 Play 按钮即可看到添加到恐龙的步行循环。图 QS.7 显示了视口中的行走恐龙。

## FIGURE QS.7

恐龙以笨重的步态在山丘上行走。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_59_0.png)

## 教程：渲染最终动画

一旦恐龙行走在视口中看起来不错，您就可以准备渲染最终动画。这是一个可以通过指定动画格式开始的过程。一旦开始，Max 会自动处理动画的所有帧，并在完成后通知您。

要渲染最终动画，请按照以下步骤操作：

- 1. 选择 Render→ Render Setup 菜单以打开 Render Setup 对话框。
- 2. 在对话框顶部，启用 Active Time Segment，以便渲染动画的所有 300 帧。然后将 Output Size 设置为 640x480。
- 3. 在 Render Output 部分，点击 Files 按钮以打开文件对话框。将格式设置为 AVI，为文件命名为 Walking Dinosaur 之类的名称，然后点击 Save 按钮。在出现的 AVI Compression Setup 对话框中，只需选择默认值并点击 OK。
- 4. 在 Render Setup 对话框的底部，确保选择了 Perspective 视图并点击 Render 按钮。

Max 然后渲染动画的每一帧，并在对话框中显示其进度。完成后，最终动画文件将以您输入的文件名保存。然后您可以找到并播放它。图 QS.8 显示了最终动画的一帧。

## FIGURE QS.8

最终动画包括每一帧的渲染结果。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_60_0.png)

## Summary

我希望您对进入 Max 的第一步感到满意。本章让您接触到 Max 的许多重要方面，包括以下内容：

- 设置场景
- 启用 mental ray
- 为场景对象应用材质
- 使用 Sun & Sky 系统并在视口中启用灯光和阴影
- 将预设 CAT 绑定与蒙皮网格匹配
- 使用 CAT Motion 层创建步行循环
- 渲染最终动画

但请系好安全带，因为软件中还有太多内容等待您。在第 1 章中，您将轻松开始深入了解 Max 界面。如果您准备好迎接更高级的挑战，请查看目录并深入研究任何看起来不错的主题。

