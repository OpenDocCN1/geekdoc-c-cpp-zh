```
class rectangle
{
    int length, breadth;
    public:
    int area ();
    void set_square(square a);
};
class square
{
    int side;
    public:
    void set_side (int s);
    friend class rectangle;
};
int rectangle::area()
{
    return length * breadth;
}
void square::set_side(int s)
{
    side=s;
}
void rectangle::set_square (square a)
{
    length = breadth = a.side;
}
```