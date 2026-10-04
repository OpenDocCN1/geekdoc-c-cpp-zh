
接下来是名为 `gen` 的目录。主类文件是 `R.java`，它是基于 `activity_main.xml`、`strings.xml` 等文件生成的。之后是 `res` 目录，它代表资源。`res` 目录下包含 `drawable`、`layout` 和 `values` 子目录。`drawable` 包含图形，`layout` 包含布局。

![](img/cbb97d4daaabf800d0384cb0ef181aa8_36_0.png)

包资源管理器。

来源：Eclipse 基金会。

最后，我们是 `AndroidManifest.xml` 文件。你可以将此文件视为应用程序的“说明书”。它包含了权限声明、版本号等信息。在打包应用程序时，你应该确保正确地构造它。

立即知道问题所在，将鼠标指针悬停在红色圆圈或正方形上（某些错误的情况下）片刻，就会出现错误的解释。

最后一种错误是运行时错误（run-time error），它是最令人沮丧的。因为这种错误发生在应用程序运行时，而在编译时没有任何指示表明有错误。运行时错误会在应用程序运行时的模拟器中出现，通常如图 2.7 所示。

![](img/cbb97d4daaabf800d0384cb0ef181aa8_38_0.png)

模拟器中的运行时错误指示。

来源：The Eclipse Foundation。

此外，由于运行时错误的性质，它们并不是每次运行模拟器都会发生。与语法错误不同，当运行时错误发生时，模拟器不会提供解释。这确实令人沮丧！这就是 Eclipse 中的 Debug 视图（Debug perspective）帮助最大的地方。

图 2.7 中的错误是以下应用代码的结果。

```java
package com.sheushi.Debugging;

import android.app.Activity;
import android.os.Bundle;

public class DebuggingActivity extends Activity {

    /** Called when the activity is first created. */

    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(R.layout.main);

        int bogus[] = new int[5];

        for (int ct = 0; ct <= 5; ct++) {
            bogus[ct] = ct;
        }
    }
}
```

仔细检查发现我们导致了一个未检查的 Java 异常：`ArrayIndexOutOfBoundsException`。Java 程序员对异常处理非常熟悉。要查看 Eclipse 中的 Debug 视图，选择 Window 菜单下的 View Perspective，然后选择 Debug。你会看到一个与 2.8 类似的屏幕。

![](img/cbb97d4daaabf800d0384cb0ef181aa8_39_0.png)

Eclipse Debug 视图。

来源：The Eclipse Foundation。

在右下角有一个标记为 LogCat 选项卡的面板。这是检查错误来源的第一地方。任何红色的文本都是你应该检查的内容。查看 2.9 中的放大图。

注意由 `java.lang.ArrayIndexOutOfBoundsException` 引起的行。这就是我们的问题。现在我们知道在代码中要寻找什么来修复问题了。让我们回去使用 try-catch 块修复该问题。在 catch 块中，我们将打印一些诊断信息。注意，我们不能在移动应用程序上使用典型的 `printStackTrace()` 来帮助自己。相反，我们可以使用 logger。注意以下代码中的变化。

