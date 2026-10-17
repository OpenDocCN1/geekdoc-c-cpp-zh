
# 第 5 章 内容提供者

当在平板电脑的竖屏模式下运行时（代码将此应用程序固定在竖屏模式），应用程序将如图 5.2 所示。

Android 提供的内容提供者完整列表可以在 `http://developer.android.com/reference/android/provider/package-summary.html` 找到。

## 核心概念摘要

- 内容提供者允许应用程序程序员访问由典型 Android 设备上的公共服务存储的数据，例如联系人列表和日历。数据通过查询进行访问，类似于访问应用程序程序员为特特定应用程序创建的表。尽管书中未涉及，但应用程序程序员可以围绕存储在设备上的数据表创建自己的内容提供者。
- 用于数据表的所有典型操作（如创建、读取、更新和删除记录）都可以通过第三方应用程序对内容提供者维护的记录进行。然而，应用程序需要在清单文件中写入特定的权限，以允许应用程序更改内容提供者的记录。清单条目将向应用程序安装程序发出这些权限请求，并允许设备用户在选择不允许权限时取消安装。
- 虽然某些内容提供者的记录系统设计可能非常简单，但其他系统如联系人列表可能相当复杂。选择访问内容提供者记录的程序员应该对应用程序进行大量的测试，以确保这些记录的完整性不受破坏。

![](img/cbb97d4daaabf800d0384cb0ef181aa8_181_0.png)

**图 5.2** 在 Toshiba Thrive 平板设备上运行的带有联系人列表增强的应用程序。

来源：Google。

## 复习题

你可以在书末附录找到这些复习题的答案。

1. 内容提供者使用的通用资源标识符 (URI) 的通用语法是 ____________________。
2. `____________________` 类的对象用于持有发送到内容提供者的查询结果。
3. 向系统日历添加事件时，应该将哪五个时间值添加到事件的开始结束时间内？____________________。
4. 1 月用于添加事件的数值为：____________________。
5. 下午 2:00 开始的事件应该使用什么整数值？____________________。
6. 访问日历内容提供者需要在文件中添加哪些权限？____________________
7. 访问联系人内容提供者需要在文件中添加哪些权限？____________________
8. 查询内容提供者时，哪个类返回 `Cursor` 对象？
9. 添加到设备的多个电子邮件帐户共享同一个内容提供者，对吗？____________________。
10. 为了方便起见，应用程序程序员可以通过 `____________________` 访问内置接口。

## 建议项目

- 在第 4 章和第 5 章中，我们使用 `ListView` 以结构化的形式显示数据。重写显示设备日历的应用程序，使用 `ListView` 而不是文本字段。
- 使用日历内容提供者构建一个简单的预约系统。
- 开发一个查询具有电子邮件地址的联系人的查询。然后使用 `Intent` 向他们发送问候。
- 自行研究 Android 设备上哪些其他服务可以作为内容提供者访问。然后构建一个从一个或多个此类服务检索的应用程序。

# 第 6 章 客户端-服务器应用程序上的无连接通信

手机或平板的处理资源非常丰富，任何业务应用程序都可能依赖或至少从访问外部数据受益，无论来自互联网还是局域网 (LAN)。数据可以多种格式进出设备，从纯文本到图像等任何形式。访问可以是无连接的（例如网页），也可以通过连接到服务器端应用程序的面向连接的数据流。对于不熟悉网络的人来说，面向连接的通信是指通信设备在传递有用信息之前通过交换消息来建立连接。这种类型的通信更可靠，但双方之间必须传递更多数据。这些额外数据被称为开销。相反，无连接通信不使用此类确认，任何一方都没有义务跟踪通信状态。这些连接本质上不那么可靠，但开销较小。例如，网页请求是无连接的，因为每个请求都需要新的连接。最容易集成到应用程序中且最容易演示的可能是使用 `WebView` 小部件访问网页。较新的应用程序编程接口 (APIs) 为 `WebView` 提供了丰富的功能。

对象以此进行控制。然而，最基本的设置就能提供一个可用的平台，允许快速访问万维网。访问网页的可能用途可能是访问在线或公司内部目录、访问公司产品等。应用程序程序员无需开发任何网页设计工作，也不需要开发专门为平板电脑开发的企业信息。本质上，浏览器可以使用的任何内容，应用程序都可以使用。

