

## FIGURE 46.5

Fire Effect Parameters rollout 让你定义效果的外观。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1164_0.png)

## FIGURE 46.6

Fire 大气效果可以是 Tendril 或 Fireball 形状。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1164_1.png)

## FIGURE 46.7

Stretch 值可以拉长火焰。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1164_2.png)

## Part XI: Advanced Lighting and Rendering

Regularity 值决定了大气装置被填充的程度。前面几张图中的球形小工具都设置为 0.2，因此整个球形并未被填充。设置为 1.0 会使 Fire 效果呈现球形外观，因为整个小工具都被填充了。若要获得更随机的形状，请使用较小的 Regularity 值。

Flame Size 值会影响每个火焰的整体大小（尽管这也取决于小工具的大小）。Flame Detail 值控制每个火焰的边缘锐度，范围为 1 到 10。较低的值会产生模糊、平滑的火焰，而较高的值则会产生更尖锐、更清晰的火焰。

Density 值决定了每个火焰中心的厚度；较高的 Density 值会导致火焰中心更亮，而较低的值会产生更细、更飘逸的火焰。图 46.8 显示了从左到右 Density 值为 10、20、50 和 100 时产生的差异。

## FIGURE 46.8

Fire 效果的亮度与火焰的 Density 值密切相关。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1165_0.png)

Samples 值设置效果的采样率。需要更高的采样值才能获得更多细节，但这会增加渲染时间。

Motion 部分包含设置火效 Phase 和 Drift 的选项。Phase 值决定火焰燃烧的狂野程度。对于狂暴失控的火焰，请动画化 Phase 值使其快速变化。对于恒定稳定的火焰，请在整个帧中保持该值恒定。Drift 值设置火焰的高度。较高的 Drift 值会产生高耸、燃烧猛烈的火焰。

选中 Explosion 复选框时，火焰将被设置为爆炸。爆炸的开始和结束时间在 Setup Explosion Phase Curve 对话框中设置，该对话框在点击 Setup Explosion 按钮时打开。如果选中 Smoke 选项，则当 Phase 值在 100 到 200 之间时，火焰颜色会变为烟雾颜色。Fury 值会改变火焰的翻滚程度。大于 1.0 的值会导致翻滚更快，小于 1.0 的值会导致翻滚更慢。

### Tutorial: Creating the sun

你可以使用 Fire 效果创建逼真的太阳。建模部分很简单——只需要一个简单的球体——但真正的效果来自材质和 Fire 效果。

要创建太阳，请按照以下步骤操作：

- 1. 从 DVD 上的 Chap 46 目录打开 Sun.max 文件。
- 该文件包含一个简单的球体，并应用了明亮的黄色材质。
- 2. 选择 Create > Helpers > Atmospherics > Sphere Gizmo，并在 Front 视口中拖动一个包围“太阳”球体的球体。

## Chapter 46: Using Atmospheric and Render Effects

- 3. 在 SphereGizmo 仍被选中的情况下，打开 Modify 面板并在 Environment and Effects 对话框的 Atmospheres rollout 中点击 Add 按钮，该对话框可通过 Rendering→ Environment 菜单命令或按 8 键打开。从 Add Atmosphere 对话框中选择 Fire Effect，然后点击 OK。然后选择 Fire 效果并点击 Setup 按钮。Environment and Effects 对话框将打开。
- 4. 在 Fire Effects Parameters rollout 中，保持默认颜色不变——Inner Color 为黄色，Outer Color 为红色，Smoke Color 为黑色。对于 Flame Type，选择 Tendril，Stretch 和 Regularity 值为 1。将 Flame Size 设置为 30，Density 设置为 15，Flame Detail 设置为 10，Samples 设置为 15。

图 46.9 显示了渲染后得到的太阳。

## FIGURE 46.9

使用简单球体、带有 Noise Bump 贴图的材质以及 Fire 效果创建的太阳图像

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1166_0.png)

### Tutorial: Creating clouds

天空图像很容易找到，或者你也可以将相机拿到室外自行拍摄。难点在于当你试图让物体穿梭于云层之间时。虽然你可以用 Shadow/Matte 遮罩来实现这一点，但如果云是真正的 3D 物体则会更容易。在本教程中，你将使用 Fire 效果创建一些简单的云。

要为天空背景创建一些云，请按照以下步骤操作：

## Part XI: Advanced Lighting and Rendering

- 1. 从 DVD 上的 Chap 46 目录打开 Clouds.max 文件。
- 该文件包含几个半球形的大气装置小工具。
- 2. 选择 Rendering→Environment（或按 8 键）打开 Environment and Effects 对话框。点击 Background Color 样本，选择浅蓝色。在 Atmosphere 部分，点击 Add 按钮，从 Add Atmospheric Effect 列表中选择 Fire Effect，然后点击 OK。
- 3. 将效果命名为 Clouds，点击 Pick Gizmo 按钮，选择视口中的每个 Sphere Gizmo 对象，然后点击每个颜色样本。将 Inner Color 改为深灰色，Outer Color 改为浅灰色，Smoke Color 改为白色。将 Shape 设置为 Fireball，Stretch 为 1，Regularity 为 0.2。将 Flame Size 设置为 35，Flame Detail 设置为 3，Density 设置为 15，Samples 设置为 15。

### Tip

如果你想为云添加一些运动，点击 Animate 按钮，将 Time Slider 拖到最后一帧，并将 Phase 值改为 45，Drift 值改为 30。云会缓慢地在天空中漂移。完成后禁用 Animate 按钮。

- 4. 在 Fire Effect Parameters rollout 中，点击 Pick Gizmo 按钮，然后点击视口中的其中一个小工具。重复此步骤，直到选择了所有小工具。

图 46.10 显示了 resulting 天空背景。通过改变 Fire 参数，你可以创建不同类型的云。

## FIGURE 46.10

你可以使用 Fire 大气效果创建云。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1167_0.png)

## Using the Fog Effect

Fog 是一种大气效果，通过引入朦胧层来遮挡物体或背景；离视点越远的物体可见度越低。普通的 Fog 效果无需 Atmospheric Apparatus 小工具即可使用，并出现在摄像机环境范围值之间。摄像机的 Near 和 Far Range 设置决定了这些值。

在 Environment and Effects 对话框中，当 Fog 效果添加到 Effects 列表时会出现 Fog Parameters rollout。该 rollout 如图 46.11 所示，包含用于设置雾色的颜色样本。它还包含用于加载贴图的 Environment Color Map 按钮。如果选择了贴图，Use Map 选项可将其打开或关闭。你还可以为 Environment Opacity 选择贴图，这会影响雾的密度。

Fog Background 选项可将雾应用于背景图像。Type 选项包括 Standard 和 Layered 雾。选择其中一个雾背景选项会启用其对应的参数。

## FIGURE 46.11

Fog Parameters rollout 让你使用 Standard 雾或 Layered 雾。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1168_0.png)

Standard 参数包括 Exponential 选项，用于随距离增加密度。如果禁用此选项，密度将随距离线性变化。Near 和 Far 值用于设置范围密度。

Layered fog 模拟从浓雾区到淡雾区的雾层。Top 和 Bottom 值设置雾的限制，Density 值设置其厚度。Falloff 选项让你设置雾密度降为 0 的位置。Horizon Noise 选项会根据 Size、Angle 和 Phase 值在地平线处的雾层添加噪声。

图 46.12 显示了几种不同的雾选项。左上图像显示无雾的场景，右上图像使用 Standard 选项，左下图像使用 Density 为 50 的 Layered 选项。右下图像启用了 Horizon Noise 选项。

