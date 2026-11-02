
![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_708_0.png)

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_708_1.png)

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_708_2.png)

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_708_3.png)

图 B-1 ExtendedSplashScreen1 示例的四个阶段：（1）默认启动画面，左上，（2）动画显示徽标和标题，右上，（3）显示进度指示器，左下，（4）淡出扩展启动画面以显示主页面，右下。屏幕左上角的 10 秒倒计时模拟初始化工作。

在第二个 div 中，由于它最后声明，所以覆盖在第一个之上，counter 元素显示倒计时用于调试目的，但你可以想象这样的计数器变成一个确定性进度条或类似控件。其余元素提供图像和进度环。但在我们了解更多关于屏幕大小之前，我们无法在 CSS 中定位这些元素。我们能做的最好的事情就是将 splashScreen 元素设置为用背景色填充屏幕，并将其他元素的 position 样式设置为 absolute，以便我们可以从代码中设置其确切位置。这在 default.css 中完成：

```
#splashScreen {
  background: #825000; /* Matches the splash screen color in the manifest */
  width: 100%;        /* Cover the whole display area */
  height: 100%;
}

#splashScreen #counter {
  margin: 10px;
  font-size: 20px;
}

#splashScreen #logo {
  position: absolute;
}

#splashScreen #title {
  position: absolute;
}
```

```
#splashScreen #progress {
    position: absolute;
    color: #fc2; /* use a gold ring instead of default purple */
}
```

现在在 default.js 中，我们声明了一些模块级变量用于启动画面元素，外加两个值来控制扩展启动画面的显示时长（模拟初始化工作）以及一个指示何时显示进度环的值：

```
var app = WinJS.Application;
var activation = Windows.ApplicationModel.Activation;

var ssDiv = null;        //Splash screen overlay div
var logo = null;         //Child elements
var title = null;
var progress = null;

var initSeconds = 10;    //Length in seconds to simulate loading
var showProgressAfter = 4; //When to show the progress control in the countdown
var splashScreen = null;
```

在 activated 事件处理程序中，我们现在可以根据 args.detail.splashScreen.imageLocation 属性来定位所有内容（注意有关 WinJS.UI.processAll 和 setPromise 的注释，我们在这里不使用）：

```
app.onactivated = function (args) {
    if (args.detail.kind === activation.ActivationKind.launch) {
        //WinJS.UI.processAll is needed ONLY if you have WinJS controls on the extended
        //splash screen, otherwise you can skip the call to setPromise, as we're doing here.
        //args.setPromise(WinJS.UI.processAll());

        ssDiv = document.getElementById("splashScreen");
        splashScreen = args.detail.splashScreen;    //Need this for later
        var loc = splashScreen.imageLocation;

        //Set initial placement of the logo to match the default start screen
        logo = ssDiv.querySelector("#logo");
        logo.style.left = loc.x + "px";
        logo.style.top = loc.y + "px";

        //Place the title graphic offscreen to the right so we can animate it in
        title = ssDiv.querySelector("#title");
        title.style.left = ssDiv.clientWidth + "px";  //Just off to the right
        title.style.top = loc.y + "px";               //Same height as the logo

        //Center the progress indicator below the graphic and initially hide it
        progress = ssDiv.querySelector("#progress");
        progress.style.left = (loc.x + loc.width / 2 - progress.clientWidth / 2) + "px";
        progress.style.top = (loc.y + loc.height + progress.clientHeight / 4) + "px";
        progress.style.display = "none";

        //Start countdown to simulate initialization
        countDown();
        };
```

此时，显示仍然完全像图 B-1 的左上部分，只是它是我们的扩展启动画面页面而不是默认的启动画面。因此，我们可以在此时从 activated 处理程序返回（或完成延迟），用户不会看到任何变化，但现在我们可以在应用加载时做一些更具视觉吸引力和信息性的事情。

模拟初始化工作并为动画徽标和标题留出时间，我使用一秒 setTimeout 调用实现了一个简单的倒计时器：

