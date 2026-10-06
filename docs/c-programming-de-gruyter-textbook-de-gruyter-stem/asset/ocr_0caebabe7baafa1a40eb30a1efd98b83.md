# 5.3 Static Members of Class — 169

| Point |
| - X : int |
| - Y : int |
| - countP : int = 0 |
| + Point(xx : int = 0, yy : int = 0) |
| + GetX() : int |
| + GetY() : int |
| + Point(p : int &) |
| <<static>> + GetC() : void |

![](bbox=[0.358, 0.226, 0.793, 0.238])

```
public:
//external interface
Point(int xx=0, int yy=0) {X=xx;Y=yy;countP++;} //constructor
Point(Point &); //copy constructor
~Point() { count--; }
int GetX() { return X; }
int GetY() { return Y; }
static void GetC() {cout<< Object id="<<countP<<endl; }
//static function member
private:
//private data member
int X,Y;
static int countP; //referential declaration of
//static data member
;
Point::Point(Point &p)
{
X.p=X;
Y.p=Y;
countP++;
}
int Point::countP=0;
//definitional declaration of
//static data member
//initialization, use class name limitation
int main()
{
//main function
Point A(4,5);//define object A
out<<"Point A,"<<A.GetX()"","<<<<AA.GetY()"";//output the number of the object,
A.GetC();//object name reference
Point B(A);//define object B
out<<"Point B,"<<B.GetX()"","<<"B.GetY()"";//output the number of objects,
Point::GetC();
//class name reference
}
```