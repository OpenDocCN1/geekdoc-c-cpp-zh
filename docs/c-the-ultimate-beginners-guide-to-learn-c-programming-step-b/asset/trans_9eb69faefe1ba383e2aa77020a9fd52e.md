

```csharp
Console.WriteLine("Printing a float value: {0}" , y);
}
void display(string z) {
    Console.WriteLine("Printing a string value: {0}", z);
}
static void Main(string[] args) {
    DisplayData dd = new DisplayData();

    // Call display function to return an integer value
    dd.display(10);
    // Call display function to return a float value
    dd.display(11.385);
    // Call display function to return a string value
    dd.display("Hello Sir/Madam");
    Console.ReadKey();
}
}
}
```

代码执行后将返回以下内容：

```text
Printing an int value: 10
Printing a float value: 11.385
Printing a string value: Hello Sir/Madam
```

我们有函数 *display()* 的三个定义。在本例中，通过改变函数所接受的参数类型实现了重载。在一个实例中，函数接受整数值；在另一个实例中接受浮点值；在最后一个实例中接受字符串。

## 运算符重载

运算符重载是指使用单个运算符执行多种操作。通过运算符重载，可以在 C# 运算符应用于用户定义类型时为其添加额外功能。当其中一个或两个操作数属于用户定义类时，就是这种情况。

以下示例演示了这一点：

```csharp
using System;
namespace PolymorphismApp {
    class Object {
        private double breadth;  // The breadth of the box
        private double length;   // The Length of the box
        private double height;   // The Height of the box
        public double calculateVolume() {
            return breadth * length * height;
        }

        public void setLength( double l ) {
            length = l;
        }

        public void setBreadth( double b ) {
            breadth = b;
        }

        public void setHeight( double h ) {
            height = h;
        }

        // Overload the + operator to add 2 objects.
        public static Object operator+ (Object obj1, Object obj2) {
            Object ob = new Object();
            ob.length = obj1.length + obj2.length;
            ob.breadth = obj1.breadth + obj2.breadth;
            ob.height = obj1.height + obj2.height;
            return ob;
        }
    }

    class BoxTester {
        static void Main(string[] args) {
            Object Object1 = new Object();   // Declare Object1 of type Object
            Object Object2 = new Object();   // Declare Object2 of type Object
            Object Object3 = new Object();   // Declare Object3 of type Object
            double volume = 0.0;   // Store volume of the object here

            // object 1 dimensions
            Object1.setLength(7.0);
            Object1.setBreadth(8.0);
            Object1.setHeight(10.0);

            // Object 2 dimensions
            Object2.setLength(6.0);
            Object2.setBreadth(9.0);
            Object2.setHeight(11.0);

            // Calculate the volume of object 1
            volume = Object1.calculateVolume();
            Console.WriteLine("The volume of Object1 : {0}", volume);
            // Calculate the volume of object 2
            volume = Object2.calculateVolume();
            Console.WriteLine("The volume of Object2 : {0}", volume);
            // Add the two objects
            Object3 = Object1 + Object2;
            // Calculate the volume of object 3
            volume = Object3.calculateVolume();
            Console.WriteLine("The volume of Object3 : {0}", volume);

            Console.ReadKey();
        }
    }
}
```

代码返回以下输出：

```text
The volume of Object1 : 560
The volume of Object2 : 594
The volume of Object3 : 4641
```

我们重载了 + 运算符。该运算符被用于两个数值类型的加法。然而，在上面的示例中，我们使用该运算符将两个对象相加，即 Object1 和 Object2。这得到了 Object3。Object1 和 Object2 是用户定义类型，这意味着我们使用 + 运算符来相加用户定义类型。

请注意，确实可以在 C# 中重载运算符，但并非所有运算符都可以重载。例如，不能重载 ==、<、>、!=、>= 和 <= 等比较运算符。对于 && 和 || 等条件逻辑运算符，我们可以重载它们，但不能直接重载。

### 动态多态

