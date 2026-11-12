

```java
getContentResolver().query(
    MediaStore.Audio.Media.EXTERNAL_CONTENT_URI, null,
    MediaStore.Audio.Media._ID + " = " + id, null, null);
if(mCursor == null)
    return;
if(!mCursor.moveToFirst()){
    mCursor.close();
    mCursor = null;
    return;
}
int pathIDX = mCursor.getColumnIndex(MediaStore.Audio.Media.DATA);
String path = mCursor.getString(pathIDX);
try{
    mPlayer.reset();
    mPlayer.setDataSource(path);
    mPlayer.prepare();
}catch(IOException io){
    Log.e("MediaService", "Unable to set data source",io);
}
```

虽然这段代码稍微有点长，但其中大部分内容应该与你之前完成过的任务类似。

- 1. 我在向内容提供器查询传入方法中的 id。
- 2. 我先通过检查游标是否返回 null（如果 SD 卡被移除，就可能发生这种情况）来确保音乐确实存在。我还会检查游标中是否存在有效的数据行。

## 另一种方式

这里同样值得指出，我选择了两条路线中较为困难的一条。除了向内容提供器查询确切的媒体路径之外，我还可以为所讨论的媒体构建一个 URI，然后把它直接交给播放器。我之所以选择这条可能稍微复杂一点的播放路径，只是为了让你在以后需要获取文件本身时，知道该怎么做。

- 3. 当我确定游标有效并且包含一首可播放歌曲的数据后，我可以重置播放器（以防它已经在播放其他内容），为其设置数据源，并告诉媒体播放器进行准备。这些方法执行完毕后，媒体播放器就可以开始播放了。

至此，当 Activity 调用 play 时，你的服务就已经准备就绪了。

## 播放时间

现在服务已经有了数据源并完成了准备，Activity 就可以调用 play，这将触发以下代码运行：

```java
private void play(){
    if(mPlayer != null){
        mPlayer.start();
        setForegroundState(true);
    }
}
```

你需要启动媒体播放，并确保服务切换到前台运行。setForegroundState 是我在第 6 章中定义的一个方法，它会在通知栏中放置一个图标。如果你需要复习如何将服务置于前台模式，请回顾第 6 章或查看本章的示例代码。

## 天下没有不散的筵席……但愿如此

在某个时刻，音乐必须停止——要么是因为歌曲已经播放完毕，要么是因为用户将其终止。我的示例代码中包含一个 stop 方法，但由于它看起来几乎与我在上一节中列出的 play 方法完全相同，因此这里就不赘述了。然而，因为我希望服务的生命周期能比 Activity 的运行时间更长，所以我需要让服务自行关闭。你可以通过将服务注册为媒体播放器的 OnCompletionListener 来找到关闭服务的合适时机。相关代码行如下所示：

```java
mPlayer.setOnCompletionListener(this);
```

你可以在播放器创建之后的任何时间点调用它。当然，你的服务需要实现 OnCompletionListener 并拥有正确的 onCompletion 方法。

```java
@Override
public void onCompletion(MediaPlayer mp) {
    stopSelf();
}
```

这意味着一旦媒体播放完毕，服务将调用自身的 stop，由于服务的生命周期机制，这将触发 Android 调用服务的 onDestroy 方法——这是进行清理工作的绝佳位置。清理完成后，服务将被释放并停止运行。

## 清理工作

在处理游标和媒体播放器时，清理工作至关重要。如果你没有正确处理这一部分，设备的大量内存可能会在处理过程中丢失。下面是 onDestroy 方法，我在其中同时清理了游标和媒体播放器：

```java
@Override
public void onDestroy(){
    super.onDestroy();
    if(mCursor != null)
        mCursor.close();
    if(mPlayer != null) {
        mPlayer.stop();
        mPlayer.release();
    }
}
```

我必须小心谨慎，因为错误的数据源 ID 或损坏的媒体文件可能会导致这两个指针中的任何一个为 null，那样的话，当我尝试关闭它们时，服务就会很容易崩溃。

## 中断处理