在第一个演示中，我们将介绍使用 `WebView` 小部件的两种方法。第一种是在主 XML 文件中包含一个 `WebView`，并为它设置特定的像素大小。这允许浏览器窗口与应用程序的其他部分共享屏幕空间。通过此示例，读者可以看到如何轻松地在屏幕上定位 `WebView`。第二种方案是通过使用带有独立 XML 文件的独立 `Intent`，将 `WebView` 显示在自己的屏幕上。这种方法可以让 `WebView` 占据最大尺寸，并为应用程序的其他部分留出主屏幕。

然而，在对互联网进行任何操作之前，我们必须在清单文件中输入适当的权限。在你的项目清单文件中添加以下行：

```xml
<uses-permission android:name="android.permission.INTERNET"/>
```

请确保它是一个外层元素，不要将其包含在任何其他标签对中。此外，由于此演示使用了两个 `Activity` 类，第二个类必须添加到清单文件中。不过，这次的条目位于 `<application>` 和 `<activity>` 标签之间。

```xml
<activity android:name=".WebIntent"/>
```

如果你从未编写过多屏幕应用程序，这里有一个快速教程。首先，各种活动被编写为独立的类，并带有独立的源文件。在 Eclipse 中，你可以通过右键点击 Package Explorer 面板中的包，并选择“New（新建）”->“Class（类）”来实现这一点。确保你在顶部写有包名和必要的导入，并确保你的类继承了 `Activity` 类。用你的代码覆盖 `onCreate()` 方法，但要确保在方法中执行任何其他操作之前调用“super”构造函数。你还需要为此活动创建一个 XML 文件，并在你的新类中使用类似如下行代码来引用它：

```java
setContentView(R.layout.browse);
```

你的 XML 文件的实际名称（不带 XML 扩展名）将替换上面的单词。通过右键点击 Package Explorer 中 `res` 文件夹下的 `layout` 文件夹，并选择 `Android XML file` 作为文件类型，为你的额外活动启动 XML 文件。（参见图 6.1 和图 6.2。）

## 互联网上的无连接通信

![](img/cbb97d4daaabf800d0384cb0ef181aa8_186_0.png)

**图 6.1** 从 Package Explorer 开始新建类。

来源：Eclipse Foundation。

从你的主活动，你通过调用类似于下面的代码的 `Intent` 来调用另一个活动：

```java
Intent myIntent = new Intent(MainActivity.this.getApplicationContext(), Intent.class);
startActivity(myIntent);
```

设备的许多服务，例如电话（当然，如果设备是智能手机）等，我们在 `Intent` 类中内置了符号常量。要使用其中一个，你使用类似于下面的代码来调用它，这将启动电话服务。

```java
Uri uri = Uri.parse("tel:888-555-1212");
Intent myIntent = new Intent(Intent.CALL, uri);
startActivity(myIntent);
```

在我们的示例中，注意我们需要从主屏幕将网站 URL 传递到包含网页浏览器的第二个屏幕。我们通过在调用第二个 `Intent` 时传递一个 `Bundle` 来实现这一点。该 `Bundle` 是通过使用 `Intent` 类的 `.putExtra()` 方法并使用键值对作为参数来填充的。你可以根据需要向 `Bundle` 中添加尽可能多的条目。在第二个活动侧，你通过匹配的名称从 `Bundle` 中提取值，键值对。

![](img/cbb97d4daaabf800d0384cb0ef181aa8_187_0.png)

**图 6.2** 从 Package Explorer 开始新建 XML 文件。

来源：Eclipse Foundation。

如果你想从被调用活动向原始活动发送数据，请确保在调用活动中使用 `startForResult` 而不是 `startActivity`。为了防止系统混淆哪个 `Bundle` 对应哪个活动，作为 `startForResult` 的第二个参数添加一个唯一的标识整数。

```java
@Override
public void onCreate(Bundle savedInstanceState) {
    getpageforintent.setOnClickListener(new View.OnClickListener() {
        public void onClick(View v) {
            // 
        }
    });
}

public void onStop() {
    super.onStop();
    this.finish();
}

@Override
public boolean onCreateOptionsMenu(Menu menu) {
    getMenuInflater().inflate(R.menu.activity_main, menu);
    return true;
}
```

以下是第二个 `Activity` 的简要代码。它从 `Bundle` 中提取网页 URL 并使用它来加载 `WebView` 对象。

