

```cpp
friend CollectionEmp;
};

class CollectionEmp
{
private:
    employee ColEmp[10];
    int Index;
public:
    bool AddToCol(employee Emp)
    {
        if(Index < 9)
        {
            ColEmp[Index] = Emp;
            Index++;
            return true;
        }
        else
            return false;
    }

    void ListDeptWise()
    {
        string TempDeptName;
        cout << "Enter the department of the university:";
        cin >> TempDeptName;
        cout << "\n";

        for(int i = 0; i < 10; ++i)
        {
            if(ColEmp[i].DeptName == TempDeptName)
            {
                ColEmp[i].DisplayDetails();
            }
        }
    }

    CollectionEmp()
    {
        Index = 0;
    }

    CollectionEmp(employee TempEmp[], int Size = 10)
    {
        Index = 0;
        for(int i = 0; i < Size; ++i)
        {
            AddToCol(TempEmp[i]);
        }
    }
};

void main()
{
employee UniEmployee[10] =
{
    employee(1, "Lara", "Exam", "Professor"),
    employee(2, "Ponting", "Marksheet", "Clerk"),
    employee(3, "Laxman", "Accounts", "Head Clerk"),
    employee(4, "Flintoff", "Exam", "Clerk"),
    employee(5, "Murlidharan", "Accounts", "CAO"),
    employee(6, "Sarfaraz", "Exam", "Informator"),
    employee(7, "Dean Jones", "Exam", "Invigilator"),
    employee(8, "Madugalle", "Exam", "Examiner"),
    employee(9, "Ganguly", "Marksheet", "Repeater"),
    employee(10, "Nafees", "Accounts", "Clerk")
};
CollectionEmp UniCol(UniEmployee);
UniCol.ListDeptWise();
}
```

## 程序的工作原理

请查看 CollectionEmp 类的两个构造函数。CollectionEmp 类所包含的 Employee 对象的构造函数并未被调用。

```cpp
CollectionEmp()
{
    Index = 0;
}

CollectionEmp(employee TempEmp[], int Size = 10)
{
    Index = 0;
    for(int i = 0; i < Size; ++i)
    {
        AddToCol(TempEmp[i]);
    }
}
```

让我们理解这个程序试图实现什么。由于该程序已在前面分析过，让我们只看新增的部分。复合对象构造函数不需要调用其所包含对象的构造函数。

在第 5 章讨论拷贝构造函数时，我们曾见过作为 customer 对象一部分的 item 对象的类似示例。即使在 customer 对象的定义中，我们也没有指定任何构造函数调用。与基类构造函数必须被调用的派生类构造函数不同，在这种情况下没有必要调用该构造函数。然而，在容器类的构造函数中可能需要调用所包含对象的构造函数。程序 9.9 就是一个需要进行此类构造函数调用的案例的示例。

### 在复合对象中调用所包含对象的构造函数

假设有一个图形图形（例如人脸），它包含一个三角形、一个正方形和一对圆形（代表鼻子、嘴巴和一对眼睛）。人脸的每个实例都决定了其各个组件的位置，即，如果人脸的第一个实例位于屏幕上的 (2, 2) 处，则组件，即一对圆形、三角形和正方形，将相对于 (2, 2) 绘制。

如果下一个人脸绘制在 (20, 20) 处，则圆形、正方形和三角形将相对于位置 (20, 20) 绘制。当人脸被构造时，所有组件图形都需要相对于人脸的位置进行构造。图形图形 Face 的构造函数应使用所需参数调用，其中之一必须是 Position，该参数反过来用于调用嵌入式（组件）对象的构造函数以找到它们各自的位置。这是一个简化的脸，可以在二维空间中将其放置在想要的位置。根据人脸的位置，元素（两只眼睛的两个圆圈，一个鼻子的三角形和一个嘴巴的正方形）将被绘制。这里为了简单起见，忽略了人脸的方向（人脸朝向的方向）和缩放（使人脸变大变小）等问题。

程序 9.9 用于绘制人脸，但实际上并未在屏幕上绘制人脸，而只是打印一条消息。如果程序中绘制人脸，则代码将依赖于编译器（因为 C++ 没有标准图形库）且更复杂。因此，这里未显示。它仅用于表示复合对象的概念。需要学习的重要部分是调用构造函数以初始化复合对象的一部分的用户定义对象，即在调用人脸构造函数时调用圆、三角形和正方形的构造函数。组件对象的位置取决于复合对象的位置。组件对象的构造函数应使用 MIL 如程序所示进行调用。程序中所有点的 X 和 Y 坐标的值是直观选择的。绘制图形可能不会绘制出精确的人脸，但可能与之相似。可能需要调整所有组件的 X 和 Y 值以使人脸看起来像真正的人脸。

