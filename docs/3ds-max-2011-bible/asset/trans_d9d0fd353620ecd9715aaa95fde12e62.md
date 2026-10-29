

## FIGURE 44.2

使用预计算的头发可以在渲染时为你节省大量时间。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1133_0.png)

## Simulating Cloth Dynamics

头发并不是唯一受益于动态运动的系统。布料也可以从动态模拟中受益。设置动态布料模拟的步骤与头发类似。首先，应用布料修改器并定义布料属性和作用于布料的环境力。然后运行模拟。

## Defining cloth properties and forces

要将对象（布料和碰撞对象）添加到模拟中，请在 Object rollout 中单击 Object Properties 按钮。这将打开如图 44.3 所示的 Object Properties 对话框。单击 Add Objects 按钮即可选择要添加到模拟中的场景对象。只有添加到场景中的对象才会被包含在模拟中。如果未添加某个对象，则会被忽略。所有添加到模拟中的对象都会添加到左侧的列表中。列表中选中的对象可以指定为 Inactive、Cloth 或 Collision Object。对于 Cloth 和 Collision Objects，可以设置属性。你还可以加载和保存布料预设。布料预设使用 .sti 扩展名保存。

### Tip

如果布料倾向于穿过物体，则可以增加碰撞对象的 Offset 值。

## FIGURE 44.3

Object Properties 对话框让你可以定义布料和碰撞对象的属性。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1134_0.png)

在所有参与模拟的对象都被包含并定义后，你可以在 Simulation Parameters rollout 中设置模拟范围。待覆盖对象的初始状态可以使用位于 Object rollout 中的 Set Initial State 按钮进行设置。Object rollout 中的 Cloth Forces 按钮会打开一个简单的对话框，你可以在其中选择向模拟添加额外的力。重力默认添加，但你可以在 Simulation Parameters rollout 中更改其值。

## Creating a cloth simulation

完成初始设置后，单击 Simulate 按钮即可开始模拟过程。随着每一帧的计算，对象会在视口中更新。计算完每一帧后，你可以通过拖动 Time Slider 或单击 Play Animation 按钮来查看整个动态模拟。如果想在不运行多帧的情况下覆盖布料，可以使用 Simulate Local 按钮。Simulate Local (damped) 按钮会使模拟以局部方式运行并具有大量阻尼，这在布料覆盖过快时很有用。如果想因为某些属性已更改而删除当前模拟，请单击 Erase Simulation 按钮，或者使用 Truncate Simulation 按钮删除当前模拟帧之后的所有帧。

### Tip

如果模拟计算时间过长，可以按 Escape 按钮取消模拟。

如果需要更改布料或力属性，请单击 Erase Simulation，进行更改，然后再次运行模拟。模拟运动可以用 Create Keys 按钮保存为关键帧。图 44.4 显示了一个简单的平面对象，在 100 帧的过程中被覆盖在椅子上。

## FIGURE 44.4

在定义布料和力属性后，执行的模拟会将布料覆盖在椅子上。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1135_0.png)

## Viewing cloth tension

对于使用 Garment Maker 修改器创建的布料对象，你可以使用 Simulation Parameters rollout 中的 Tension 选项查看布料的张力。该选项以阴影颜色显示张力最大的区域。图 44.5 显示了第 29 章“添加和造型头发和毛发，以及使用布料”中女性模型上覆盖的连衣裙的张力。你还可以选择在施加足够力时撕裂的接缝。

## Tutorial: Draping cloth over a jet

作为布料系统的更大示例，你将把一块遮布覆盖在喷气式飞机上。

要模拟布料对象的动态，请按照以下步骤操作：

- 1. 打开 DVD 上 Chap 44 目录中的 Sheet over Mig jet.max 文件。

该文件包含由 Viewpoint Datalabs 创建的 Mig-29 喷气式飞机模型。

- 2. 选择 Create ▸ Standard Primitives ▸ Plane 菜单命令，并在 Top 视口中拖动以创建覆盖飞机的平面对象。将 Length 和 Width 值设置为 150，将 Length 和 Width Segment 值设置为 100 以获得布料所需的足够分辨率，并在 Front 视口中向上拖动平面对象，使其位于飞机上方。

