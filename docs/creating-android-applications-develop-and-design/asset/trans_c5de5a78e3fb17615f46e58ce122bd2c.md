
## 限制应用仅可在能够正常工作的设备上访问

你的 Android 应用在许多情况下可能需要某些非常特定的硬件才能正常工作。试想，用户把相机应用下载到没有相机的设备上，体验会非常糟糕。

### `<uses-feature>` 标签

Android 提供了一种途径，让你可以告诉应用市场应允许哪些设备下载和购买你的应用。这通过 `AndroidManifest.xml` 文件中的 `<uses-feature>` 标签完成。

例如，如果你的应用要求设备配备相机，就应该在清单文件中添加以下行：

```xml
<uses-feature android:name="android.hardware.camera"
              android:required="true"/>
```

这一行告诉 Android，该应用不应安装在没有相机的设备上，因为相机是正确运行所必需的。反过来说，你也可以声明应用会使用某项特定硬件，但在该硬件不存在时进行适当的降级。图像编辑应用可能想使用相机，但如果设备没有相机，它仍可通过修改从网络保存到设备内置图库中的图像来运行。你可以通过将该硬件声明为使用中、但把要求设置为 false 来告诉系统这一点：

```xml
<uses-feature android:name="android.hardware.camera"
              android:required="false"/>
```

你可以设置大量硬件特性。最好查阅文档以获取完整列表（http://developer.android.com/guide/topics/manifest/uses-feature-element.html）。

### SDK 版本号

你还可以声明应用支持哪些 SDK 版本。为此，需要在清单文件中声明 `<uses-sdk>`。事实上，如果你使用 Eclipse 或 Android 命令行工具创建项目，就已经有一个基本声明：

```xml
<uses-sdk android:minSdkVersion="10" />
```

如果你依赖的某些类或对象在旧设备上不可用，可以添加支持的最小和最大 SDK。不过，你也可以用如下声明同时屏蔽较旧和较新的 SDK 版本：

```xml
<uses-sdk
    android:maxSdkVersion="10"
    android:minSdkVersion="6" />
```

这会告诉 Android Market 仅对 SDK 6（Android 2.0.1 更新 1）及以上的设备列出相关应用。它还会阻止高于 Gingerbread 的设备运行你的软件。此外，如果你尝试通过网页链接加载该应用，下载器会以应用不受支持为由阻止安装。

值得一提的是，这种强硬屏蔽确实应当作为最后手段。如果你能让应用在最新和最旧的设备上都良好运行，就应该这样做。通过这种声明，你可以限制谁被允许安装你的应用。

## 用反射化解烦恼

解决这个问题——以及所有涉及较晚版本才声明的 SDK 方法的问题——的办法是使用反射来访问它们。反射允许你在代码中不显式定义或包含某些 Java 方法的情况下使用它们。它非常适合处理这类情况。

理想情况下，如果 `apply` 可用（SDK 9 及更高版本），我希望调用 `apply`；但如果 `apply` 会引发问题，就回退到 `commit`。下面正是这样做的 `setUsername` 新版本：

```java
public void setUsername(String username){
    SharedPreferences prefs =
        PreferenceManager.getDefaultSharedPreferences(this);
    Editor ed = prefs.edit();
    ed.putString("username", username);
    try{
        Method applyMethod =
            Editor.class.getDeclaredMethod("apply",
                new Class[]{});
        if(applyMethod != null)
            applyMethod.invoke(ed, new Object[]{});
        else
            ed.commit();
    }catch(Exception error){
        ed.commit();
    }
}
```

虽然这个方法开头与之前的方法相同——获取 `Editor` 并用它保存字符串——但在真正保存用户名时，做法就不同了。

反射可能抛出几种不同的错误（需要重点留意的是 `NotFoundException`），因此反射调用需要包在 try-catch 块中。我首先从 `Editor` 类请求 `apply` 方法。如果拿到了它（并且它不为 null、不抛出异常，而且月相也正好合适），我就能调用它（同样通过反射调用），然后大功告成。如果它不属于 `SharedPreferences.Editor` 类的一部分而未被找到，我就会回退到调用 `commit`。反射让我可以定义并使用那些可能未编译进早期 SDK 版本的方法。

### 始终关注 API 级别

在 Android 文档中，每个类和方法右侧都有一个小灰色标签，写着“Since: API Level #”。如果该数字高于你希望支持的系统版本，你可能需要重新评估是否使用该类或方法。

反射让你可以两全其美。你可以在支持这些最新方法的较新设备上使用它们，而在不支持的设备上优雅降级。

不过要记住，反射速度较慢且可能容易出错，因此要少用并谨慎使用。如果你要频繁使用某个具有两种不同实现的类或方法（例如 `Contacts`），请考虑改用条件式类加载。也就是说，为每个版本的类编写两个 `Adapter` 类（一个用于旧版本，一个用于新版本），并使用受支持的那一个。你始终可以通过检查 `android.os.Build.Version.SDK` 来查明设备运行的是哪个 SDK。

## 小结

在本章中，你学习了如何处理屏幕分辨率、密度和配置方面的差异。你通过高级使用布局文件夹、`<include>` 标签以及 Android 的 XML 布局系统做到了这一点。然后，你学习了如何通过在清单文件中放置声明来告诉 Android 你需要哪些设备特性。最后，你学习了如何使用反射：在高级方法可用时利用它们，在不可用时避开它们。

有了所有这些工具，你应该已经准备好将你的杀手级移动应用带到 Android 平台上海量的设备上——从冰箱到手机再到电视——大展身手。

无论如何，单调乏味令人厌倦。不同的设备带来创新、更多用户选择，以及样子滑稽的屏幕保护膜。既然你已经具备处理这些情况的能力，就能轻松缩放资源并自如驾驭横屏模式。

## 8 电影与音乐

![](img/47ad0ac10bf11125744ef22c945d3099_202_0.png)

希望音频和视觉媒体支持会成为你下一个沉浸式 Android 应用的重要组成部分。这两个行业都正迎来重塑的时机，而下一场媒体格式革命几乎必然会涉及移动设备。为此，本章将带你入门 Android 视频和音乐库的基础知识。我还会指出，在构建后台媒体播放服务时需要了解的几件事：电影、音乐播放、后台服务以及需要注意的事项。

### 电影

在 Android 设备上播放电影归根结底要用 `VideoView` 类。本节中，我会使用一个简单示例应用，依次播放手机 SD 卡上保存的每个视频。总体流程如下：

- 我会使用 `ContentProvider`（你应该还记得第 6 章中上传最新照片时我们简要讨论过它）来请求保存到用户外部存储卡上的每个视频。
- 在用 `Cursor`（Android 的查询结果数据对象）加载设备上的所有视频后，我需要一个方法来播放下一个视频。
- 我会将一个 activity 设置为监听器，这样当视频播放完成时，我就可以调用 `playNextVideo` 方法，继续播放游标中的下一个视频。
- 最后，当用户离开播放屏幕时，我会清理游标。

不过，在做这些事情之前，我需要先在主布局中放置一个 `VideoView` 来使用。

### 添加 VideoView

将 `VideoView` 放到屏幕上，就像把它添加到 XML 布局中一样简单。现在我的 `main.xml` 文件如下所示：

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    >
    <VideoView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:id="@+id/my_video_view"
        />
</LinearLayout>
```
