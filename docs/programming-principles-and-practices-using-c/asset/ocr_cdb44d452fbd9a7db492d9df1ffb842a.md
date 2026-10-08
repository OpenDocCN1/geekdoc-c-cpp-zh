In our graphics interface library, we represent an image in memory as an object of class **Image**:

```
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
```

The **Image** constructor tries to open a file with the name given to it. Then it tries to create a picture using the encoding specified as an optional argument or (more often) as a file suffix. If the image cannot be displayed (e.g., because the file wasn't found), the **Image** displays a **Bad_image**. The definition of **Bad_image** looks like this:

```
```cpp
struct Bad_image : Fl_Image {
   Bad_image(int h, int w) : Fl_Image(h,w,0) { }
   void draw(int x,int y, int, int, int, int) { draw_empty(x,y); }
};
```
```

The handling of images within a graphics library is quite complicated, but the main complexity of our graphics interface class **Image** is in the file handling in the constructor:

```
```cpp
// somewhat overlaborate constructor
// because errors related to image files can be such a pain to debug
Image::Image(Point xy, string s, Suffix e)
   :w(0), h(0), fn(xy,"")
{
   add(xy);

   if (!can_open(s)) {     // can we open s?
      fn.set_label("cannot open ""+s+"");
```
```