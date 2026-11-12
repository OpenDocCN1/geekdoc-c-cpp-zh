
```java
new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        //Do button two stuff here
    }
};

@Override
public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.main);
    Button button = (Button)findViewById(R.id.button_one);
    if(button != null)
        button.setOnClickListener(mClickListenerOne);
    Button button_two = (Button)findViewById(R.id.button_two);
    if(button_two != null)
        button_two.setOnClickListener(mClickListenerTwo);
}
```

这次，我没有将 Activity 声明为 OnClickListener 的实现类，而是创建了两个单独的内部对象，分别处理每个按钮的点击事件。我会把*第一个按钮*所需代码放在第一个对象中，把*第二个按钮*所需代码放在第二个对象中。当屏幕上有多个按钮时，我在自己的应用中也经常这样做。这样可以避免我编写一大堆 if 语句（或一个 switch 语句）来判断点击了哪个视图，然后执行相应的操作。

你可以根据自己的需求混合使用这两种技巧。两种方式并没有太大的优劣之分，但了解每种方式有助于你保持代码井井有条。

在这个例子中，我给两个按钮添加了点击监听器。点击监听器可以附加到任何你想让用户与之交互的视图上，无论是整个视图组还是简单的文本视图。

值得再次提及的是，通过设置点击监听器，你是在告诉系统该项可以被选中（用手指触摸）并被点击（用触摸板高亮，然后按中心键或轨迹球确认）。因此，为视图配置的默认选中操作将在选中事件发生时自动执行（无论是来自方向键还是触摸屏）。例如，按钮在用户选中时会变色。文本视图，根据设备的默认 UI 风格，也可能会改变文本的活动颜色。最后，你可以（而且很可能应该）通过声明一个有状态的可绘制对象来指定自定义的显示行为。我将在本书后面展示如何实现这些。

## 创建自定义视图

自定义视图的概念实际上可以分为两部分：扩展现有视图和创建全新视图。在我的 Android 开发职业生涯中，我很少创建完全自定义的视图，所以这里我们跳过这部分。Android SDK 文档为那些勤奋刻苦、想从零开始自己动手实现的读者提供了指引。不过，即使你打算扩展一个 Android 视图，也必须创建一个继承现有视图的新类。下面是具体做法。

### 声明新类

声明自定义视图的第一步是创建类。Android 允许你通过继承现有类来创建任意现有 UI 对象的子类。声明方式如下：

```java
public class CustomTextView extends TextView{
    public CustomTextView(Context context) {
        super(context);
    }
}
```

创建一个自定义文本视图只需这些代码。不过，既然这个自定义文本视图的自定义程度（就像快餐玉米卷里的牛肉一样少），我会添加一些简单的东西让它与众不同。

### 扩展视图

虽然 Android 的布局和视图功能强大且用途广泛，但有时它们并不能完全符合你的需求。幸运的是，扩展它们的功能很容易。为了演示，我编写了一个自定义文本视图，它会改变屏幕上显示的每个字母的颜色。虽然这不算最实用的用例，但它可以展示实现自定义行为是多么简单。

### 定制扩展视图

你可能会惊讶于正确渲染文本到屏幕需要多少代码。Android 的 TextView.java 类有近 5000 行代码。但得益于类的扩展能力，你可以使用所有复杂的布局代码，只定制你感兴趣的部分。在这个例子中，我捕获文本的变化，并为新字符串中的每个字母添加一个新的 ForegroundColorSpan。首先，我声明一个颜色数组。

```java
public class CustomTextView extends TextView{
    int colorArray[] = new int[]{Color.WHITE,
            Color.RED,
            Color.YELLOW,
            Color.GREEN,
            Color.BLUE,
            Color.MAGENTA,
            Color.CYAN,
            Color.DKGRAY};
```

现在，每次文本改变时，我都会为每个字母添加一个新的 ForegroundColorSpan。

```java
protected void onTextChanged(CharSequence text,
        int start, int before, int after )
{
    //Keep the view from getting into an infinite loop
    if(selfChange){
        selfChange = false;
        return;
    }
    selfChange=true;
}
```

我确保不会陷入无限循环（颜色变化会触发另一个 onTextChanged 调用，而该调用又会改变颜色，接着再次触发……你懂的）。接下来是改变颜色的代码：

```java
SpannableStringBuilder builder = new SpannableStringBuilder(text);
builder.clearSpans();
ForegroundColorSpan colorSpan;
int color;
for(int i=0; i < text.length(); i++){
    //pick the next color
    color = colorArray[i%colorArray.length];
    //Create the color span
    colorSpan = new ForegroundColorSpan(color);
    //Add the color span for this one char
    builder.setSpan(colorSpan,
            i, i,
            Spannable.SPAN_EXCLUSIVE_EXCLUSIVE);
}
setText(builder);
```

同样，这并不复杂，但扩展现有视图类也不复杂。另外请注意，这段代码会清除文本上可能已经设置的所有格式。（在这一点上，不必过于纠结 spans 和 SpannableStringBuilder 是如何工作的。简而言之，它们是可以添加到字符串上的格式块。更多信息请查阅 Android SDK 文档。）如果你想挑战一下编码，可以尝试创建一个包含所有可能的 RGB 十六进制颜色值的数组，并循环遍历该数组。

### 使用你扩展的视图

与任何其他 Android 视图一样，你可以在 Java 代码中于运行时创建它的新实例，也可以在 XML 布局文件中预先声明它。下面是在 Activity 中使用它的方法：

```java
public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    CustomTextView customView = new CustomTextView(this);
    customView.setText("Hello There!");
    setContentView(customView);
}
```

这里没有任何你以前没见过的东西。我创建视图的新实例，为它设置文本，然后把它设为 Activity 的主视图。你也可以把它和其他视图一起放入某个布局中。还可以把这个自定义视图添加到用 XML 描述的布局中。但在你开始于 XML 文件中声明自定义视图之前，需要创建完整的 View 构造函数集合。你的自定义视图应该看起来像这样：

```java
public class CustomTextView extends TextView{
    public CustomTextView(Context context,
                          AttributeSet attributeSet,
                          int defStyle)
    {
        super(context, attributeSet, defStyle);
    }

    public CustomTextView(Context context,
                          AttributeSet attributeSet)
    {
        super(context, attributeSet);
    }

    public CustomTextView(Context context){
        super(context);
    }
    //Rest of the class omitted for brevity
}
```

当 Android 解析你的 XML 布局并创建视图时，它需要向构造函数传入一个属性集，因为其中包含所有布局信息、文本，以及你添加的以 android 开头的各种属性。如果你忘了添加这些构造函数，一切仍能编译，但当你尝试绘制屏幕时，就会弹出可怕的“意外强制关闭”窗口。

现在有了正确的构造函数，你可以在 XML 中创建并布局自定义视图了。在下面的代码中，我添加了一个彩虹动画自定义文本显示的实例。

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    >
    <com.haseman.ui.CustomTextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="See how the colors change!"
        />
```
