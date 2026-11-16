

## 构造函数和析构函数作业

- 检查并运行以下文件。显示每个文件产生的输出。请注意，源代码显示在以下页面中，也可以在 Canvas 上找到。
  - elevator1.cpp - 初始化函数
  - elevator2.cpp - 构造函数
  - elevator3.cpp - 重载构造函数
  - elevator4.cpp - 析构函数

- 将 elevator4.cpp 复制到 elevator5.cpp。通过在构造函数和析构函数成员函数中，以及在 main() 中对象实例化之前和之后插入 cout 语句，验证 Elevator 变量的构造函数和析构函数是否被调用。显示新代码及其生成的输出。

- 创建一个新程序 order1.cpp，包含一个类 Order，该类仅包含构造函数和析构函数。通过在构造函数和析构函数成员函数内部插入 cout 语句并在 main() 中创建多个变量，确定变量的构造函数和析构函数调用顺序。要为每个变量生成唯一标识符，请在 cout 语句中使用关键字 this。this 是当前对象的地址，是一个指针。显示新代码及其生成的输出。

- 将 order1.cpp 复制到 order2.cpp。使用 order2.cpp 中的类检查变量的作用域以及构造函数和析构函数调用。在 main() 中放置多个作用域，并在每个作用域的开头定义一个或多个 order 对象。显示新代码及其生成的输出。

```cpp
// elevator1.cpp - initialization function
#include <iostream>
#define FLOORS 10

using namespace std;

class elevator {
    private:
        int floorSelected;
        int floorNumber;
    public:
        void initialize();
        void selectFloor(int floor);
        void go();
};

void elevator::initialize() {
    floorSelected = 0;
    floorNumber = 0;
}

void elevator::selectFloor(int floor) {
    if(floor < 0 || floor >= FLOORS)
        return;
    floorSelected = floor;
}

void elevator::go() {
    if(floorNumber < floorSelected)
        while(++floorNumber < floorSelected)
            cout << "floor: " << floorNumber << "; going up!" << endl;
    else if(floorNumber > floorSelected)
        while(--floorNumber > floorSelected)
            cout << "floor: " << floorNumber << "; going down!" << endl;
    cout << "floor: " << floorNumber << "; stopping." << endl;
}

int main() {
    elevator A;
    A.initialize();
    A.selectFloor(7);
    A.go();
    return 0;
}
```

```cpp
// elevator2.cpp - constructor

#include <iostream>
#define FLOORS 10

using namespace std;

class elevator {
  private:
    int floorSelected;
    int floorNumber;
  public:
    elevator(); // constructor has class name
    void selectFloor(int floor);
    void go();
};

elevator::elevator() {
  floorSelected = 0;
  floorNumber = 0;
}

void elevator::selectFloor(int floor) {
  if(floor < 0 || floor >= FLOORS)
    return;
  floorSelected = floor;
}

void elevator::go() {
  if(floorNumber < floorSelected)
    while(++floorNumber < floorSelected)
      cout << "floor: " << floorNumber << "; going up!" << endl;
  else if(floorNumber > floorSelected)
    while(--floorNumber > floorSelected)
      cout << "floor: " << floorNumber << "; going down!" << endl;
  cout << "floor: " << floorNumber << "; stopping." << endl;
}

int main() {
  elevator A; // constructor called here
  A.selectFloor(7);
  A.go();
  return 0;
}
```

```cpp
// elevator3.cpp - overloading constructors

#include <iostream>
#define FLOORS 10

using namespace std;

class elevator {
    private:
    int floorSelected;
    int floorNumber;

    public:
    elevator();
    elevator(int selected, int number);
    void selectFloor(int floor);
    void go();
};

elevator::elevator() {
    floorSelected = 0;
    floorNumber = 0;
}

elevator::elevator(int selected, int number) {
    floorSelected = selected;
    floorNumber = number;
}

void elevator::selectFloor(int floor) {
    if(floor < 0 || floor >= FLOORS)
    return;
    floorSelected = floor;
}

void elevator::go() {
    if(floorNumber < floorSelected)
    while(++floorNumber < floorSelected)
    cout << "floor: " << floorNumber << " going up!" << endl;
    else if(floorNumber > floorSelected)
    while(--floorNumber > floorSelected)
    cout << "floor: " << floorNumber << " going down!" << endl;
    cout << "floor: " << floorNumber << " stopping." << endl;
}

int main() {
    elevator A; // constructor called here
    elevator B(7,2); // constructor with arguments
    A.selectFloor(7);
    A.go();
    return 0;
}
```