```java
package com.sheusi.clientserver;

import android.app.Activity;
import android.os.Bundle;
import android.webkit.*;

public class WebIntent extends Activity {
    WebView fullpagewebite = null;

    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.browse);
        Bundle tobedisplayed = this.getIntent().getExtras();
        String pageaddress = tobedisplayed.getString("payload");
        fullpagewebite = (WebView) findViewById(R.id.fullpagewebite);
        fullpagewebite.getSettings().setJavaScriptEnabled(true);
        fullpagewebite.loadUrl(pageaddress);
    }
}
```

使用内置浏览器的运行程序应该如图 6.3 所示。

![](img/cbb97d4daaabf800d0384cb0ef181aa8_191_0.png)

**图 6.3** 在 Toshiba Thrive 平板上使用内置浏览器运行客户端服务器应用程序。

来源：Google。

请记住，网页本质上是一个带有特定内容（即 HTML）的文本文件，只有在浏览器中被解释和渲染时，它才会显示为网页。网页格式为这种形式与其传输方式无关。没有理由文本文件、XML 文件或图像文件不能使用相同的技术进行传输。对于我们刚刚涵盖的应用程序的后续修改，我在 Fleobile.com 的 Web 服务器上从 Wikipedia.org 加载了基本的《米兰达权利》（Miranda Rights）。该文件是纯文本，并被恰当地命名为 `miranda.txt`。我选择这些权利是因为它们作为纯文本很有意义（网页作为纯文本通常意义不大），它们很简短，而且可能很有用，尽管人们希望永远不需要它们。我们将通过将内置 `WebView` 替换为 `EditText` 字段来修改之前的应用程序，并使用它来显示下载的文本。

将你主 XML 文件中的 `WebView` 替换为以下元素。

```xml
android:id="@id/website"
android:layout_width="match_parent"
android:layout_height="500dp"
android:layout_below="@id/getpageforintent"
android:layout_centerHorizontal="true"
android:padding="@dim/padding_medium"
tools:context=".MainActivity" />
```

使用 URL 连接下载文件，必须在单独的线程中运行该过程。为了实现这一点，我创建了一个扩展 Java `Thread` 类的内部类来处理下载。线程的构造函数将 URL（网络地址结合要下载的文件名）作为其唯一参数。随着文本的下载，它填充一个 `StringBuilder` 对象，该对象稍后返回给按钮的 `onClick()` 方法。一旦下载完成且 `StringBuilder` 返回到 `onClick()` 方法，它就可以显示在任何能够显示文本的控件中、保存到文件中，或者两者兼有。

在某些情况下，条件使得应用程序必须从 URL 下载内容，例如连接较弱或服务器很忙。如果程序员评估认为这种情况是可能的，他可能希望在应用程序继续之前为连接设置一个允许的超时时间。要实现这一点，他将使用 `URLConnection` 的 `setTimeout()` 方法，并将允许的毫秒数作为参数。然而，如果连接没有在允许的时间内建立，该方法将失败并导致 `TimeoutException`，应用程序必须以某种优雅的方式对异常进行处理。

另一个需要解决的时间问题是，`onClick()` 方法中的代码必须等待下载线程完成后才能继续检索 `StringBuffer` 并使用它的业务。为了做到这一点，我们使用了创建并实例化用于下载的线程的 `join()` 方法。

需要注意的是，为了方便起见，我硬编码了下载的实际文件名（`miranda.txt`）并将其附加到 URL 之后，以保持用户界面的一致性并允许全屏浏览器选项继续正常工作。程序员在适配应用程序时必须处理如何指定文件名。主 `Activity` 修改后的代码如下。

```java
package com.sheusi.clientserver;

import android.os.Bundle;
import android.app.Activity;
import android.view.Menu;
import android.view.MenuItem;
import android.view.View;
import android.support.v4.NavUtils;
import android.widget.*;
import android.content.Intent;
import java.net.*;
import java.io.*;
import android.util.Log;
```

```java
public class MainActivity extends Activity {
    EditText website = null;
    Button getpage = null;
    Button getpageforintent = null;
    EditText urlrequest = null;

    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);
        getpageforintent.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
                String myurl = urlrequest.toString();
                if (!myurl.isEmpty()) {
                    Background b = new Background(myurl + "/miranda.txt");
                    b.start();
                }
            }
        });
        getpage.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
                try {
                    b.join();
                    StringBuffer sb = b.retrieveBuffer();
                }
            }
        });
    }
}
```
