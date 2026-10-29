

## Part I: Getting Started with 3ds Max

左右移动；使用上下两个方块进行相同操作时，视图会上下旋转。点击圆圈内并拖动会在单一平面内旋转，点击并拖动圆圈外部则会绕圆心顺时针或逆时针旋转视图。如果感到困惑，请观察光标，它会根据旋转类型而改变。Ctrl 和 Alt 键也可以加快或减慢旋转视图。图 2.9 还显示了一个使用 Min/Max Toggle 按钮最大化的视口。

**Figure 2.9** — The rotation guide appears whenever the Arc Rotate button is selected.

Rotation guide

![](img/ebbb4844f027f7d1c580e48108d2b6cb_97_0.png)

> **Note:** If you rotate one of the default non-perspective views, it automatically becomes an Orthographic view, but you can undo the change using the Views → Undo View Change command or the Shift+Z shortcut.

### Maximizing the active viewport

迟早有一天，视口会感觉太小了。当这种情况发生时，你有几种方法可以增大视口大小。第一个要尝试的技巧是点击并拖动任意视口边框来改变视口大小。拖动视口交汇处可以同时调整所有视口大小。图 2.10 显示了动态调整大小后的视口。

**Figure 2.10** — You can dynamically resize viewports by dragging their borders.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_98_0.png)

> **Tip:** You can return to the original layout by right-clicking any of the viewport borders and selecting Reset Layout from the pop-up menu.

第二个技巧是使用 Min/Max Toggle (Alt+W) 将活动视口扩展以填满四个视口所占的空间。再次点击 Min/Max Toggle（或按 Alt+W）即可返回到定义的布局。

最大化视口只能暂时解决问题，但在此之前，你可以再进一步，在说服老板给你买更大显示器之前。你可以通过选择 Views → Expert Mode (Ctrl+X) 进入专家模式。它通过移除主工具栏、命令面板和大部分下部界面栏来最大化视口空间。

在大部分界面元素被移除后，你需要依靠菜单、键盘快捷键和四键菜单来执行命令。要重新启用默认界面，请点击 Max 窗口右下角的 Cancel Expert Mode 按钮（或再次按 Ctrl+X）。图 2.11 显示了专家模式下的界面。

**Figure 2.11** — Expert Mode maximizes the viewports by eliminating most of the interface elements.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_99_0.png)

### Controlling camera and spotlight views

如果场景中存在摄像机或聚光灯，你可以将任意视口设置为摄像机视图 (C) 或聚光灯视图 ($)。当其中任一视图处于活动状态时，视口导航控件按钮会发生变化。在摄像机视图中，推拉、滚动、横移、平移、环绕和视场控制会激活。灯光视图包含衰减和热点控制。

> **Cross-Ref:** Chapter 19, “Configuring and Aiming Cameras,” and Chapter 20, “Using Lights and Basic Lighting Techniques,” cover these changes in more detail.

### Changing the Viewport Display

尽管视口导航控件侧重于控制视口中可见的内容，但 Views 菜单中以及每个视口顶部的视口标签中也有许多有用的命令，可直接影响视口。三个视口标签包括通用视口标签（即简单的加号）、视点视口标签和着色视口标签。

### Undoing and saving viewport changes

如果你在视图中迷路了，可以使用 Views → Undo View Change (Shift+Z) 和 Views → Redo View Change (Shift+Y) 来撤消和重做视口更改。这些命令与 Edit → Undo 和 Edit → Redo 命令不同，后者可以撤消或重做几何体更改。

你可以使用 Views → Save Active Viewport 菜单命令保存对视口所做的更改。此命令保存视口导航设置以便召回。要恢复这些设置，请使用 Views → Restore Active Viewport。

> **Note:** The Save and Restore Active Viewport commands do not save any viewport configuration settings, just the navigated view. Saving an active view uses a buffer, so it remembers only one view for each viewport.

### Disabling and refreshing viewports

如果场景变得过于复杂，你可能会在等待每个视口更新更改时出现减速，但不用担心，因为有几个选项可以帮助你。第一个要尝试的选项是禁用视口。

你可以通过右键单击通用视口标签并从弹出菜单中选择 Disable View 菜单命令来禁用视口，也可以通过键盘快捷键 D 来操作。当禁用的视口处于活动状态时，它会正常更新；当它处于非活动状态时，视口根本不会更新，直到它再次变为活动状态。禁用的视口会在左上角视口标签旁边显示“Disabled”字样来标识。

提高视口更新速度的另一个技巧是禁用 Views → Update During Spinner Drag 菜单选项。更改参数微调器可能会导致减速，因为微调器变化时每个视口都需要更新。如果微调器变化很快，即使是强大的系统也会明显变慢。禁用此选项会导致视口等待微调器停止变化后再更新。

有时在进行更改后，视口并未完全刷新。这通常发生在其他程序的对话框被移动到视口前面或对象被移动时发生，因为它们经常相互遮挡并且线条会消失。如果发生这种情况，你可以使用 Views → Redraw All Views 菜单命令（键盘快捷键，\`）强制 Max 刷新所有视口。Redraw All Views 命令刷新每个视口并使所有内容再次可见。

### Viewing materials in the viewports

Views 菜单还包括几个用于在视口中显示场景细节（如材质、灯光和阴影）的命令。这些选项中的每一个都可能降低刷新率，但它们提供了即时反馈，这通常很有帮助。

贴图也会占用大量内存。Views → Show Materials in Viewport As → Standard Display with Maps 命令会在视口中显示所有应用的贴图。如果你不需要查看贴图，则切换到 Views → Show Materials in Viewport As → Standard Display 将加快显示速度。还有 Hardware Display 和 Hardware Display with Maps 选项，可使用显卡内存来显示应用的纹理。

> **Cross-Ref:** More on applying texture maps is covered in Chapter 17, "Adding Material Details with Maps."

### Displaying lights and shadows in the viewports

视口着色标签菜单中包含用于在视口中启用灯光和阴影效果的选项。

视口着色标签子菜单中的选项默认处于禁用状态，这表示不显示阴影并将灯光数量限制为 8 个。有使用场景灯光或默认灯光照亮场景的选项。视口中阴影不可见，除非启用了硬件着色。视口着色标签菜单中有一个启用硬件着色的选项。你也可以使用 Shift+F3 键盘快捷键启用此选项。启用硬件着色后，你可以打开视口阴影，如图 2.12 所示。

在视口中预览阴影需要使用 Direct3D 驱动程序，并且你的显卡必须支持 Shader Model 2.0（适用于 Good 显示选项）或 Shader Model 3.0（适用于 Best 显示选项）。你可以通过选择 Help → Diagnose Video Hardware 菜单命令来检查可以使用哪种视口着色方法。这会运行一个脚本，并在 MAXScript Listener 窗口中报告其结果，如图 2.13 所示。

> **Note:** If your computer doesn’t support either of these Shader models, then the options will be disabled in the viewport shading label menu and in the Viewport Configuration dialog box.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_101_0.png)