使用 C#，我们可以创建抽象类，这些类适合接口的部分类实现。当派生类从抽象类继承后，这一实现便得以完成。抽象类具有抽象方法，派生类实现这些方法。然而，派生类具有更专门的功能。

请注意，不能创建任何抽象类的实例。抽象方法不能在抽象类之外声明。如果 C# 类被声明为 *sealed*，这意味着该类不能被继承。然而，不允许将抽象类声明为 *sealed*。以下是抽象类的示例：

```csharp
using System;
namespace PolymorphismApp {
    abstract class Object {
        public abstract int area();
    }
    class Object1 : Object {
        private int width;
        private int length;
        public Object1( int x = 0, int y = 0) {
            length = x;
            width = y;
        }
        public override int area () {
            Console.WriteLine("The Object1 area is:");
            return (width * length);
        }
    }
    class Object1Tester {
        static void Main(string[] args) {
            Object1 obj = new Object1(8, 6);
            double x = obj.area();
            Console.WriteLine("The area is: {0}",x);
            Console.ReadKey();
        }
    }
}
```

代码将打印以下结果：

```text
The Object1 area is:
The area is: 48
```

在类中定义希望由继承类实现的函数后，应使用虚函数。

为了实现动态多态，我们使用 *abstract* 类和 *virtual* 函数。  
让我们用一个示例来演示这一点：

```csharp
using System;

namespace PolymorphismApp {
    class Object {
        protected int width, height;
        public Object( int x = 0, int y = 0) {
            width = x;
            height = y;
        }
        public virtual int area() {
            Console.WriteLine("The area of the parent class is :");
            return 0;
        }
    }
    class Object1 : Object {
        public Object1( int x = 0, int y = 0): base(x, y) {

        }
        public override int area () {
            Console.WriteLine("The area of Object1 class is:");
            return (width * height);
        }
    }
    class Object2 : Object {
        public Object2(int x = 0, int y = 0): base(x, y) {
        }
        public override int area() {
            Console.WriteLine("The area of Object2 class is:");
            return (width * height / 2);
        }
    }
    class Caller {
        public void CallArea(Object obj) {
            int x;
            x = obj.area();
            Console.WriteLine("The Area is: {0}", x);
        }
    }
    class TesterClass {
        static void Main(string[] args) {
            Caller c = new Caller();
            Object1 ob1 = new Object1(10, 7);
            Object2 ob2 = new Object2(10, 5);
            c.CallArea(ob1);
            c.CallArea(ob2);
            Console.ReadKey();
        }
    }
}
```

代码返回以下输出：

```text
The area of Object1 class is:
The Area is: 70
The area of Object2 class is:
The Area is: 25
```

## 第 16 章：正则表达式[38]

正则表达式被解释为一种可以与输入文本进行匹配的模式。在 .Net 框架中，有一个正则表达式引擎，我们可以使用它来执行该匹配。模式由一个或多个运算符、字符字面量或构造组成。

### Regex 类

这是一个用于表示正则表达式的类。该类附带许多内置函数，如下所示：

- `public bool IsMatch(string input)` - 该方法指定 Regex 构造函数中指定的正则表达式是否在指定输入字符串中获得匹配。
- `public bool IsMatch(string input, int startPoint)` - 该方法指定 Regex 构造函数中指定的正则表达式是否从输入字符串中的指定位置开始在指定输入字符串中获得匹配。
- `public static bool IsMatch(string input, string pattern)` - 该方法指定指定的正则表达式是否在指定输入字符串中获得匹配。
- `public MatchCollection Matches(string input)`
- `public string Replace(string input, string replacement)` - 该方法用指定的替换字符串替换输入字符串中的匹配项。
- `public string[] Split(string input)` - 该函数有助于按照 Regex 构造函数中指定的正则表达式模式所定义的位置，将输入字符串拆分为子字符串数组。

考虑下面给出的示例：

```csharp
using System.Text.RegularExpressions;
using System;

namespace RegularExpApp {
    class MyProgram {
```