| pid | Tag | Message |
|---|---|---|
| 296 | AndroidRuntime | at android.internal zygote main(Zygote.java:62) |
| 296 | AndroidRuntime | at delvik system.NativeStart main(Native Method) |
| 296 | AndroidRuntime | Caused by java.lang IndexOutOfBoundsException |
| 296 | AndroidRuntime | at sheushi Debugging DebuggingActivity.onCreate |
| 296 | AndroidRuntime | at android app Instrumentation.onCreate(Instrument |
| 296 | AndroidRuntime | at android app ActivityThread performLaunchActivity(Activity| |
| 0 | ActivityManager | 11 more |
| 226 | MediaProvider | Force finishing activity sheushi Debugging/ DebuggingActivity |
| | | //sdcard volume ID 452804882 |

Eclipse LogCat 面板。

```java
package android.app.Activity;

import android.os.Bundle;
import android.util.Log;

public class DebuggingActivity extends Activity {

    /** Called when the activity is first created. */

    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);

        int bogus[] = new int[5];

        try {
            bogus[ct] = ct;
        } catch (ArrayIndexOutOfBoundsException aioe) {
            String err;
            if (aioe.getMessage() == null)
                err = "Outran Array";
            else
                err = aioe.getMessage();
            Log.i("Error Here", err);
        }
    }
}
```

你看到我们添加了 try-catch、一个 Log 语句以及额外的 import 语句以在我们的命名空间中包含 android 类。try-catch 允许应用程序运行，但如果我们再次查看调试屏幕，会发现图 2.10 中的 LogCat 部分。

![](img/cbb97d4daaabf800d0384cb0ef181aa8_41_0.png)

显示我们消息的 Eclipse LogCat 面板。

来源：The Eclipse。

在 tag 栏下，我们看到了 Error Here，这里的 tag 是在 `Log.i()` 方法调用中作为第一个参数指定的，以及我们指定的消息。如果异常有消息要打印，它将会出现。（注：文本在此处继续或结束）。

```xml
android:title="Do Something Else"/>

<item android:id="@id/close"
    android:icon="@drawable/icon"
    android:title="Close"/>

</menu>
```

最后，接下来是清单文件和实际 Activity 代码。

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.sheusi.MenuStuff"
    android:versionCode="1"
    android:versionName="1.0">
    <uses-sdk android:minSdkVersion="8"
        android:targetSdkVersion="8"/>
    <application android:icon="@drawable/icon"
        android:label="@string/app_name">
        <activity android:name=".MenuWerx"
            android:label="@string/app_name">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
        </activity>
    </application>
</manifest>
```

最后，这是主 Activity 的 Java 代码。

```java
package com.sheusi.MenuStuff;

import android.app.Activity;
import android.os.Bundle;
import android.view.Inflater;
import android.view.MenuItem;

public class MenuWerx extends Activity {

    /** 当 activity 首次创建时调用。 */

    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        MenuInflater inflater = getLayoutInflater();
        inflater.inflate(R.menu.mymenu, menu);
        return super.onCreateOptionsMenu(menu);
    }

    @Override
    public boolean onOptionsItemSelected(MenuItem mi) {
        if (mi.getItemId() == R.id.dummy) {
            // 无操作
            return true;
        }
        if (mi.getItemId() == R.id.anotherdummy) {
            // 再次无操作
            return true;
        }
        if (mi.getItemId() == R.id.close) {
            this.finish();
            return true;
        }
        return true;
    }

    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);
    }
}
```

注意清单文件中的目标 SDK 和最小 SDK 版本都是 8，而代码指定了 Android 2.2 为目标环境。通过阅读代码，你会发现唯一一个产生实际作用的菜单按钮是关闭（Close）按钮。通过阅读 `menu.xml` 文件，你可能注意到菜单选项上的图像是默认图标。例如，程序员可以指定任何他选择的其它图像。图 2.12 是应用程序在配置为 Android 2.2 的模拟器上运行的图像。

在 Android 3.0 设备上在不更改代码、XML 或清单文件的情况下运行相同的应用程序，看起来将如图 2.13 所示。显示的图像了菜单按钮（屏幕左下角的第四个图像，一个网格形状的对象）以及横跨屏幕底部的打开菜单。

接下来，我们将清单文件中的目标 SDK 版本更改为 11，对应于 Android 3.0。我们将最小 SDK 保持为 8 以保留向下兼容。图 2.14 显示了页面顶部的标题栏。默认情况下，图像栏显示启动图标和应用程序名称（左上角）。在右上角，你会注意到我之前指出的溢出（Overflow）按钮。点击溢出按钮将显示一个包含我三个菜单选项的下拉列表。

如果我们只更改清单文件，那么我们就把应用程序的用户界面提升到 Android 3.x 水平。但通过几个步骤可以使其变得更有吸引力。

![](img/cbb97d4daaabf800d0384cb0ef181aa8_46_0.png)

在 Android 2.2 模拟器上运行菜单演示程序。

来源：Eclipse Foundation。

首先，为了通过一些代码更改使应用程序更符合 3.0 及更高版本的改进，我们需要在 Eclipse 中更改构建目标。你可以通过在 Package Explorer 中右键点击项目名称，并选择列表底部的 Properties（属性）来实现。在新的列表中选择 Android，你将看到图 2.15 中安装的面板。勾选 Android 3.0 的复选框，并点击底部的 Enter（完成）按钮。

接下来，我们将菜单选项从操作溢出按钮中取出并直接放置在标题栏上。尽管标题栏很漂亮，但它的空间是的。正如你可以想象的，剩余的内容将进入溢溢出，因此请对你的选项进行优先级排序，让重要的项出现在标题栏上。修改你的 `menu.xml` 文件，使其如下文件列表所示，为每个菜单项添加 `android:showAsAction="ifRoom|withText"`。

```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:id="@id/dummy"
        android:showAsAction="@ifRoom|withText"
        android:icon="@drawable/icon"
        android:title="Do Something"/>
    <item android:id="@id/anotherdummy"
        android:showAsAction="@ifRoom|withText"
        android:icon="@drawable/icon"
        android:title="Do Something"/>
    <item android:id="@id/close"
        android:showAsAction="@ifRoom|withText"
        android:icon="@drawable/icon"
        android:title="Close"/>
```
