
## 13.16 Mark

一个 **Point**（点）只是 **Window**（窗口）中的一个位置。它不是我们绘制的东西，也不是我们可以看到的东西。如果我们想要标记一个单独的 **Point** 以便能够看到它，我们可以用 §13.2 中的一对线来表示它，或者使用 **Marks**（标记）。这有点啰嗦，所以我们有 **Marks** 的一个简单版本，它由一个点和一个字符初始化。例如，我们可以像这样标记我们在 §13.12 中圆的中心：

```cpp
Mark m1 {Point{100,200}, 'x'};
Mark m2 {Point{150,200}, 'y'};
Mark m3 {Point{200,200}, 'z'};
c1.set_color(Color::blue);
c2.set_color(Color::red);
c3.set_color(Color::green);
```

这将产生

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_510_0.png)

一个 **Mark**（标记）就是一个 **Marks**，其初始（通常也是唯一的）点被直接给出：

```cpp
struct Mark : Marks {
    Mark(Point xy, char c) : Marks(string(1,c))
    {
        add(xy);
    }
};
```

**string(1,c)** 是 **string** 的一个构造函数，将 **string** 初始化为包含单个字符 **c**。

所有 **Mark** 提供的只是一个方便的表示法，用于创建一个 **Marks** 对象，其中单个点被标记为单个字符。**Mark** 值得我们花精力去定义吗？还是说它只是“无谓的复杂化和混淆”？没有明确的、逻辑上的答案。我们就这个问题来回讨论过，但最终决定它对用户有用，且定义它的代价很小。

为什么要使用字符作为“标记”？我们可以使用任何小形状，但字符提供了一组有用且简单的标记。通常，能够使用多种“标记”来区分不同的点集是非常有用的。像 **x**、**o**、**+** 和 **\*** 这样的字符围绕中心是令人愉悦的对称的。

## 13.17 Images

普通的个人计算机在文件中存储成千上万的图像，并且可以通过网络访问数百万张更多图像。自然，我们希望即使在相当简单的程序中也能显示其中的一些图像。例如，这里是一张飓风 Rita 接近得克萨斯湾岸时的投影路径图像（*rita\_path.gif*）：

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_511_0.png)

我们可以选择该图像的一部分，并添加一张从太空拍摄的 Rita 照片（rita.jpg）：

```cpp
Image rita {Point(0,0),"rita.jpg"};
Image path {Point(0,0),"rita_path.gif"};
path.set_mask(Point(50,250),600,400);  // select likely landfall
win.attach(path);
win.attach(rita);
```

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_512_0.png)

set_mask() 操作选择图像的一个子图像以供显示。在这里，我们从 rita_path.gif（加载为 path）中选择一个 600x400 像素的图像，其左上角点位于 path 的点 (50,250)。只选择图像的一部分进行显示是如此常见，以至于我们选择直接支持它。

形状按它们被附加的顺序铺设，就像桌上的纸片一样，因此我们只需在附加 rita 之前附加 path，就得到了 path “在底部”的效果。

图像可以编码为令人眼花缭乱的多种格式。这里我们只处理最常见的两种，JPEG 和 GIF：

```cpp
enum class Suffix { none, jpg, gif };
```

在我们的图形界面库中，我们在内存中用类 **Image** 的对象来表示图像：

```cpp
struct Image : Shape {
   Image(Point xy, string file_name, Suffix e = Suffix::none);
   ~Image() { delete p; }
   void draw_lines() const;
   void set_mask(Point xy, int ww, int hh)
      { w=ww; h=hh; cx=xy.x; cy=xy.y; }
private:
   int w,h;   // define "masking box" within image relative to position (cx,cy)
   int cx,cy;
   Fl_Image* p;
   Text fn;
};
```

**Image** 构造函数试图打开具有给定名称的文件。然后它试图使用指定为可选参数或（更常见的是）文件后缀的编码来创建图片。如果图像无法显示（例如，因为找不到文件），**Image** 将显示一个 **Bad_image**。**Bad_image** 的定义如下：

```cpp
struct Bad_image : Fl_Image {
   Bad_image(int h, int w) : Fl_Image(h,w,0) { }
   void draw(int x,int y, int, int, int, int) { draw_empty(x,y); }
};
```