当你在为 Android 设备编写音乐软件时，牢记你软件所运行的硬件实际上是一部手机，这一点至关重要。这意味着你需要留意几件事。

- **音频焦点。** 你需要使用 *AudioManager* 类（Android 2.2 中引入）来注册音频焦点监听器，因为其他应用程序可能会播放提醒、导航指示，或者它们自己的糟糕音乐。这对于让 Android 音乐播放应用与系统其他部分和谐共处至关重要。
- **耳机内置控制键。** 你需要让服务通过清单文件（或在服务启动时的运行时）注册接收耳机按键意图。至少，要设置服务在耳机控制键被点击时暂停播放。
- **电话来电。** 通过 *TelephonyManager* 或音频焦点工具监控电话的通话状态，你*绝对必须*留意来电。手机铃声响起时必须停止所有音频。没有什么比不处理电话来电更能激怒你的用户（并损害你的评分）了。
- **SD 卡缺失。** 你需要确保你的应用能够正确处理 SD 卡缺失或移除的情况。用户可以在任意时间通过 USB 线将外部存储卡挂载为可移动驱动器。如果你监听 ACTION_MEDIA_REMOVED 意图，Android 会向你发出提醒。

这看起来似乎有很多事情需要注意（事实也确实如此），但别担心，Google 的开发者们已经发布了一款开源媒体播放器（随 Android 源码一起提供），它可以作为处理这些问题的极佳指南。一如既往，官方文档中也会有很多关于这个主题的内容。

## 总结

在本章中，我向你展示了如何

- 播放简单的视频
- 按下按钮时播放音效
- 使用之前创建的服务接口，并从中构建一个功能完整的媒体播放器

你现在应该已经熟悉媒体播放的核心要点了。如果你想在视频方面更进一步（我希望你会），你需要研究如何使用控制器来修改视频视图的状态。

扩展媒体播放服务的下一步，是思考如何传递 ID 数组（播放列表），以及如何处理用户动态更新这些播放列表（当用户修改它们时）。

只要你足够细心并认真对待 Android，它可以成为一个非常强大的媒体平台。走出去，制作一大批更好的音乐播放器吧——哪怕只是为了让我自己也能用上。

## 9

## 确定位置并使用地图

![](img/47ad0ac10bf11125744ef22c945d3099_224_0.png)

构建任何移动应用程序的主要好处之一，就是能够向用户提供基于位置的数据。Android 也不例外。利用用户的位置来帮助他们做出明智的决定，这一点应该始终铭记于心。不过，关于确定和使用设备位置的基础知识，还是有一些需要了解的内容。我将向你展示一些快速获取位置的技巧，然后很快向你展示如何显示 Android 内置的 Google 地图视图。

## 寻找好的提供器

使用位置服务的第一步，当然是在添加权限之后，找到一个好的提供器。除了耗时耗电的 GPS 系统之外，每台设备可能还有几种不同的位置服务。Android 允许你为最终使用的提供器指定条件。你可以通过构建一个你希望的功能列表，然后请求 Android 返回最适合你需求的那个提供器来实现这一点。下面是我用 getBestProvider 方法整理的一个比较理想的示例：

```java
private String getBestProvider(LocationManager locationManager){
    Criteria criteria = new Criteria();
    criteria.setAccuracy(Criteria.ACCURACY_COARSE);
    criteria.setPowerRequirement(Criteria.POWER_LOW);
    criteria.setCostAllowed(false);
    return locationManager.getBestProvider(criteria, true);
}
```

在调用 getBestProvider 方法之前，你需要先获取一个 LocationManager 对象，可以通过以下代码实现：

```java
locationManager = (LocationManager)getSystemService
    (Context.LOCATION_SERVICE);
```

通常，我会把这个指针保存在某个地方，这样以后就再也不需要重新查找了。

## 获取数据

一旦你收到了理想提供器的字符串 ID，就可以注册并开始从该提供器接收位置更新。以下是注册更新的代码：

```java
locationManager.requestLocationUpdates(provider, 60000, 1000, this);
```