```
function countDown() {
    if (initSeconds == 0) {
        showMainPage();
    } else {
        document.getElementById("counter").innerText = initSeconds;

        if (--showProgressAfter) {
            progress.style.display = "";
        }

        initSeconds--;
        setTimeout(countDown, 1000);
    }
}
```

注意我们如何在（伪造的）初始化完成后显示主页面，以及先前定位（但隐藏）的进度环如何在指定秒数后显示。你可以在图 B-1 的左下看到进度环。

为了从扩展启动画面淡出到主页面（图 B-1 右下显示了部分淡出），showMainPage 函数使用 WinJS Animations 库，如下所示，其中 `WinJS.UI.Animation.fadeOut` 接受受影响元素的数组。FadeOut 返回一个 promise，因此我们可以附加一个完成处理程序来知道何时隐藏现在不可见的覆盖 div，我们可以将其从 DOM 中移除以释放内存：

```
function showMainPage() {
    //Hide the progress control, fade out the rest, and remove the overlay
    //div from the DOM when it's all done.
    progress.style.display = "none";
    var promise = WinJS.UI.Animation.fadeOut([ssDiv, logo, title]);

    promise.done(function () {
        ssDiv.removeNode(true);
        splashScreen.ondismissed = null; //Clean up any closures for this WinRT event
    });
}
```

请参阅第 14 章“Purposeful Animations”，了解动画库的详细信息。需要始终牢记的一个细节是，当动画仅影响 transform 和 opacity 属性时，动画在 GPU（图形处理单元）中运行；动画化其他任何内容将在 CPU 上运行，通常性能较差。

为了完成体验，我们现在想要添加一些动画，将徽标向左平移并旋转，并将标题图形从屏幕右侧的初始位置滑入。开始这些动画的正确时间是当 args.detail.splashScreen.ondismissed 事件被触发时，就像我在 activated 中在调用我的 countDown 函数之前所做的那样。此 dismissed 事件处理程序只需计算徽标和标题的平移量，并使用辅助函数 WinJS.UI.executeTransition 为两者设置 CSS 过渡：

```
//Start our animations when the default splash screen is dismissed
splashScreen.ondismissed = function () {
    var logoImageWidth = 300;    //Logo is 620px wide, but image is only 300 in the middle
    var logoBlankSide = 160;     //That leaves 160px to either side

    //Calculate the width of logo image + separator + title. This is what we want to end
    //up being centered on the screen.
    var separator = 40;
    var combinedWidth = logoImageWidth + separator + title.clientWidth;

    //Final X position of the logo is screen center - half the combined width - blank
    //area. The (negative) translation is this position minus the starting point (loc.x)
    var logoFinalX = ((ssDiv.clientWidth - combinedWidth) / 2) - logoBlankSide;
    var logoXTranslate = logoFinalX - loc.x;

    //Final X position of the title is screen center + half combined width - title width.
    //The (negative) translation is this position minus the starting point (screen width)
    var titleFinalX = ((ssDiv.clientWidth + combinedWidth) / 2) - title.clientWidth;
    var titleXTranslate = titleFinalX - ssDiv.clientWidth;

    //Spin the logo at the same time we translate it
    WinJS.UI.executeTransition(logo, {
        property: "transform", delay: 0, duration: 2000, timing: "ease",
        to: "translateX(" + logoXTranslate + "px) rotate(360deg)"
    });

    //Ease in the title after the logo is already moving (750ms delay)
    WinJS.UI.executeTransition(title, {
        property: "transform", delay: 750, duration: 1250, timing: "ease",
        to: "translateX(" + titleXTranslate + "px)"
    });
}
```

这带我们从图 B-1 的左上部分经过右上阶段，到达左下阶段。当然，要真正欣赏效果，只需运行示例！

此代码结构可能与你在自己的应用中需要的类似，只是使用单个 setTimeout 调用延迟显示进度控件，用你的真实异步初始化工作替换 countDown 例程，并设置特定于你的启动画面的元素和动画