```cpp
// elevator4.cpp - destructors
#include <iostream>
#define FLOORS 10
using namespace std;
class elevator {
    private:
        int floorSelected;
        int floorNumber;
    public:
        elevator();
        elevator(int selected, int number);
        ~elevator();
        void selectFloor(int floor);
        void go();
};
elevator::elevator() {
    floorSelected = 0;
    floorNumber = 0;
}
elevator::elevator(int selected, int number) {
    floorSelected = selected;
    floorNumber = number;
}
elevator::~elevator() {
    selectFloor(0);
    go();
}
void elevator::selectFloor(int floor) {
    if(floor < 0 || floor >= FLOORS)
        return;
    floorSelected = floor;
}
void elevator::go() {
    if(floorNumber < floorSelected)
        while(++floorNumber < floorSelected)
            cout << "Floor: " << floorNumber << ", going up!" << endl;
    else if(floorNumber > floorSelected)
        while(--floorNumber > floorSelected)
            cout << "Floor: " << floorNumber << ", going down!" << endl;
    cout << "Floor: " << floorNumber << ", stopping." << endl;
}

int main() {
    elevator A;
    elevator B(7,2);
    A.selectFloor(7);
    A.go();
    return 0;
}
```

## 构造函数实验（条形码）

2009 年以前，美国邮政局信封上的条形码使用一种称为 POSTNET 的格式来表示五位（或更多位）邮政编码。条形码由长条和短条组成，如下所示：

![](img/adb3588dc0dfe9f607c1d417be6bb240_144_0.png)

对于本程序，我们将条形码表示为一串数字。数字 1 表示长条，数字 0 表示短条。因此，上面所示的条形码在我们的程序中将表示为：

```
110100101000101011000010011
```

条形码的第一位和最后一位始终是 1。去掉这两位后剩下 25 位数字。如果将这 25 位数字分成每组五位，则得到：

```
10100 10100 01010 11000 01001
```

接下来，考虑每组五位数字。每组数字中始终恰好有两个 1。每个数字代表一个数值。从左到右，数字分别编码值 7、4、2、1 和 0。将相应的数值与数字相乘并计算总和，以得到邮政编码的最终编码数字。下表显示了 10100 的编码。

| 条形码数字 | 1 | 0 | 1 | 0 | 0 |
|---|---|---|---|---|---|
| 数值 | 7 | 4 | 2 | 1 | 0 |
| 数字 x 数值的乘积 | 7 | 0 | 2 | 0 | 0 |

邮政编码数字 = 7 + 0 + 2 + 0 + 0 = 9

对每组五位数字重复此过程并连接起来，以得到完整的邮政编码。请注意有一个特殊值。如果一组五位数字的和为 11，则这表示数字 0（这是必要的，因为每组有两个 1 时无法表示零）。上面示例条形码的邮政编码解码为 99504。虽然 POSTNET 方案可能看起来不必要地复杂，但其设计允许机器检测扫描邮政编码时是否出现错误。

你的任务是编写一个 ZipCode 类，包括 ZipCode.h 和 ZipCode.cpp，用于编码和解码美国邮政局信封上使用的五位条形码。该类应有两个构造函数。第一个构造函数应以整数形式输入邮政编码，第二个构造函数应以由 0 和 1 组成的条形码字符串形式输入邮政编码，如上所述。虽然你有两种输入邮政编码的方式，但类在内部应仅使用一种格式存储邮政编码（你可以选择将其存储为由 0 和 1 组成的条形码字符串，或作为邮政编码数字。）该类还应至少有两个公共成员函数，一个以整数形式返回邮政编码，另一个以由 0 和 1 组成的条形码格式字符串返回邮政编码。所有辅助成员函数（在 main() 中未调用但由 ZipCode 类在内部用于执行计算的函数）应声明为私有。

使用以下驱动程序测试你的 ZipCode 类。你应该能够在不做任何更改的情况下编译和链接你的代码到该程序。但是，你最终需要对 main() 进行更改，以将程序的输出捕获到输出文件 csis.txt 中。main() 不应做其他更改。

