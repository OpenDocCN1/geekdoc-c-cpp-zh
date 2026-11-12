
- 4. 将以下高亮行添加到 New Activity 类的 onCreate 方法中：

```java
public void onCreate(Bundle icicle){
    super.onCreate(icicle);
    setContentView(R.layout.new_activity);
}
```

setContentView 是用于告诉 Android 为新活动显示哪个 XML 文件的方法。既然你已经创建了新类、字符串和布局文件，现在是时候启动该活动并在屏幕上显示新视图了。

## 捕获按键

启动新活动的一种简单方法是让用户按下其设备上的中央键。如果你的手机没有中央键，你可以轻松修改以下代码以接受你喜欢的任意按键。要监听按键事件，你需要扩展原始活动的 onKeyDown 方法。请记住，这只是一个简单的示例场景。在实际应用中，用户按下单个按键就启动新活动可能并不是很常见的用例，但它可以作为一个很好且简单的示例。大多数新活动是在用户选择列表项、按下按钮或对屏幕执行其他操作时启动的。

你的新版 onKeyDown 应该如下所示：

```java
@Override
public boolean onKeyDown(int keyCode, KeyEvent event){
    if(keyCode == KeyEvent.KEYCODE_DPAD_CENTER){
        //Launch new Activity here!
        return true;
    }
    return super.onKeyDown(keyCode, event);
}
```

通过声明 onKeyDown，你重写了默认的按键处理程序，以便执行特定于你自己活动的操作。如果传入的按键不是你的活动自行处理的内容，将其传递给父类版本的方法总是一个好主意。

注意，当 keyCode 与中央按钮匹配时，你返回 true。通过这种方式，你告诉 Android 活动和视图，该按键已被正确处理，不应再传递给其他任何对象。否则，你允许活动超类处理该按键。现在这似乎不是什么大问题，但随着你的 Android 活动变得越来越复杂，它会变得更加重要。

### 启动活动

最后，是时候启动新活动了。这将开始你对 Intent 的短暂探索。每个新活动都是由于新的 Intent 被分派到系统（系统会处理它并采取适当的操作）而启动的。为了启动第一个活动，你需要一个应用上下文的引用以及新活动的类对象。让我们先创建新的 Intent。

- 1. 将以下代码放入你的 onKeyDown 按键处理方法中：

```java
Intent startIntent=new Intent(
    this.getApplicationContext(),
    NewActivity.class);
```

你正在向新的 Intent 传递应用上下文以及你希望启动的活动的类对象。这告诉 Android 在应用程序包中具体到哪里查找。创建和与 Intent 交互的方式有很多；不过，这是启动新活动最简单的方式。一旦 Intent 被正确构造，接下来只需告诉 Android 系统你想启动新活动即可。

- 2. 将以下行放入你的按键处理方法中：

```java
startActivity(startIntent);
```

![](img/47ad0ac10bf11125744ef22c945d3099_45_0.png)

你的 onKeyDown 处理程序应如下所示：

```java
public boolean onKeyDown(int keyCode, KeyEvent event){
    if(keyCode == KeyEvent.KEYCODE_DPAD_CENTER){
        Intent startIntent=new Intent(this, NewActivity.class);
        startActivity(startIntent);
        return true;
    }
    return super.onKeyDown(keyCode, event);
}
```

> **注意：** 在整个过程中，原始活动从未访问过新活动的实例。这两个活动之间可能传递的任何信息都必须通过中间 Intent 进行。你将在下一节中学习如何做到这一点。

### 试一试

如果你正在运行 Eclipse，并且一直跟着我编写代码，那么现在只需启动模拟器并安装你的新活动即可（你应该还记得第 1 章中的步骤）。一旦新应用程序启动，按下中央键即可看到你所有劳动成果（**图 2.1**）。

既然你知道了如何创建和启动新活动，现在该讨论这个过程是如何工作的了。为了以后进行 UI 布局和数据管理/保留，你需要理解每次你的某个活动进入和离开屏幕时会调用哪些方法。

## 获取 Intent

Intent 可以有无数种形式。

每当你需要启动活动或服务时，都会使用它们。此外，你还会经常使用 Intent 进行系统级通信。例如，你可以通过注册一个广泛发布的 Intent 来接收有关电源系统变化的通知。如果你的某个活动在清单文件中注册了一个 Intent（例如 com.haseman.peachPit.OhOhPickMe），那么只要你将活动设为公开，手机上的任何应用程序都可以通过调用以下代码直接启动到你的活动：

```java
startActivity(new Intent("com.haseman.peachPit.OhOhPickMe"));
```

## 活动的一生

尽早知道每个活动都过着非常短暂但激动人心的一生是件好事。它始于你的活动注册接收的 Intent 被广播到系统时。系统会调用你的活动构造函数（并在必要时启动你的应用程序），然后按以下顺序在活动上调用以下方法：

- 1. onCreate
- 2. onStart
- 3. onResume

当你实现一个活动时，你的工作是扩展构成此生命周期的方法。唯一必须扩展的是 onCreate。其他方法如果你声明了，将按生命周期顺序被调用。

你的活动是顶层可见的应用程序，可以绘制到屏幕、接收按键事件，通常也是聚会的主角。当用户从活动按下返回键时，这些相应的方法将按以下顺序被调用：

- 1. onPause
- 2. onStop
- 3. onDestroy

## 活动短暂而残酷的一生

活动的生命极其短暂。它们不断被创建和销毁，因此非常重要的一点是，不要在其中保存任何与你的活动所控制的屏幕之外有关的数据。

以下都是会导致任何活动被销毁的有效操作：

- 1. 用户将设备从纵向旋转为横向，或反之。
- 2. 活动不再显示在屏幕上，或系统资源不足。
- 3. 今天是星期二。
- 4. 用户按下了返回键或主页键并离开了你的应用程序。

再次强调，确保你的活动的数据成员仅与屏幕上的元素相关。此外，不要指望活动为你保存任何数据。你将在后续章节中学习处理此问题的策略。

这些方法执行完毕后，你的活动将被关闭，并应准备好进行垃圾回收。

为了理解活动的流程，让我们快速详细地查看每个生命周期方法。请记住，你必须在这些方法中调用超类方法（通常在做其他任何事情之前），否则 Android 会向你抛出异常。

> **注意：** `onCreate` 是应用程序生命周期方法中唯一必须实现的方法。在我大多数 Android 工作中，我发现最终只实现其中一两个方法，具体取决于每个活动负责什么。

![](img/47ad0ac10bf11125744ef22c945d3099_47_0.png)

### PUBLIC VOID ONCREATE(BUNDLE ICICLE)

Android 会在你的活动启动时调用你对此方法的声明。然而请记住，在应用程序运行期间，你可能会经历每个活动的多个实例。例如，如果用户将屏幕方向从横向改为纵向，你的活动将被销毁，并且同一活动的新实例将被创建并初始化。

