
```csharp
class Circle
{
    private int _radius;
    public int Radius{
        get {
            return this._radius;
        }
        set {
            this._radius = value;
        }
    }
    ...
}
```

```csharp
class Circle
{
    public DateTime CircleCreatedDate { get; }
    ...
}
```

```csharp
class Circle
{
    public Circle()
    {
        CircleCreatedDate = DateTime.Now;
    }

    public DateTime CircleCreatedDate { get; }
    ...
}
```

```csharp
class Circle
{
    public DateTime CircleCreatedDate { get; } = DateTime.Now;
} ...
```

```csharp
public class Triangle
{
    private int side1Length;
    private int side2Length;
    private int side3Length;

    // 默认构造函数 - 所有所有边的默认值
    public Triangle()
    {
        this.side1Length = this.side2Length = this.side3Length = 10;
    }

    // 指定 side1Length 的长度，其他边的默认值
    public Triangle(int length1)
    {
        this.side1Length = length1;
        this.side2Length = this.side3Length = 10;
    }

    // 指定 side1Length 和 side2Length 的长度，
    // side2Length 的默认值
    public Triangle(int length1, int length2)
    {
        this.side1Length = length1;
        this.side2Length = length2;
        this.side3Length = 10;
    }

    // 指定所有边的长度
    public Triangle(int length1, int length2, int length3)
    {
        this.side1Length = length1;
        this.side2Length = length2;
        this.side3Length = length3;
    }
}
```

```csharp
public class Triangle {
    private int side1Length = 10;
    private int side2Length = 10;
    private int side3Length = 10;

    public int Side1Length
    {
        set => this.side1Length = value;
    }

    public int Side2Length
    {
        set => this.side2Length = value;
    }

    public int Side3Length
    {
        set => this.side3Length = value;
    }
}
```

```csharp
Triangle tri1 = new Triangle { Side3Length = 15 };
Triangle tri2 = new Triangle { Side1Length = 15, Side3Length = 20 };
Triangle tri3 = new Triangle { Side2Length = 12, Side3Length = 17 };
Triangle tri4 = new Triangle { Side1Length = 9, Side2Length = 12, Side3Length = 15 };
```

```csharp
Triangle tri5 = new Triangle("Equilateral triangle")
{
    Side1Length = 3,
    Side2Length = 3,
    Side3Length = 3
};
```

```csharp
class Grade
{
    public int StudentID { get; init; }
    public string Subject { get; init; }
    public char SubjectGrade { get; init; }
}
```

```csharp
var grade1 = new Grade() { StudentID = 1, Subject = "Math", SubjectGrade = 'A' };
```

```csharp
grade1.SubjectGrade = 'B'; // 引起编译器错误：
// 仅初始化属性或索引器 'Grade.SubjectGrade'
// 只能在对象初始化器中赋值
```

```csharp
class Polygon
{
    public int NumSides { get; set; }
    public double SideLength { get; set; }
}
```

```csharp
class Polygon
{
    ...
    public Polygon()
    {
        this.NumSides = 4;
        this.SideLength = 10.0;
    }
}
```

```csharp
static void doWork()
{
    Polygon square = new Polygon();
    Polygon triangle = new Polygon { NumSides = 3 };
    Polygon pentagon = new Polygon { SideLength = 15.5, NumSides = 5 };
}
```

```csharp
static void doWork()
{
    ...
    Console.WriteLine($"Square: number of sides is {square.NumSides}, length of each side is {square.SideLength}");
    Console.WriteLine($"Triangle: number of sides is {triangle.NumSides}, length of each side is {triangle.SideLength}");
    Console.WriteLine($"Pentagon: number of sides is {pentagon.NumSides}, length of each side is {pentagon.SideLength}");
}
```

```csharp
struct Grade
{
    public int StudentID { get; init; }
    public string Subject { get; init; }
    public char SubjectGrade { get; init; }
    public override bool Equals(object obj)
    {
        ...
    }
    public override int GetHashCode()
    {
        ...
    }
}
```

```csharp
var grade1 = new Grade() { StudentID = 1, Subject = "Math", SubjectGrade = 'A' };
var grade2 = new Grade() { StudentID = 1, Subject = "French", SubjectGrade = 'C' };
grade3 = grade1; // 复制 grade1 实例
```

```csharp
Console.WriteLine($"{grade1.Equals(grade3)}");
```

```csharp
record Grade
{
    public int StudentID { get; init; }
    public string Subject { get; init; }
    public char SubjectGrade { get; init; }
}
```

