

粒子在两侧之间移动。周期是完成一次侧向运动循环所需的时间。相位定义了粒子沿振幅曲线开始的位置。

## Particle Spawn rollout

Particle Spawn rollout（如图 41.13 所示）设置在粒子死亡或与其他粒子碰撞时生成新粒子的选项。如果设置为 None，碰撞的粒子会相互弹开，而死亡的粒子则直接消失。Die After Collision 选项会导致粒子在碰撞后消失。Persist 值设置粒子在消失前停留的时间长短。Variation 值会使 Persist 值按定义的百分比变化。

## FIGURE 41.13

Particle Spawn rollout（分为两部分显示）可使粒子生成新的粒子。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1070_0.png)

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1070_1.png)

Spawn on Collision、Spawn on Death 和 Spawn Trails 选项均启用生成控制并定义粒子何时生成新粒子。Spawns 值是粒子可以生成其他粒子的次数。Affects 值是可以生成新粒子的粒子百分比；降低此值会产生一些不生成的粒子。Multiplier 值决定生成的粒子数量。

### Note

Spawn Trails 选项会导致每个粒子在每一帧都生成一个新粒子。此选项可能会迅速产生大量粒子，应谨慎使用。

Chaos 设置定义了生成粒子的方向和速度。Direction Chaos 值为 100 时，生成的粒子可以向任何方向移动，而设置为 0 时则与源粒子方向相同。

Chaos Speed Factor 是生成粒子与其源粒子之间的速度差。此因子可能比原始速度更快或更慢。选择 Both 选项会随机加速一些粒子并减慢其他粒子。您也可以选择让生成粒子使用其父粒子的速度，或将因子值用作固定值。

## Part X: Dynamic Animation

Scale Chaos Factor 的工作原理与 Chaos Speed Factor 类似，只是它会将粒子缩放为比其源粒子更大或更小。

Lifespan Value Queue 允许您定义不同的生命周期级别。原始粒子的生命周期等于队列中的第一个条目。从这些粒子生成的粒子持续时间与第二个值相同，以此类推。要向列表添加值，请在 Lifespan 微调器中输入值并单击 Add 按钮。Delete 按钮可从列表中删除值，Replace 按钮可切换值位置。

如果 Instanced Geometry 是所选的粒子类型，您可以向 Object Mutation Queue 填充在每个生成级别使用的附加对象。这些对象在粒子生成后出现。要选择要添加到队列的新对象，请使用 Pick 按钮。您可以选择多个对象，它们将按列出顺序使用。

## Load/Save Presets rollout

您可以使用如图 41.14 所示的 Load/Save Presets rollout 保存和加载每个粒子配置。要保存配置，请在 Preset Name 字段中输入名称并单击 Save 按钮。所有已保存的预设都显示在列表中。要使用其中一个预设配置，请选择它并单击 Load 按钮。

## FIGURE 41.14

Load/Save Presets rollout 使您能够保存不同的参数设置。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1071_0.png)

### Note

已保存的预设仅对用于保存它的粒子系统类型有效。例如，您不能保存 Super Spray 预设并将其加载到 Blizzard 系统中。

Max 包含多个默认预设，可在入门时使用。这些预设包括 Bubbles、Fireworks、Hose、Shockwave、Trail、Welding Sparks 和 Default（产生直线粒子）。

## Using the Blizzard Particle System

Blizzard 粒子系统使用与 Super Spray 系统相同的 rollout，只是某些选项略有不同。Blizzard 发射器图标是一个带有指向粒子方向的线的平面（类似于 Spray 和 Snow 粒子系统）。粒子从整个平面表面发射。

Blizzard 与 Super Spray 参数之间的差异包括 Blizzard 图标的尺寸。在 Particle Generation rollout 中，您会找到 Tumble 和 Tumble Rate 值。另一个区别是 Particle Type rollout 的 Material Mapping 组下的 Emitter Fit Planar 选项。此选项根据粒子在发射器上的出现位置设置粒子在出生时进行映射。另一个主要区别是 Blizzard 粒子系统没有 Bubble Motion rollout，因为雪花不太适合做气泡。最后，您会在 Load/Save Presets rollout 中找到不同的预设集，包括 Blizzard、Rain、Mist 和 Snowfall。