## FIGURE 44.5

你可以使用 Garment Maker 修改器查看创建的布料的张力。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1136_0.png)

### Note

你也可以从应用了 Garment Maker 修改器的矩形样条创建布料。这种方法使用 Delaunay 三角剖分，比 Plane 对象中的矩形部分更适合模拟布料。

- 3. 选择平面对象后，选择 Modifiers ▸ Cloth ▸ Cloth 菜单命令以将 Cloth 修改器应用于该对象。

- 4. 打开 Modifier 面板，并在 Object rollout 中单击 Object Properties 按钮以打开 Object Properties 对话框。在左侧列表中选择 Plane01 对象，并选择 Cloth 选项。然后从 Presets 下拉列表中选择 Silk 选项，并将 Thickness 设置为 0.5。

- 5. 在 Object Properties 对话框仍打开的情况下，单击 Add Objects 按钮，单击 Select All 按钮，然后单击 Add 按钮。选中左侧列表中所有添加的属性后，选择 Collision Object 选项并单击 OK 关闭对话框。

## Part X: Dynamic Animation

6. 在 Simulation Parameters rollout 中启用 End Frame 选项并将结束帧设置为 100。然后在 Object rollout 中单击 Simulate 按钮。平面对象下降并在下落时覆盖被覆盖的喷气式飞机。

图 44.6 显示了覆盖在喷气式飞机上的布单。

## FIGURE 44.6

使用布料系统可以计算布料对象的动态。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1137_0.png)

## Summary

使用动态模拟，你可以控制和计算头发、毛发和布料的运动。这些运动考虑了场景中包含的各种力和碰撞对象。

具体来说，本章涵盖了以下主题：

- Enabling hair dynamics
- Simulating cloth dynamic motion by initiating a simulation process

接下来是第 XI 部分“高级灯光和渲染”。它包括从高级灯光选项开始的多个高级主题的介绍。

## Part XI

## Advanced Lighting and Rendering

- **IN THIS PART**
- **Chapter 45**
Working with Advanced Lighting, Light Tracing, and Radiosity
- **Chapter 46**
Using Atmospheric and Render Effects
- **Chapter 47**
Rendering with mental ray
- **Chapter 48**
Batch and Network Rendering

## Working with Advanced Lighting, Light Tracing, and Radiosity

如果你走进一个黑暗的房间并伸手去找灯开关，如果发现一个单独控制高级灯光的开关，你会感到困惑。但在 Max 中，高级灯光控件值得付出努力。它们使你能够将灯光解决方案提升到下一个层次。

Max 中的高级灯光控件使你能够使用两种单独的全局照明技术来灯光场景，即光线追踪和光子映射。两种解决方案都处理光线从物体反射并被反射到环境中的效果。

光线追踪通常用于室外场景，其中光线由远离场景的单一强光源组成。光线追踪包括表面之间颜色渗色的支持。光线追踪的另一个方面是阴影更柔和。

Radiosity 计算的灯光解决方案比使用标准灯光更逼真。随着你学习使用 radiosity，你很快就会发现它是一个复杂的系统，需要大量调整才能做到完美。

## IN THIS CHAPTER

- Using advanced lighting
- Understanding light tracing
- Setting local advanced lighting parameters
- Understanding radiosity
- Setting global advanced lighting parameters
- Using the Advanced Lighting materials and the Lighting Analysis Assistant

## Selecting Advanced Lighting

你可以在 Advanced Lighting 面板中控制场景的高级灯光设置，该面板是 Render Scene 对话框的一部分。你可以通过选择 Rendering ⇨ Light Tracer 或 Rendering ⇨ Radiosity（或按 9 键）访问此面板。Advanced Lighting 面板包括一个 rollout，其中有一个下拉列表，你可以在其中选择要使用的灯光插件。选项为 None、Light Tracer 和 Radiosity。

### Note

如果启用了 mental ray 渲染器，则 Light Tracer 和 Radiosity 选项不可用。