```csharp
record Grade(int StudentID, string Subject, char SubjectGrade);
```

```csharp
var grade1 = new Grade(1, "Math", 'A');
var grade2 = new Grade(1, "French", 'C');
var grade3 = grade1;
```

```csharp
grade1.SubjectGrade = 'B'; // 引起编译器错误：
// 仅初始化属性或索引器 'Grade.SubjectGrade'
// 只能在对象初始化器中赋值
```

```csharp
var grade1 = new Grade() { StudentID = 1, Subject = "Math", SubjectGrade = 'A' };
var grade2 = new Grade() { StudentID = 1, Subject = "French", SubjectGrade = 'C' };
grade3 = grade1; // 复制 grade1 实例
```

```csharp
grade1.SubjectGrade = 'B'; // 引起编译器错误：
```
```csharp
class Grade
{
    public int StudentID { get; init; }
}
```

```csharp
class Polygon
{
    public int NumSides { get; set; }
}
```

```csharp
class Circle
{
    public DateTime CircleCreatedDate { get; }
    = DateTime.Now;
    ...
}
```

```csharp
Triangle tri3 = new Triangle { Side2Length = 12, Side3Length = 17 };
```

```csharp
class Grade
{
    public int StudentID { get; init; }
    public string Subject { get; init; }
    public char SubjectGrade { get; init; }
}
```

```csharp
var grade1 = new Grade() { StudentID = 1, Subject = "Math", SubjectGrade = 'A' };
```

```csharp
record Enrollment(int StudentID, string CourseName, DateOnly DateEnrolled);
```

```csharp
var Enrollments = new Enrollment(StudentID: 1, CourseName: "Physics", DateEnrolled: new DateOnly(2021, 07, 20));
```

```csharp
var (studentID, subjectName, grade) = grade1;
```

```csharp
uint moreBinData = 0b0_11110000_01011010_11001100_00001111;
```

```csharp
uint hexData = 0x0_0F;
uint moreHexData = 0x0_F0_5A_CC_0F;
```

```csharp
uint moreHexData = 0x0_F0_5A_CC_0F;
Console.WriteLine($"{Convert.ToString(moreHexData, 2)}");
// 显示 111100000101101011011000001111
```

```csharp
bits[3] = true; // 当前为无效代码
```

```csharp
struct IntBits
{
    private int bits;
    // 简单的构造函数，实现为表达式体方法
    public IntBits(int initialBitValue) => bits = initialBitValue;
    // 在此处写入索引器
}
```

```csharp
struct IntBits
{
    public bool this [ int index ]
    {
        get => (bits & (1 << index)) != 0;
    }
    set
    {
        if (value) // 如果 value 为 true 则开启位；否则，关闭位
            bits |= (1 << index);
        else
            bits &= ~(1 << index);
    }
}
}
```

```csharp
struct IntBits
{
    ...
    public override string ToString()
    {
        return Convert.ToString(bits, 2);
    }
}
```

```csharp
int adapted = 0b_01111110;
IntBits bits = new IntBits(adapted);
bool peek = bits[6]; // 获取索引 6 处的 bool；peek 应为 true (1)
bits[0] = true; // 将索引 0 处的位设置为 true (1)
bits[3] = false; // 将索引 3 处的位设置为 false (0)
Console.WriteLine($"{bits}"); // 显示 1110111 (0b_01110111)
```

```csharp
public int this [ string name ] { ... } // OK
```

```csharp
public Name this [ PhoneNumber number ] { ... }
public PhoneNumber this [ Name name ] { ... }
```

```csharp
IntBits bits; // bits 包含一个索引器
Method(ref bits[1]); // 编译错误
```

```csharp
struct Wrapper
{
    private int[] data;
    ...
    public int[] Data
    {
        get => this.data;
        set => this.data = value;
    }
}
```

```csharp
Wrapper wrap = new Wrapper();
...
int[] myData = wrap.Data;
myData[0]++;
myData[1]++;
```

```csharp
struct Wrapper
{
    private int[] data;
    ...
    public int[] Data
    {
        get { return this.data.Clone() as int[]; };
        set { this.data = value.Clone() as int[]; };
    }
}
```

```csharp
struct Wrapper
{
    private int[] data;
    ...
    public int this [int i]
    {
        get => this.data[i];
        set => this.data[i] = value;
    }
}
```

```csharp
Wrapper wrap = new Wrapper();
...
int[] myData = new int[2];
myData[0] = wrap[0];
myData[1] = wrap[1];
myData[0]++;
myData[1]++;
```

```csharp
interface IRawInt
{
