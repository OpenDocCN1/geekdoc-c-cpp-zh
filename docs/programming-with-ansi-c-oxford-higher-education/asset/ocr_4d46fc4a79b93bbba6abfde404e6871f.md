```
class Triangle
{
    Point Avertex, Bvertex, Cvertex;
public:
    Triangle(Point TempAvertex, Point TempBvertex, Point TempCvertex)
    {
        Avertex = TempAvertex;
        Bvertex = TempBvertex;
        Cvertex = TempCvertex;
    }
};

class Circle
{
    Point Centre;
    int Radius;
public:
    Circle(Point TempCentre, int TempRadius)
    {
        Centre = TempCentre;
        Radius = TempRadius;
    }
};

class Face
{
    Circle LeftEye;
    Circle RightEye;
    Triangle Nose;
    Square Mouth;
    Point Position;
public:
    Face(Point TempPosition),
    LeftEye(Point((TempPosition.GetX() + 20),
    TempPosition.GetY() + 10), 4),
    RightEye(Point((TempPosition.GetX() + 50),
    TempPosition.GetY() + 10), 4),
    Nose(Point((TempPosition.GetX() + 35),
    TempPosition.GetY() + 20),
    (Point((TempPosition.GetX() + 30),
    TempPosition.GetY() + 25)),
    (Point((TempPosition.GetX() + 40),
    TempPosition.GetY() + 25))),
    Mouth((Point(TempPosition.GetX() + 25),
    TempPosition.GetY() + 30), 20)
    {
        Position = TempPosition;
    }
};

void main()
{
    Face DummyFace(Point(20, 30));
    Face OtherFace(Point(50, 70));
}
```