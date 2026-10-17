
```java
package com.sheusi.paretochart;
import android.os.Bundle;
import android.app.Activity;
import android.content.Context;
import android.graphics.Canvas;
import android.graphics.Color;
import android.graphics.Paint;
import android.view.Menu;
import android.widget.Widget.*;
import android.view.*;
import android.util.DisplayMetrics;
import java.util.ArrayList;
import java.util.Collections;
import android.content.pm.ActivityInfo;

public class MainActivity extends Activity implements View.OnClickListener {
    LinearLayout l1 = null;
    EditText et = null;
    Button b1 = null;
    Button b2 = null;
    Context myContext = null;
    MyPlot mp = null;

    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        this.setRequestedOrientation(ActivityInfo.SCREEN_ORIENTATION_LANDSCAPE);
        myContext = this.getApplicationContext();
        l1 = (LinearLayout) findById(R.layout.rightside);
        et = (EditText) findById(R.id.et);
        b1 = (Button) findById(R.id.b1);
        b2 = (Button) findById(R.id.b2);
        b1.setOnClickListener(this);
        b2.setOnClickListener(this);
    }

    @Override
    public void onClick(View v) {
        if (v == b2) {
            et.setText("");
        } else {
            int freqotal = 0;
            int m_cumpercentage = 0;
            ArrayList<Factor> pareto = new ArrayList<Factor>();
            String[] lines;
            String[] pieces;
            String s = et.getText().toString();
            if (s.contains("-")) {
                et.setText("数据格式错误，请使用 \n频率。\n点击按钮清除数据.");
                return;
            }

            lines = s.split("\n");
            for (int ct = 0; ct < lines.length; ++ct) {
                if (lines[ct].contains("-")) {
                    pieces = lines[ct].split("-");
                    pareto.add(new Factor(pieces[0], Integer.parseInt(pieces[1])));
                }
            }
            Collections.sort(pareto);
            Object[] array = pareto.toArray();
            for (int x = 0; x < array.length; ++x) {
                freqotal += ((Factor) array[x]).getFrequency();
            }
            System.out.println("Total frequency: " + freqotal);
            for (int x = 0; x < array.length; ++x) {
                ((Factor) array[x]).percentage = ((Factor) array[x]).getFrequency() * 100 / freqotal;
                m_cumpercentage += ((Factor) array[x]).getFrequency() * 100 / freqotal;
            }
            if (mp != null) {
                removeView(mp);
                mp = null;
            }
            mp = new MyPlot(getApplicationContext(), array);
            addView(mp);
        }
    }

    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        getInflater().inflate(R.menu.activity_main, menu);
        return true;
    }

    @Override
    public void onStop() {
        super.onStop();
        et.setText("");
        if (mp != null) {
            removeView(mp);
            mp = null;
        }
    }
}

class Factor implements Comparable {
    String category;
    public int frequency;
    public int percentage;
    public int cumpercentage;

    public Factor(String n, int a) {
        category = n;
        frequency = a;
    }

    public int getFrequency() {
        return frequency;
    }

    @Override
    public int compareTo(Object ol) {
        if (this.frequency == ((Factor) ol).frequency)
            return 0;
        else if (this.frequency > ((Factor) ol).frequency)
            return -1;
        else
            return 1;
    }
}

class MyPlot extends TextView {
    Paint paint = new Paint();
    DisplayMetrics dm = new DisplayMetrics();
    private Object[] plots;
    private int hirowvalue;
    private int count;
    private int column;

    public MyPlot(Context context, Object[] array) {
        super(context);
        setBackgroundColor(Color.YELLOW);
        setHeight(500);
        setWidth(500);
        plots = array;
    }

    @Override
    public void onDraw(Canvas c) {
        paint.setStrokeWidth(2);
        // 绘制右侧刻度
        count = 0;
        int jump = 0;
        while (count < 100) {
            c.drawText(String.valueOf(count) + "%", 450, 500 - jump, paint);
            count = count + 10;
            jump++;
        }
        c.drawText("100%", 450, 9, paint);
        // 绘制左侧刻度
        hirowvalue = ((Factor) plots[0]).getFrequency();
        vfactor = 500 / hirowvalue;
        count = 0;
        int interval = 0;
        while (count <= hirowvalue) {
            c.drawText("-", 3, 500 - count * vfactor, paint);
            if (interval % 5 == 0) {
                c.drawText(String.valueOf(interval), 6, 500 - count * vfactor, paint);
            }
            ++interval;
            count++;
        }
        // 绘制频率柱状图和标签
        paint.setStrokeWidth(20);
        paint.setColor(Color.BLUE);
        column = 1;
        for (count = 0; count < plots.length; ++count) {
            c.drawLine(column * 50, 500, column * 50, 500 - ((Factor) plots[count]).getFrequency() * vfactor, paint);
            c.drawText((Factor) plots[count]).category, column * 50, 500 - ((Factor) plots[count]).getFrequency() * vfactor, paint);
            ++column;
        }
        // 绘制累计百分比点
        paint.setColor(Color.RED);
        paint.setStrokeWidth(2);
        column = 1;
        for (count = 0; count < plots.length; ++count) {
            c.drawCircle(column * 50, 500 - ((Factor) plots[count]).cumpercentage * 5, (float) 2.0, paint);
            ++column;
        }
        // 连接点
        paint.setStrokeWidth(2);
        column = 1;
        for (count = 0; count < plots.length - 1; ++count) {
            c.drawLine(column * 50, 500 - ((Factor) plots[count]).percentage * 5, (column + 1) * 50, 500 - ((Factor) plots[count + 1]).percentage * 5, paint);
            column++;
        }
    }
}
```