## Using the PArray Particle System

PArray 粒子系统是一个独特的粒子系统。它从所选对象的表面发射粒子。这些粒子可以从对象的表面、边缘或顶点发射。粒子从与发射器图标分开的对象发射。

PArray 粒子系统包含与 Super Spray 粒子系统相同的许多 rollout。PArray 粒子系统的发射器图标是一个内部有三个四面体对象的立方体。该系统有一些有趣的参数差异，从如图 41.15 所示的 Basic Parameters rollout 开始。

## FIGURE 41.15

PArray 粒子系统的 Basic Parameters rollout 允许您选择粒子形成的位置。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1072_0.png)

在 PArray 系统中，您可以使用 Pick Object 按钮选择单独的对象作为发射器。您还可以选择对象上粒子形成的位置。选项包括 Over Entire Surface、Along Visible Edges、At All Vertices、At Distinct Points 和 At Face Centers。对于 At Distinct Points 选项，您可以选择要使用的点数。

Use Selected SubObject 选项在 Pick Object 按钮选择的地点形成粒子，但仅限于通过 Stack 传递的子对象选择。这在您只想从网格的特定选择发射粒子时很有用，例如龙的嘴或消防水带的末端。PArray 系统 Basic Parameters rollout 中的其他选项与其它系统相同。

Particle Generation rollout 包含一个 Divergence 值。此值是每个粒子相对于发射器法线的速度角变化。

## Splitting an object into fragments

PArray 系统的 Particle Type rollout 包含一种独特的粒子类型：Object Fragments。此类型将所选对象分解为多个碎片。Object Fragment 设置包括 Thickness 值。此值为每个碎片提供深度。如果值设置为 0，碎片将全部为单面多边形。

在 Particle Type rollout 中，All Faces 选项将每个单独的三角形面分离为单独的碎片。此选项的替代方案是使用 Number of Chunks 选项，它使您能够将对象划分为块并定义要使用的块数。第三个选项根据平滑角度拆分对象，可以指定该角度。

在 Particle Type rollout 的 Material 部分，您可以选择用于碎片内部、外部和背面的材质 ID。

Load/Save Presets rollout 包含大量有趣的预设，包括 Blast、Disintegrate、Geyser 和 Comet。

## Tutorial: Creating rising steam

在本教程中，您将创建从街道通风口升起的蒸汽效果。使用 PArray 粒子系统，您可以控制蒸汽的确切位置。

要创建从通风口升起的蒸汽效果，请按照以下步骤操作：

- 1. 打开 DVD 上 Chap 41 目录中的 Street vent.max 文件。此文件包含一个带有通风口的街景。汽车模型由 Viewpoint Datalabs 创建。
- 2. 选择 Create > Particles > PArray 菜单命令，并在 Front 视口中拖动以创建系统。
- 3. 在 Basic Parameters rollout 中，单击 Pick Object 按钮并选择位于通风口对象正下方的 Quadpatch 对象。将 Particle Formation 选项设置为 Over Entire Surface。
- 因为 Plane 对象只有一个面，所以粒子沿着 Plane 的法线方向移动。
- 4. 在 Particle Generation rollout 中，将 Emit Stop 值设置为 100，将 Life 值设置为 60，Variation 为 50。将 Particle Size 值设置为 5.0，Variation 为 30。
- 5. 在 Particle Type rollout 中，选择 Standard Particles 和 Constant Particles 选项。
- 6. 打开 Material Editor（选择 M 键），并将所选的样本槽命名为 steam。单击 Opacity 值右侧的贴图按钮，并在 Material/Map Browser 中双击 Mask 贴图类型。在 Mask Parameters rollout 中，单击贴图按钮并选择 Noise 贴图类型。然后单击 Go to Parent 按钮返回到 Mask 贴图，单击 Mask 按钮并选择 Gradient 贴图类型。对于 Gradient 材质，将黑色颜色样本拖到白色颜色样本上，在出现的对话框中选择 Swap，并启用 Radial 选项。最后，将 steam 材质拖到 PArray 图标上。

图 41.16 显示了第 60 帧的蒸汽通风口。