在图形库中处理图像是相当复杂的，但我们的图形界面类 **Image** 的主要复杂性在于构造函数的文件处理：

```cpp
// somewhat overlaborate constructor
// because errors related to image files can be such a pain to debug
Image::Image(Point xy, string s, Suffix e)
   :w(0), h(0), fn(xy,"")
{
   add(xy);

   if (!can_open(s)) {     // can we open s?
      fn.set_label("cannot open "+s+"");
      p = new Bad_image(30,20);   // the "error image"
      return;
   }

   if (e == Suffix::none) e = get_encoding(s);

   switch(e) {    // check if it is a known encoding
   case Suffix::jpg:
       p = new Fl_JPEG_Image(s.c_str());
       break;
   case Suffix::gif:
       p = new Fl_GIF_Image(s.c_str());
       break;
   default:      // unsupported image encoding
       fn.set_label("unsupported file type \\"+s\"");
       p = new Bad_image(30,20);    // the "error image"
   }
}
```

我们使用后缀来选择我们要创建的持有图像的对象类型（`Fl_JPEG_Image` 或 `Fl_GIF_Image`）。我们使用 **new** 创建该实现对象并将其赋值给一个指针。这是一个实现细节（有关 operator **new** 和指针的讨论见第 17 章），与 FLTK 的组织有关，在这里没有根本重要性。FLTK 使用 C 风格字符串，因此我们必须使用 `s.c_str()` 而不是普通的 `s`。

现在，我们只需要实现 `can_open()` 来测试是否可以以只读方式打开指定名称的文件：

```cpp
bool can_open(const string& s)
{ // check if a file named s exists and can be opened for reading
    ifstream ff(s);
    return ff.is_open();
}
```

打开一个文件然后又关闭它，是一种相当笨拙的方法，用于可移植地将“无法打开文件”相关的错误与文件数据格式相关的错误分离开来。

如果你喜欢，可以查找 `get_encoding()` 函数。它只是查找后缀，并在已知后缀表中查找该后缀。该查找表是标准库的 **map**（见 §21.6）。

## Drill（练习）

- 1. 创建一个 800 乘 1000 的 **Simple_window**。
- 2. 在该窗口最左侧 800 乘 800 的部分放置一个 8 乘 8 的网格（使得每个方块为 100 乘 100）。
- 3. 将将从左上角开始的对角线上的八个方块设为红色（使用 **Rectangle**）。
- 4. 找到一个 200 乘 200 像素的图像（JPEG 或 GIF），并在网格上放置三个副本（每个图像覆盖四个方块）。如果你找不到恰好为 200 乘 200 的图像，使用 set_mask() 选择较大图像中 200 乘 200 的部分。不要遮挡红色方块。
- 5. 添加一个 100 乘 100 的图像。当你点击“Next”按钮时，让它在一个方块到另一个方块之间移动。只需在循环中放入 wait_for_button() 以及一些为你的图像选择新方块的代码。

## Review（复习）

- 1. 为什么我们不“仅仅”直接使用商业或开源图形库？
- 2. 要完成简单的图形输出，你需要我们图形界面库中大约多少个类？
- 3. 使用图形界面库需要哪些头文件？
- 4. 哪些类定义了闭合形状？
- 5. 为什么我们不直接对每种形状都使用 **Line**？
- 6. **Point** 的参数表示什么？
- 7. **Line_style** 的组成部分是什么？
- 8. **Color** 的组成部分是什么？
- 9. RGB 是什么？
- 10. 两条 **Lines** 和一个包含两条线的 **Lines** 之间的区别是什么？
- 11. 你能为每个 **Shape** 设置哪些属性？
- 12. 由五个 **Points** 定义的 **Closed_polyline** 有多少条边？
- 13. 如果你定义了一个 **Shape** 但没有将其附加到 **Window**，你会看到什么？
- 14. **Rectangle** 与具有四个 **Points**（角）的 **Polygon** 有何不同？
- 15. **Polygon** 与 **Closed_polyline** 有何不同？
- 16. 哪个在上面：填充还是轮廓？
- 17. 我们为什么没有费心去定义一个 **Triangle** 类（毕竟，我们确实定义了 **Rectangle**）？
- 18. 如何移动 **Window** 中的 **Shape** 到另一个位置？
- 19. 如何用一行文本标记 **Shape**？