## 核心概念总结

平板设备的大屏幕尺寸允许开发者创建丰富且密集的用户界面，同时为屏幕虚拟键盘留出空间。尽管本书侧重于选择和锁定竖屏或横屏模式，但应用程序开发者可以设计一种能够在运行时适应环境的屏幕。

开发者可以在设计时在 XML 文件中配置屏幕上的控件或小部件，也可以在运行时从屏幕上添加或删除它们。使用在第 2 章“迁移到 Android 3.0 及以上版本”中讨论的片段（`fragments`），开发者可以在应用程序中切换大块的屏幕控件。

应用程序开发者可以对 `EditText` 等小部件进行子类化，以包含错误检查和验证，然后在单个应用程序或多个应用程序中重用它们。同样，开发者可以对 `TextView` 小部件进行子类化以显示数据的图形表示。使用任意数量和颜色的条形、线条或点可以提供愉快且信息丰富的用户体验。

`SimpleAdapter`、`ArrayList` 和 `HashMap` 类对于以美观向用户展示数据至关重要。学习这些类并通过修改本章所示的示例来练习它们。

## 复习题

你可以在书末尾的附录中找到这些复习题的答案。

- 1. 如 `RelativeLayout` 和 `LinearLayout` 等布局管理器属于一组被称为 ________ 的控件。

- 2. 用于屏幕水平和垂直方向的正确术语是 ________ 和 ________ 模式。

- 3. 根据小部件与屏幕上其他控件的关系进行定位的布局是 ________。

- 4. 缩写 `dp` 和 `dip` 是 ________ 的代表。

- 5. 一个 `LinearLayout` 可以嵌入屏幕上的另一个 `LinearLayout` 中，对还是错？

### 第 4 章 表单与图形

6. 写单行代码，将屏幕锁定在竖屏模式。

7. 所有子类中引用其父类并通常在构造函数使用的方法是

8. 模运算运算符的作用是什么？

9. 开发者使用哪种监听器类（`listener class`）来检测用户何时离开屏幕上的特定小部件（例如在表单从一个 `EditText` 移动到下一个 `EditText`）？

10. 图形点 0,0 位于容器的哪个角？

## 建议项目

- ■ 研究、比较和对比 JPEG、BMP 和 PMG 图形格式。它们的用途、优点和缺点是什么？

- ■ 收集特定年份的平均每月气温并以帕累托图练习为指南绘制图表。

- ■ 为 `EditText` 类编写一个子类，它可以接受浮点值，并在用户离开字段时将其正确四舍入为适当的整数值。再写另一个子类，在用户离开字段时将文本转换为全大写。

- ■ 研究用于文本字段的 `android:inputType="textPassword"` 属性。编写一个简单的演示，匹配从一个 `EditText` 的账户名到另一个 `EditText` 中输入的密码，并在用户离开最后一个字段时指示匹配或不匹配。

# 第 5 章 内容提供者

## 引言

Android 手持设备或平板设备上许多独立使用的操作（如日历、联系人列表或相册）都通过内容提供者系统提供给应用程序。本质上与自身关联了基本相同数据段的独立人员、地点、事物和事件，非常适合存储在数据表中。事实上，对于设备上的内容提供者也是如此。它们被视为带有数据表的数据库，并以与 SQLite 表相同的方式响应查询。内容提供者以以下格式的统一资源标识符 (`URI`) 命名。

```
content://package.and.class.name /tablename
```

例如，我们将查看第一个内容提供者日历。日历的条目存储在名为 `events` 的表中，当用户发布、读取或修改事件时，其地址如下所示。

```
content://com.android.calendar/events
```

在某种程度上，内容提供者防止了应用程序程序员在每次应用程序需要访问设备内置应用程序时都重复造轮。它们还确保用户从一个专门的应用程序到另一个应用程序访问的是一致、可预测的数据集。通常，设备会为可以通过内容提供者访问的数据表提供用户界面，例如设备用户使用这些界面来输入联系人、输入预约或从相册检索图像。由于内容提供者抽象了对系统维护的数据的访问，应用程序开发者可以轻松地访问数据。这使得内容提供者特别有用。

## 日历与事件发布

我们将从查看日历开始。日历通常与名为 `events` 的表相关。日历的条目存储在名为 `events` 的表中，当用户发布、读取或修改事件时，其地址如下所示。

```
content://com.android.calendar/events
```
