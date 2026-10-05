

通过教程学习 Unity 游戏

## 软粒子：未勾选

实时反射探针：已勾选

看板面向摄像头：已勾选

| 渲染 | |
| :--- | :--- |
| 像素光照数量 | 全分辨率 |
| 纹理质量 | |
| 各向异性纹理 | 每个纹理 |
| 各向异性抗锯齿 | 2x 多重采样 |
| 软粒子 | |
| 实时反射 | |
| 看板面向相机 | |
| 分辨率缩放 Fi: 1 |

了解更多关于 Unity 和 Oculus 设置，请查阅《从 Oculus 构建移动应用》文档。你可以在这里找到它：https://developer.oculus.com/documentation/unity/latest/concepts/unity-build-android/#unity-build-android

# 为你的应用签名

信不信由，你还有更多配置需要完成！尽管你已经从 Oculus 应用中启用了开发者模式，你仍然需要对应用进行签名。坦率地说，这个签名过程非常简单。要获取证书，请前往 OSIG 生成器。你可以在这里找到它：https://dashboard.oculus.com/tools/osig-generator/

一旦填写完关于头显的信息，系统将为你提供证书。你需要将其添加到你的项目中。在你的项目浏览器中，将证书添加到以下位置（区分大小写）：**Assets > Plugins > Android > assets/**

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_574_0.png)

raywriterlich.com

# 侧载你的游戏

最后，构建你的游戏并将 APK 文件保存到桌面。如果这是你第一次将头显用于开发，你需要对游戏进行侧载（sideload）。你需要通过 Android 调试桥 (ADB)来实现这一点，它是我之前提到的 Android SDK 的一部分。根据你安装 Android SDK 的位置，在 **Android SDK platform-tools** 子目录下找到 ADB。此外，你将通过命令行访问它。要侧载你的 APK 文件，只需运行命令：`adb install -r`

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_575_0.png)

你将收到一条消息显示设备未授权。现在，戴上你的头显并确认你想要使用该设备进行开发。确保勾选了 USB 调试选项。确认后，运行相同的 ADB 命令安装你的 .apk 文件。它应该无问题地复制文件，加载后，它将出现在你的 Oculus Go 库中。更棒，你现在可以在 Unity 内部进行构建和运行，游戏会自动安装到你的头显上。

# 在 Oculus 上运行

此时，Oculus Rift 或 Oculus Rift Go 都可以运行该游戏。确保你的 Rift 已开启，然后保存并播放游戏场景（Game scene）。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_575_1.png)

# 通过教程学习 Unity 游戏

如果你拿起 Rift 并轻轻移动，显示器将回应该动作和旋转。但先不要戴上 HMD（头戴器），因为相机还没有设置好。

禁用主相机（Main Camera），并将 OVR ▸ Prefabs 文件夹中的 OVRCameraRig 预制体拖到层级（Hierarchy）中。

选择 OVRCameraRig，并将其位置设置为 (-1, 7.3, 1.54)。这将使相机处于正确的位置。调整你的姿势并准备好 HMD，现在运行场景并戴上 Rift。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_576_0.png)

观察 UI 和不断进的敌人。一切都应该如预期般运行——直到你尝试近距离观察风景或敌人。当你这样做这样做时，你会发现自己几乎无法移动，只能注视。这是因为 OVRCameraRig 的默认缩放被设置为现实比例。如果你在现实世界中移动一点，相机在场景中的移动距离也与此大致相同。

为了解决这个问题，你将变成一个巨人！选择 OVRCameraRig 并将其缩放设置为 (12, 12, 12)。戴好 HMD 站起来，留出足够的空间让你蹲下，然后按下播放按钮测试你新获得的力量。现在尝试注视和移动，并蹲下近观察敌人和场景。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_576_1.png)

很酷，对吧？

# 与世界交互

下一步是实现一些交互。现在敌人源源不断，但没有办法使用塔楼槽位放置新塔楼。

首先，OVR 相机需要一个物理射线投射器（Physics Raycaster）向玩家注视的场景中发射射线。在层级视图中选择 OVRCameraRig > TrackingSpace > CenterEyeAnchor，并添加 Physics Raycaster 组件。你可以在检查器（Inspector）面板中点击 Add Component 按钮并搜索 Physics Raycaster 来完成。

接下来需要一种在世界和 UI 上指向并选择对象的方法。为此，你需要一个新的输入模块（Input Module），即视线输入模块（Gaze Input Module）。

视线输入意味着玩家视图中心有一个 3D 指针，让他们能够轻松聚焦于物体。

视线输入意味着玩家视图中心有一个 3D 指针，让他们能够轻松聚焦于物体。![](img/fd5c2ca20ea33da76d2b61297cc57f6c_577_0.png)

传统的做法是通过注视（或凝视）物体来选择的。但在 Oculus 的情况下，视线输入是内置的。别担心，这并不是由 Oculus 提供的。在项目面板中创建一个名为 OculusGazeModule 的新脚本。在文件顶部添加以下使用 语句：

```csharp
using System.Generic;
using UnityEngine;
using UnityEngine.EventSystems;

public class OculusGazeModule : MonoBehaviour {

public GameObject reticle;
public Transform centerEyeTransform;
public float reticleSize = 0.02f;
private PointerDataData eventData;
private RaycastResult currentRaycast;
```

这些是变量：

- 1. 玩家注视的物体的引用。
- 2. 中心眼睛相机的引用。
- 3. 根据距离和 reticleSizeMultiplier调整调整视粒子大小。
- 4. 用于事件系统的 PointerData。
- 5. 射线射射场景的结果。
- 6. OVRCamera 将是。

在 Process 下添加这个空方法：

```csharp
public override void Process()
{
}
```

在 Process 下添加 HandleLook() 方法：

```csharp
void HandleLook()
{
    if (eventData == null)
    {
        eventData = new PointerData(eventSystem);
    }
}
```

逐条处理每个注释的部分：

- 2. 将虚拟指针的位置设置为屏幕中心。
- 3. 创建一个存储射线检测结果的列表。
- 4. 对 UI 中所有启用的射线投射器进行射线检测。

```csharp
    eventData.position = Camera.main.ViewportToScreenPoint(new Vector3(.5f, .5f));
    List<RaycastResult> raycastResults = new List<RaycastResult>();
    eventSystem.RaycastAll(eventData, raycastResults);
    eventData.currentRaycast = FindFirstRaycast(raycastResults);
    reticle.transform.position = centerEyeTransform.position + (centerEyeTransform.forward * currentRaycast.distance);
    float currentReticleSize = currentRaycast.distance * reticleSize;
    reticle.transform.localScale = new Vector3(currentReticleSize, currentReticleSize, currentReticleSize);
    ProcessMove(eventData);
```

- 5. 获取任何射线检测的首次命中，并将其保存到 currentRaycast 和 PointerData 的射线数据中。
- 6. 将视粒子移动到射线命中的点。
- 7. 根据与中心眼睛相机的距离和 reticleSize 调整视粒子的大小。
- 8. 将指针数据传递给事件系统，以便正确处理进入和退出对象的情况。

添加此方法来处理玩家输入：

```csharp
void HandleSelection()
{
    if (eventData.pointerEnter != null )
```

