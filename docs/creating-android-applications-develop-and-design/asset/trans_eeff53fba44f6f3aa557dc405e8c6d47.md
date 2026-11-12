
## 记住主线程！

仅仅因为你在一个服务中运行，并不意味着你就脱离了主线程！服务的 `onCreate` 方法会在主线程上被调用。如果你需要执行任何繁重的工作，可以考虑使用 `AsyncTask` 或 `Handler+Looper` 模式，或者不要使用普通服务，而是使用 `IntentService` 在主线程之外处理繁重数据。此外，某些操作（例如录制音频）只能从主线程发起。现在是上午10点，你知道你的线程都在哪里吗？

## 保持服务运行

`startForeground` 方法是你与 Android 达成巧妙交易的机会。系统同意，在你调用此方法之后、直到你调用 `stopForeground` 之前，它不会杀死你的服务。作为交换，你必须通过传入一个 `Notification` 对象，向用户提供要显示在顶部栏中的图标和视图。这个契约允许长时间运行、必不可少且密集型服务（例如音乐播放或照片上传）运行而不必担心被终止。同时，用户也能知道为什么他们的手机可能有点卡顿。

## 关闭它！

某个时刻，聚会终将结束，该清理了。这可能是因为你的服务调用了 `stopSelf`，或者因为另一个组件调用了 `Context.stopService`。以下是生命周期中的销毁部分：

- `onDestroy` 是你取消任何正在运行的任务并释放你占用的任何资源（例如媒体或网络任务）的机会。这也是你注销任何为监视新媒体而设置的 `BroadcastReceivers` 或 `ContentObservers` 的机会。

如果你期待一个多步骤的关闭过程，恐怕你会失望。因为服务没有位于屏幕顶层的概念，所以无需暂停、恢复，或执行活动必须支持的任何其他复杂交互。

与服务通信主要有两种方式：意图广播和绑定器接口。我将向你展示两者的示例，并在此过程中让你看到服务的两个实用任务。事实上，与服务通信的方式还有很多。但根据我的经验，这是两种最有用的方式。一如既往，如果这两种方法都不太适合你，请查阅文档。

## 基于意图的通信

想象两个在不同房间的工人，他们只能通过电子邮件相互通信。这些电子邮件可以包含附件和其他数据。这两个工人必须仅使用这一种通信方式度过一天。正如你可能想象的那样，只要他们不必彼此说太多话，这可以是一种高效且实用的方式来完成大量事情。

在某种意义上，这正是与服务进行*基于意图的通信*在现实生活中的样子。服务通过意图启动；当它完成任务或等待的事情发生时，它会发送一个广播意图，提醒任何监听者某个特定任务已完成。你在第4章看到过一个例子，当时我使用意图服务下载图像。让我再给你展示一个。

下面的例子是我能以这种印刷形式给出的基于意图的通信的最佳示例之一。我将创建一个新服务所需的所有部分，该服务在前台运行并带有通知。我使用 Android 的 ContentProvider 来监听并获取新拍摄照片的位置。这段代码会在拍摄任何新照片时提醒你，无论使用哪个应用程序拍摄。至于你如何处理照片，我留给你无限的想象力。

## 自动上传图片

Google+ Android 应用我最喜欢的功能之一是它能够在后台自动上传照片。事实证明，借助 ContentProvider、Service 和 ContentObserver，你可以在自己的应用中轻松实现这一点。我的示例服务将启动，将自己置于前台，并在拍摄新照片时触发广播意图。在你自己的代码中，你可以上传图像或采取任意数量的其他操作。使用这种技术将涉及以下一般步骤。

- 1. 声明服务。
- 2. 获取一个服务。
- 3. 启动服务。
- 4. 初始化服务。
- 5. 转到前台。
- 6. 观察内容变化。

让我们开始吧。

### 声明服务

你必须告诉 Android 在哪里找到该服务。

