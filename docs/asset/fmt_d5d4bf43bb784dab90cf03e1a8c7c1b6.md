
# Android 布局与 Java 代码示例

## 布局 XML

```xml
android:layout_height="wrap_content" />

<EditText
    android:id="@+id/desc"
    android:layout_width="fill_parent"
    android:layout_height="wrap_content" />

<EditText
    android:id="@+id/date"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" />

<Button
    android:id="@+id/archive"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" />

<Button
    android:id="@+id/close_app"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" />

</LinearLayout>

<Button
    android:id="@+id/shutter"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" />

<ImageView
    android:id="@+id/pic"
    android:layout_width="match_content"
    android:layout_height="match_parent" />

</LinearLayout>
```

## PhotoCapture Activity (第一版)

正如我提到的，应用程序的 Java 代码非常短。它显示在这里。

```java
package com.usi.photapture;

import android.app.Activity;
import android.content.Context;
import android.content.Intent;
import android.graphics.Bitmap;
import android.graphics.Matrix;
import android.hardware.Camera;
import android.os.Bundle;
import android.os.Environment;
import android.view.View;
import android.widget.Button;
import android.widget.ImageView;
import java.util.Date;

public class PhotoCapture extends Activity {

    Button shutter = null;
    ImageView pic = null;
    EditText picdate = null;
    EditText pictitle = null;
    EditText picdesc = null;
    Button archive = null;
    Button closeapp = null;
    Matrix tempMatrix = null;
    Context myContext = null;
    Camera camera = null;

    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_capture);
        setRequestedOrientation(Activity.SCREEN_ORIENTATION_LANDSCAPE);

        myContext = this.getApplicationContext();
        pic = (ImageView) findViewById(R.id.pic);
        pictitle = (EditText) findViewById(R.id.pic_title);
        picdesc = (EditText) findViewById(R.id.pic_desc);
        shutter = (Button) findViewById(R.id.shutter);
        archive = (Button) findViewById(R.id.archive);
        closeapp = (Button) findViewById(R.id.close_app);

        pic.setDrawingCacheEnabled(true);
        picdate.setText(new Date().toString());

        shutter.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
                Intent intent = new Intent(android.provider.MediaStore.ACTION_IMAGE_CAPTURE);
                startActivityForResult(intent, 1);
            }
        });

        archive.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
                addArchive();
            }
        });

        closeapp.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
                if (camera == null) {
                    camera.release();
                    camera = null;
                }
                PhotoCapture.this.finish();
            }
        });
    } // ends onCreate

    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent intent) {
        super.onActivityResult(requestCode, resultCode, intent);
        if (resultCode == RESULT_OK) {
            Bitmap photo = (Bitmap) intent.getExtras().get("data");
            pic.setImageBitmap(photo);
        }
    }

    @Override
    protected void onRestoreInstanceState(Bundle savedInstanceState) {
    }

    @Override
    protected void onSaveInstanceState(Bundle outState) {
    }

    public void addArchive() {
        try {
            // 如果没有图片名称，显示 toast 并返回
            if (picture.getText().toString() == null) {
                Toast toast = Toast.makeText(getApplicationContext(),
                    "You must enter a name for the picture",
                    Toast.LENGTH_LONG);
                toast.setGravity(android.view.Gravity.TOP
                    | android.view.Gravity.CENTER_HORIZONTAL, 0, 0);
                toast.show();
            }

            // 先保存图像
            File picture = new File(Environment.getExternalStorageDirectory())
                + "/DCIM/Camera/" + picture.getText().toString() + ".jpg");
            FileOutputStream fos = new FileOutputStream(picture);
            pic.getDrawingCache(Bitmap.Compress.JPEG, 100, fos);
            fos.close();

            // 接下来，将这些照片详情追加到与图片一起存储的文本文件中
            File archive = new File(Environment.getExternalStorageDirectory())
                + "/DCIM/Camera/" + "archive.txt";
            fos = new FileOutputStream(archive, true);
            // true 参数表示追加模式
            OutputStreamWriter osw = new OutputStreamWriter(fos);
            BufferedWriter bw = new BufferedWriter(osw);
            bw.write("Date: " + picdate.getText().toString() + "\n");
            bw.write("Title: " + pictitle.getText().toString() + "\n");
            bw.write("Description: " + picdesc.getText().toString() + "\n\n");
            bw.close();
        } catch (IOException e) {
        }
    }
}
```

## 补充方法

```java
public void onClose() {
    if (camera != null) {
        camera.release();
        camera = null;
    }
    PhotoCapture.this.finish();
}
```

## 清单权限

在清单文件中，我们需要添加以下权限元素。

```xml
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```

