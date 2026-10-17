
# 第8章 相机作为数据源

```java
@Override
protected void getActivityResult(int requestCode
```

```java
@Override
protected void onSaveInstanceState(Bundle outState) {
}

public void addArchive() {
  try {
    // 如果没有图片名称，则显示 toast 并返回
    if (pictlet.getText().toString() == null) {
      Toast toast = Toast.makeText(getApplication(),
        "你必须为这张图片输入名称",
        Toast.LENGTH_LONG);
      toast.setGravity(android.view.Gravity.TOP
        | android.view.Gravity.CENTER_HORIZONTAL, 0, 0);
      toast.show();
    }
```

## 应用中的照片

```java
return;
//将这些照片详情附加到与图片一起存储的文本文件中
File archive = new File(Environment.getExternalStorageDirectory())
 + "/DCIM/Camera/" + "archive.txt";
FileOutputStream os = new FileOutputStream(archive, true);
// true 表示追加模式
OutputStreamWriter osw = new OutputStreamWriter(os);
BufferedWriter bw = new BufferedWriter(osw);
bw.write("Date: " + picdate.getText().toString() + "\n");
bw.write("Title: " + pictitle.getText().toString() + "\n");
bw.write("Description: " + picdesc.getText().toString() + "\n");
bw.close();

catch (IOException exception) {

}
```

```java
private Bitmap sizePic(String picfilename) {
// 此方法的依据来源：
// http://developer.android.com/training/camera/photobastics.html
// 获取 View 的尺寸
int targetW = 400; // 匹配 manifest 中 ImageView 的规格
int targetH = 400; // 与上相同
// 获取位的尺寸
BitmapFactory.Options bmOptions = new BitmapFactory.Options();
bmOptions.inJustDecodeBounds = true;
BitmapFactory.decodeFile(Environment.getExternalStorageDirectory() + "/pictures/newpic.jpg", bmOptions);
int photoW = bmOptions.outWidth;
int photoH = bmOptions.outHeight;
// 决定缩小图像的倍数
int scaleFactor = Math.min(photoW / targetW, photoH / targetH);
// 将图像解码为填充视图大小的位图
bmOptions.inJustDecodeBounds = false;
bmOptions.inSampleSize = scaleFactor;
bmOptions.inPurgable = true;
try {
  Thread.sleep(500); // 延迟半秒以允许图片处理
// processing
} catch (InterruptedException ie) {
}
Bitmap bitmap = BitmapFactory.decodeFile(Environment.getExternalStorageDirectory() + "/DCIM/Camera/" + picfilename + ".jpg", bmOptions);

return bitmap;
public void onClose() {
  if (camera != null) {
    camera.release();
    camera = null;
  }
  PhotoCapture.this.finish();
}
```

在这个版本中，`onActivityResult` 方法要稍微复杂一些。从 intent 返回的是所选图片的 URI。通过它，我们可以获取图像的完整路径：目录、子目录和文件 ID。就像我们在第 5 章“内容提供者”中对日历和联系人内容提供者所做的那样，我们可以使用文件 ID 作为唯一键查询图库内容提供者以获取有关图像文件的更多细节。然后我们可以检索图像标题（图像名称），并将其作为创建用于查看位图的方法 `sizePic()` 的参数。

在 `sizePic()` 方法中，我硬编码了尺寸以匹配 XML 文件中 `ImageView` 对象的尺寸。

由于图像在这一版本的应用程序中已经存在，并且应该以高分辨率格式保留，我删除了归档方法中从 `ImageView` 保存图像的代码。第二种变体的外观与第一种基本相同。

# 第 9 章 部署与版本控制

![](img/cbb97d4daaabf800d0384cb0ef181aa8_273_0.png)

# 图 9.1

Eclipse 中新项目的 API 规范设置。

来源：Eclipse 基金会。

如果你使用的是旧版本的插件，该版本在项目开始时没有提供这些设置（在我的另一台开发机上，我使用的是第 16 版本，它没有提供图 9.1 所示的界面），你仍然可以在 `manifest` 文件中手动设置这些内容。如果你处于“自备设备”（BYOD）的环境中，并且无法控制使用你应用程序的设备，那么这些属性可能至关重要。Android 版本低于你指定的最低版本的设备将无法安装该应用程序；因此，设置最低软件开发工具包（SDK）版本将让你对哪些设备将安装你的应用程序具有一定的控制。

`manifest` 文件中下一个重要的设置是 `manifest` 元素本身的属性；换句话说，它们是在起始 `<manifest>` 标签内部的属性。它们如下：

- `android:version`——这是一个表示应用程序版本的整数值。新启动的项目被设置为 1。后续的发布版本应该比之前的数字大。你可能从未打算将应用程序推向市场，但如果你确实这样做了，并计划以后通过升级来替换它，请记住更改版本号，否则市场将拒绝你。

- `android:versionName`——新项目从 1.0 开始。Android 系统并不关注这个数字，因此开发者可以随意使用它。该值以字符串形式存储，因此开发者可以在名称中使用多个小数点来指定修订级别，例如 1.2.1、1.2.2、1.3.0 等，具体根据添加的功能或或修复的 bug 程度而定。你不需要费心这个属性，但我强烈建议你作为开发者，养成使用此属性作为参考来跟踪和记录修订的习惯。

如果你的应用程序需要使用任何包含的文件、文本文件、SQLite 表或图形，此时你应该将它们放置在应用程序的相应目录中。如果应用程序不需要图形，它至少应该有启动图标。为了测试目的，项目始终始终包含了默认的启动图标。第 20 版插件在项目启动时为你提供了一系列选择，但这些并不适用于部署。网站 `http://developer.android.com/practices/ui_guidelines/icon_design.html` 提供了创建并将图标放置在正确目录中的详细说明。