如你所知，每个服务都必须在清单中声明。你可以为它添加一个意图过滤器来响应（如果你希望除自己之外的应用也能启动它）。对于我的示例，这没有必要，但以后可能是你需要利用的东西。以下是需要在清单中放置的单行：

```xml
<service android:name="PhotoListenerService"/>
```

### 获取一个服务

现在创建扩展 Service 的类。

```java
public class PhotoListenerService extends Service {
    @Override
    public IBinder onBind(Intent intent) {
        return null;
    }
}
```

由于 `onBind` 是 `Service` 类的必需方法，它必须在我的类中，否则无法编译。现在你已经有了一个服务，让我们看看如何实际启动它。

- 2. 完成这些后，你现在可以编写代码来启动和停止照片监听服务。更新后的 ServiceExampleActivity 现在如下所示：

```java
public class ServiceExampleActivity extends Activity
        implements OnClickListener {
    /** Called when the activity is first created. */
    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);
        Button btn = (Button)findViewById(R.id.start_service);
        btn.setOnClickListener(this);
        btn = (Button)findViewById(R.id.stop_service);
        btn.setOnClickListener(this);
    }
}
```

这段清单没有什么惊天动地的内容。我在视图构建完成后获取对它们的引用。我将我的类设置为实现 `OnClickListener` 接口，这允许我将活动本身设置为两个按钮的点击监听器。上面的代码在你实现 `View.onClick` 之前无法编译。

- 3. 实现 `onClick` 方法：

```java
@Override
public void onClick(View v) {
    Intent serviceIntent = new Intent(getApplicationContext(),
            PhotoListenerService.class);
    if(v.getId() == R.id.start_service){
        startService(serviceIntent);
    }
    else if(v.getId() == R.id.stop_service){
        stopService(serviceIntent);
    }
}
```

这同样非常简单。按钮被点击时将调用此 `onClick` 方法。根据实际获得点击的视图，我将启动或停止服务。

### 启动服务

现在，如果你按原样运行代码，你会按下按钮，服务会启动，然后……什么也不会发生。让我向你展示如何改变这一点。

我希望每当有人用设备的相机拍照时，系统都会通知我。为此，你需要向 Android 的媒体 ContentProvider 注册一个观察者。切换回 `PhotoListenerService.java` 文件，在服务的 `onCreate` 方法中注册媒体通知：

```java
@Override
public void onCreate(){
    super.onCreate();
    getContentResolver().
    registerContentObserver(
        MediaStore.Images.Media.EXTERNAL_CONTENT_URI,
        true,
        observer);
}
```

要注册内容观察者，我需要提供一个统一资源标识符（URI）。在这种情况下，我将使用外部 SD 卡上保存的所有照片的常量 URI。这个常量在 MediaStore 中声明。第二个参数是我告诉 Android，我想知道该 URI 的子项何时被修改。我将其设置为 true，因为我想知道图像 URI 的任何后代何时被修改、添加或删除。最后，我传入我的观察者。这个对象的 `onChange` 方法将在 ContentProvider 更新时被调用。它将注册媒体更新，但你还需要定义另一个方法。

### 转到前台

将服务带到前台可以保护它免于在资源不足时被 Android 杀死。

按如下方式实现服务的 `onStartCommand` 方法。

```java
public int onStartCommand(Intent intent, int flags, int startId) {
    super.onStartCommand(intent, flags, startId);
    lastUpdateTime = System.currentTimeMillis();
    setForegroundState(true);
    return Service.START_STICKY;
}
```

我将记录服务启动的时间（稍后会详细说明为什么这很重要）。最后，我返回 `Service.START_STICKY`，这告诉系统，如果服务因内存或性能原因被终止，我希望它重新启动。

我需要编写一个函数来处理创建通知并将服务移到前台。`setForegroundState` 是我自己的方法，负责将服务置于前台模式以及从服务移出前台模式。

```java
private void setForegroundState(boolean enable){
    if(enable){
        Notification n = new Notification(
            R.drawable.icon,
            "Service is uploading all your photos",
                System.currentTimeMillis());
        n.contentView = new RemoteViews(
```
