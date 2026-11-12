

```java
Intent i = new Intent(this, ImageIntentService.class);
i.putExtra("url", getIntent().getExtras().getString("url"));
startService(i);
pd = ProgressDialog.show(this, "Fetching Image", "Go intent service go!");
}
```

这段代码注册了一个接收器（这样你就能在下载完成后采取行动），启动了服务，最后向用户显示了一个加载对话框。

现在来看看 imageReceiver 类是什么样子：

```java
private BroadcastReceiver imageReceiver = new BroadcastReceiver() {
    @Override
    public void onReceive(Context context, Intent intent) {
        String location = intent.getExtras().getString("location");
        if (location == null || location.length() == 0) {
            Toast.makeText(context, "Failed to download image",
                    Toast.LENGTH_LONG).show();
        }
        File imageFile = new File(location);
        if (!imageFile.exists()) {
            pd.dismiss();
            Toast.makeText(context,
                    "Unable to Download file :-( ",
                    Toast.LENGTH_LONG).show();
            return;
        }
        Bitmap b = BitmapFactory.decodeFile(location);
        ImageView iv = (ImageView) findViewById(R.id.remote_image);
        iv.setImageBitmap(b);
        pd.dismiss();
    }
};
```

这是 BroadcastReceiver 类的自定义扩展。为了正确处理来自 IntentService 的事件，你需要在 Activity 中声明它。目前，这段代码有两个问题。看看你能否识别出来。

首先，你需要从 intent 中提取文件位置。你通过查找 "location" extra 来完成这一点。一旦确认这确实是一个有效文件，你就会把它传给 BitmapFactory，它会为你创建图像。然后这个位图可以传给 ImageView 进行渲染。

现在说说做错的地方（如果还没发现，就先别往下读。不许作弊！）。首先，代码没有检查 intent service 广播的完成 intent 是否正对应最初请求的图像（请记住，一个服务可以处理来自任意数量 Activity 的请求）。

其次，位图是从 SD 卡加载的……而且是在主线程上！这正是我一直警告你千万不要做的事情之一。

### 检查你的工作

在较新版本的 SDK 工具中，Android 提供了一种方法来检查你的应用是否违反规则并在主线程上运行缓慢任务。你可以在任何 Activity 中调用 StrictMode.enableDefaults，当系统发现主线程违规时，它就会开始抛出警告。StrictMode 有许多不同的配置和设置，但启用默认值并尽可能清理错误，会显著提升应用速度。

### 加载器

Loader 是一个新类，在 Honeycomb 和 Android Compatibility 库中都有提供。遗憾的是，本章没有足够篇幅详细介绍它，但我要说，如果你必须反复在主线程之外执行繁重任务，它是一个非常值得探索的优秀工具。它和 AsyncTask 一样，通常绑定到 Activity，但它更适合处理单个任务必须执行多次的情况。它非常适合加载游标（使用 CursorLoader 子类）以及其他任务，比如为 ListView 下载各个列表项。请查阅文档，了解如何最好地使用这个强大而新颖的类。

关于如何加载数据，大致就讲这些。请记住，从 SD 卡加载、网络事务以及较长的处理任务都必须在主线程之外执行，否则你的应用和用户都会遭殃。正如我在本章所示，你可以使用简单线程、AsyncTask 或 IntentService 来检索和处理数据。但也要记住，任何修改屏幕上视图或对象的操作都必须在主线程上执行（否则 Android 会向你抛出愤怒的异常）。

此外，请记住，这三种方法只是许多可能的后台数据获取模式中的少数几种。Loaders、Workers 和 ThreadPools 都是其他替代方案，可能比我所给的示例更适合你的应用。

遵循我在这里概述的简单规则，你的应用就会快速、对用户响应及时，并避免可怕的 App Not Responding 厄运通知。正确使用并避开主线程对于打造成功的应用至关重要。

如果你更感兴趣的是用来自远程源的复杂数据构建列表，下一章应该正好能给你想要的内容。我将向你展示如何把 Twitter 消息列表渲染到屏幕上的菜单中。

最后给你一个挑战：启用 Android 的严格模式，并把我在本章示例代码中留下的那些小文件访问操作移到主线程之外。这应该是一种好方法，让你在自行处理之前熟悉这个过程。

## 5 适配器、ListView 和列表

![](img/47ad0ac10bf11125744ef22c945d3099_140_0.png)

在 Android 中，列表是向用户展示数据最常用的工具之一。从游戏的入口菜单到动态的 Facebook 状态或 Twitter 消息列表，列表无处不在。Android 处理列表的系统起初虽然复杂，但一旦开始使用就会变得容易得多。在本章中，我将涵盖从简单的静态主菜单列表到由远程数据支持的动态自定义 Twitter 信息流列表元素。在此过程中，我将带你了解 Android 最常用且最复杂的 UI 视图之一的内部工作原理。

### 每个列表的两个组成部分

要在 Android 中显示有序数据的列表，你需要处理两个主要组件。

### ListView

首先，你需要一个 ListView 来显示内容。这个视图的职责就是显示信息。它可以添加到任何屏幕布局中，或者你可以使用 Android 的 ListActivity 或 ListFragment 来替你处理一些组织工作。如果你的屏幕主要设计为以列表形式向用户展示一组数据，我强烈建议你使用 ListActivity 及其同类 ListFragment。

### Adapter

你需要处理的第二个主要类是 Adapter。这个对象会一次一点地把各个视图提供给 ListView。它还负责填充和配置要放入 ListView 的各个行。Adapter 的子类多如大海中的水滴（好吧，也许略少一些），它们覆盖了各种数据类型——从静态字符串列表（ArrayAdapters）到更动态的列表（CursorAdapters）。你可以扩展自己的 adapter（我会在本章后半部分展示）。现在，让我向你展示如何用 ListView 创建一个简单的主菜单。

和往常一样，你可以跟着我在 Peachpit.com/androiddevelopment/design 上发布的示例代码操作，或者打开你的 IDE 完成我概述的任务。

### 主菜单

主菜单可以采取多种形式。从游戏到音乐应用，它们都提供了进入整个应用的顶层导航。

作为一个令人愉快的副作用，它们也是向你介绍列表工作原理的好方法。我将为资源管理器创建一个字符串数组，把它提供给数组适配器，再把该数组适配器插入由列表 Activity 包含的列表视图中。都明白了吗？处理列表时有很多动态部分需要整合，所以我会慢慢地、一步一步地讲。

### 创建菜单数据

菜单必须有内容可显示，因此你需要创建一个要显示的字符串列表。还记得那一章吗？你学到所有要显示的字符串常量都*应该*放入 res/values/strings.xml 文件。巧合的是，字符串数组也放入同一个文件，但语法略有不同。我已将以下内容添加到我的 res/values/strings.xml 文件中：

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <!--The rest of the app's strings here-->
    <string name="app_name">List Example</string>
    <string name="main_menu">Main Menu</string>
    <string-array name="menu_entries">
        <item>Menu Item One</item>
        <item>Menu Item Two</item>
        <item>Menu Item Three</item>
    </string-array>
</resources>
```

这次不是在一个 string 标签内定义每个常量，而是声明一个带名称的字符串数组，然后其中的每个元素都可以在一个 item 标签内定义。既然有了数据，现在该创建一个 Activity 来容纳它了。