### 程序 9.9 需要调用所包含对象构造函数的复合对象

```cpp
//CompositeObj2.cpp
class Point
{
    int X;
    int Y;
public:
    Point(int TempX = 0, int TempY = 0)
    {
        X = TempX;
        Y = TempY;
    }

    int GetX() const
    {
        return X;
    }
    int GetY() const
    {
        return Y;
    }
};

class Square
{
    Point LeftBottom;
    int Length;
public:
    Square(Point TempLeftBottom, int TempLength)
    {
        LeftBottom = TempLeftBottom;
        Length = TempLength;
    }
};

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
    Face(Point TempPosition) : LeftEye(Point((TempPosition.GetX() + 20),
                                             TempPosition.GetY() + 10), 4),
                               RightEye(Point((TempPosition.GetX() + 50),
                                              TempPosition.GetY() + 10), 4),
                               Nose(Point((TempPosition.GetX() + 35),
                                          TempPosition.GetY() + 20),
                                    (Point((TempPosition.GetX() + 30),
                                           TempPosition.GetY() + 25)),
                                    (Point((TempPosition.GetX() + 40),
                                           TempPosition.GetY() + 25))),
                               Mouth(Point(TempPosition.GetX() + 25,
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

## 程序的工作原理

本程序中定义了五个类。Point 类被设计为派生所有其他图形的基础平台。Point 对象被传递给 Square、Circle 和 Triangle 的构造函数。传递给 Square 的 Point 对象决定了正方形的左下顶点。长度也作为第二个参数传递。给定这两个值，正方形可以很容易地绘制。在三角形的例子中，传递了所有三个顶点。在圆的例子中，传递了一个代表圆心的点和半径。所讨论的组件图形，即 Square、Circle 和 Triangle 本身也是复合对象，包含 Point 对象在其中。在调用这些对象的构造函数时，无需调用 Point 的构造函数。为什么需要在其复合对象 Face 的构造函数中调用 Square、Circle 和 Triangle 的构造函数？这是因为它们的构造不能绝对进行。它们的构造有一个重要的参数 Position，该参数取决于复合对象的构造（复合对象被构造的位置）。因此，组件对象的构造函数应在复合对象的构造函数体内调用。

该程序有两个 Face 类型的对象。两者在二维空间中绘制在不同的位置。由于两者包含不同的坐标，Face 的所有组成部分对象都需要绘制在不同的位置。这是通过在 Face 构造函数的 MIL 中调用组件对象的构造函数来实现的。

## 继承成员与包含成员

有时，C++ 初学者会混淆继承成员和包含成员。虽然它们看起来相同，但它们非常不同。以下是区别：

- 1. 从设计角度来看，继承成员具有类似于子集关系的关联。如果 Scooter 从 Vehicle 继承，则 Scooter 对象也属于 Vehicle 类（踏板车是车辆；因此，它们是车辆的子集）。所有 Scooter 实例都是 Vehicle 实例。在程序 9.9 中，Face 包含 circle 对象，但它没有子集关系。它更像是一种部分关系。鼻子（三角形）是人脸的一部分。左右眼睛（圆圈）也是人脸的一部分。然而，并非所有 Triangle 和 circle 的实例也是 Face 的实例。

- 2. 继承成员必须使用 MIL 在派生类构造函数体之外执行其构造函数。如果基类有构造函数，派生类也必须有自己的构造函数。这两个限制不适用于包含成员。我们已经看到了两个不同的案例，一个是程序 9.8 中的员工集合对象，另一个是程序 9.9 中的组件对象 Square、Circle 和 Triangle，其中未调用嵌入对象的构造函数。

- 3. 在根据传递给容器类构造函数的数值为所包含对象的构造函数赋值时需要小心。在这里，需要使用 MIL 在容器类的构造函数中执行所包含对象的构造函数。（程序 9.9 就是这种需求的示例。代表眼睛、鼻子和嘴巴的圆圈、三角形和正方形需要根据人脸的位置进行绘制。）

- 4. C++ 对两种类型的成员（继承和包含）以类似的方式处理（嵌入到目标类中）；因此，在编程时它们看起来相似。

- 5. 理解部分与子集关系的区别还有一个帮助。它被称为在需要特定属性时选择正确的链接（或继承链）。假设正在考虑沙发扶手的对象时

