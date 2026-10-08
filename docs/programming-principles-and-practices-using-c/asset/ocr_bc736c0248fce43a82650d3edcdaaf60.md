This produces

![](bbox=[0.28, 0.13, 0.83, 0.45])

The definition of **Marked_polyline** is

```
struct Marked_polyline : Open_polyline {
    Marked_polyline(const string& m) :mark{m} { if (m=="") mark = "*"; }
    Marked_polyline(const string& m, initializer_list<Point> lst);
    void draw_lines() const;
private:
    string mark;
};
```

By deriving from **Open_polyline**, we get the handling of **Points** “for free”; all we have to do is to deal with the marks. In particular, **draw_lines()** becomes

```
void Marked_polyline::draw_lines() const
{
    Open_polyline::draw_lines();
    for (int i=0; i<number_of_points(); ++i)
        draw_mark(point(i),mark[i]%mark.size()));
}
```