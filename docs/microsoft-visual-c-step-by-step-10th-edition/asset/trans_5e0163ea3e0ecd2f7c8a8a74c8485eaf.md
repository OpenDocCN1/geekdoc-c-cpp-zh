

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
    bool this [ int index ] { get; set; }
}

struct RawInt : IRawInt
{
    ...
    public bool this [ int index ]
    {
        get { ... }
        set { ... }
    }
}
```

```csharp
class RawInt : IRawInt
{
    ...
    public virtual bool this [ int index ]
    {
        get { ... }
        set { ... }
    }
}
```

```csharp
struct RawInt : IRawInt
{
    ...
    bool IRawInt.this [ int index ]
    {
      get { ... }
      set { ... }
    }
}
```

```csharp
sealed class PhoneBook
{
  ...
  public Name this[PhoneNumber number]
  {
    get
    }
  ...
}
```

```csharp
sealed class PhoneBook
{
    ...
    public Name this [PhoneNumber number]
    {
        get
        {
            int i = Array.IndexOf(this.phoneNumbers, number);
            if (i != -1)
            {
                return this.names[i];
            }
            else
            {
                return new Name();
            }
        }
    }
}
```

```csharp
sealed class PhoneBook
{
    ...
    public PhoneNumber this [Name name]
    {
        get
        {
            int i = Array.IndexOf(this.names, name);
            if (i != -1)
            {
                return this.phoneNumbers[i];
            }
            else
            {
                return new PhoneNumber();
            }
        }
    }
}
```

```csharp
private void findByName(object sender, RoutedEventArgs e)
{
    string text = name.Text;
    if (!String.IsNullOrEmpty(text))
    {
        Name personsName = new Name(text);
        PhoneNumber personsPhoneNumber = this.phoneBook[personsName];
        name.Text = String.IsNullOrEmpty(personsPhoneNumber.Text) ?
            "Not Found" : personsPhoneNumber.Text;
    }
}
```

```csharp
private void findByClick(object sender, RoutedEventArgs e)
{
    string text = phoneNumber.Text;
    if (!String.IsNullOrEmpty(text))
    {
        PhoneNumber personsNumber = new PhoneNumber(text);
        Name personsName = this.phoneBook[personsNumber];
        name.Text = String.IsNullOrEmpty(personsName.Text) ?
            "Not Found" : personsName.Text;
    }
}
```

```csharp
uint moreBinData = 0b0_11110000_01011010_11001100_00001111;
uint moreHexData = 0x0_F0_5A_CC_0F;
```

```csharp
uint moreHexData = 0x0F_5A_CC_0F;
Console.WriteLine($"{Convert.ToString(moreHexData, 2)}");
// 显示 1111000010110101101100000111
```

```csharp
struct RawInt
{
    ...
    public bool this [ int index ]
    {
      get { ... }
      set { ... }
    }
    ...
}
```

```csharp
interface IRawInt
{
    bool this [ int index ] { get; set; }
}
```

```csharp
struct RawInt : IRawInt
{
    ...
    public bool this [ int index ]
    {
        get { ... }
        set { ... }
    }
    ...
}
```

```csharp
struct RawInt : IRawInt
{
    ...
    bool IRawInt.this [ int index ]
    {
        get { ... }
        set { ... }
    }
    ...
}
```

```csharp
private static final int DEFAULT_SIZE = 100;
private int[] data;
private int head = 0, tail = 0;
private int numElements = 0;

public Queue() {
    this.data = new int[DEFAULT_SIZE];
}

public Queue(int size) {
    if (size > 0) {
        this.data = new int[size];
    } else {
        throw new IllegalArgumentException("size must be greater than zero: " + size);
    }
}

public void enqueue(int item) Exception {
    if (this.numElements == this.data.length) {
        throw new Exception("Queue Full");
    }
    this.data[this.head] = item;
    this.head = (this.head + 1) % this.data.length;
    this.numElements++;
}

public int dequeue() Exception {
    if (this.numElements == 0) {
        throw new Exception("Queue empty");
    }
    int item = this.data[this.tail];
    this.tail = (this.tail + 1) % this.data.length;
    this.numElements--;
    return item;
}
```

```csharp
Queue queue = new Queue(); // 创建一个新的 Queue
queue.Enqueue(100);
queue.Enqueue(-25);
queue.Enqueue(33);
Console.WriteLine($"{queue.Dequeue()}"); // 显示 100
Console.WriteLine($"{queue.Dequeue()}"); // 显示 -25
Console.WriteLine($"{queue.Dequeue()}"); // 显示 33
```

```csharp
Queue queue = new Queue();
Horse myHorse = new Horse();
queue.Enqueue(myHorse); // 编译错误：无法从 Horse 转换为 int
```

```csharp
class Queue {
    ...
    private object[] data;
    ...
    public Queue() {
        this.data = new object[DEFAULT_QUEUE_SIZE];
    }

    public Queue(int size) {
        ...
        this.data = new object[size];
    }

    public void Enqueue(object item) {
        ...
    }

    public object Dequeue() {
        ...
        object queueItem = this.data[this.tail];
        ...
        return queueItem;
    }
}
```