## 核心机制说明

`startActivityResult()` 和 `onActivityResult()` 方法协同工作。前者启动设备的相机应用程序，后者将结果返回给调用的活动（activity）。此方法中的几行代码从返回值中提取位图并显示在 `ImageView` 对象中。`archive` 方法从屏幕获取位图，将其转换为 JPEG 图像，并存储在设备存储图像的地方，使用用户输入的名称。如果用户忽略了为图像输入文件名，则会出现 toast 消息并且方法结束。存档文件和图像文件默认都存储在设备存储图像的地方。

图 8.4 是 Eclipse 的 DDMS（Dalvik 调试监控服务器）视图的截图，通过该视图查看设备的文件树。在树中，你可以看到应用程序创建的存档文件和图像文件的条目。

| 名字 | 大小 | 时间 | 权限 | 信息 |
| --- | --- | --- | --- | --- |
| > Android | 2012-03-25 | 20:45 | dr-xr-xr | |
| > BSD_ROOT | 2012-06-09 | 22:57 | dr-rw-xr | |
| > Edevtmp | 2012-06-25 | 22:18 | dr-rw-xr | |
| > Blob | 2012-04-18 | 20:01 | dr-xr-xr | |
| > CS | 2012-05-02 | 07:33 | dr-xr-xr | |
| > DDMS | 2012-04-24 | 21:13 | dr-rw-xr | |
| > 100ANDROID | 14030110669268 | - | dr-xr-xr | |
| 14030942329674 | 2012-08-32 | 01:52 | dr-xr-xr | |
| 156021481330652 | 2012-06-14 | 19:56 | dr-rw-xr | |
| 12152312125367 | 2012-05-31 | 19:48 | dr-xr-xr | |
| 19919641225964 | 2012-06-15 | 20:05 | dr-rw-xr | |
| 15193152120964 | 2012-05-09 | 08:53 | dr-xr-xr | |
| 15990641225964 | 2012-06-08 | 09:54 | dr-rw-xr | |
| 17075091220930 | 2012-09-30 | 10:57 | dr-xr-xr | |
| 17026011220931 | 2012-09-31 | 10:57 | dr-xr-xr | |
| 19910011220931 | 2012-10-01 | 06:33 | dr-rw-xr | |
| archive | 1647471220937 | 2012-09-10 | 16:50 | dr-rw-xr | |
| beat | 2012-09-16 | 18:38 | dr-xr-xr | |
| testvideo | 1333947 | 2012-09-30 | 16:50 | dr-rw-xr | |
| Earth-NC | 2012-06-09 | 08:04 | dr-xr-xr | |

![img/bb97aaabf00d38cb0ef18aa263_0.png]
图 8.4 DDMS 视图，显示文件树和图像文件。来源：Eclipse。

存档文件可以放在系统的任何地方，程序员假设所选位置是可访问的。为了方便起见，运行的应用程序如图 8.5 所示。

![img/bb97aaabf00d38cb0ef18aa264_0.png]
图 8.5 照片捕捉存档应用程序。来源：Google。

在此应用程序中，单个描述文件继续作为应用程序使用；读者应该决定此应用程序的变体，可能想要从头开始创建多个文件。此应用程序中的某些调整是为了重新设计屏幕，包括标志和描述、拍摄主题、创建一个快速照片字段、给定主题的打印以及记录。应用程序的唯一缺点是 `ImageView` 中显示的位图。这些对象无法从相机获取最佳分辨率。为了解决这个缺点，考虑下一个示例中的变体。下一个版本使用设备的图库提供程序允许用户扫描设备上存在的照片库，并在选择照片时获取足够的信息以返回图库、检索文件名并在 `ImageView` 中生成真实的高质量照片。应用程序外观的区别在于更改用于启动相机的按钮标签，现在将用于启动图库预览。不需要更改设备拍摄图像时提供的名称，因为该名称将作为存档到设备上的图像文件。XML 文件对于应用程序的第二个版本几乎是相同的，除了之前提到的按钮标签，因此不需要重新打印。然而，Java 文件有重大变化，包括一些导入语句，因此在这里重新打印。

## PhotoCapture Activity (第二版)

```java
package com.sheusi.photapture;

import java.io.*;
import android.app.Activity;
import android.content.Intent;
import android.content.pm.Activity;
import android.graphics.Bitmap;
import android.graphics.Matrix;
import android.os.Bundle;
import android.os.Environment;
import android.view.View;
import android.widget.Button;
import android.widget.ImageView;
import android.widget.*;
import android.content.Context;
import java.util.Date;
import android.hardware.Camera;

// 下是导入语句
import android.provider.MediaStore;
import android.net.Uri;
```
