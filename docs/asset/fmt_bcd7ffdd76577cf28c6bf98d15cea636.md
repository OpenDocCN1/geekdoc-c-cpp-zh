
- 表达式树—使 `DLR` 能够扩展语言集成查询 `LINQ` 表达式树的功用，例如控制流、赋值和其他语言建模节点到动态语言。这些表达式树以抽象语法树 `AST` 的形式定义语言的语义。`AST` 使 `DLR` 能够动态生成代码，`CLR` 在运行时执行该代码。

- **调用站点缓存**—使 `DLR` 能够存储操作和变量特征的信息，例如其数据类型。调用站点缓存还检查是否以前执行过此类操作，并检索有关变量的所有信息。

- **动态对象互操作性**—使 `DLR` 能够提供表示动态对象和操作的类和接口集合。语言开发人员和动态库的作者可以使用这些类和接口创建可在静态和动态类型语言中使用的类。

让我们学习 `ExpandoObject` 和 `DynamicObject` 类。

## 理解 ExpandoObject 和 DynamicObject 类

`DLR` 是使用 `System.Dynamic` 命名空间的类和接口创建的。该命名空间包含 `ExpandoObject` 和 `DynamicObject` 等类。这些类用于在 C# 中实现运行时功能。`ExpandoObject` 类是一个其成员可以在运行时显式添加和删除的类。此类的对象可以在运行时动态初始化。换句话说，`ExpandoObject` 类允许对象的动态绑定，这使你可以使用与 `dynobj.Method` 方法类似的标准语法，而不是使用更复杂的语法，例如 `dynobj.getAttribute("Method")`。

`DynamicObject` 类允许你定义可以在动态对象上执行的具体操作以及执行这些操作的`方法`。例如，你可以定义获取或设置对象属性、调用方法或执行标准数学运算，例如加法和乘法的后果。`DynamicObject` 类提供了一个指定运行时动态行为的父类。此父类不能直接实例化；因此，要实现动态行为，必须从 `DynamicObject` 类继承并重写必要的方法。

在详细讨论了 C# 的动态增强功能之后，让我们现在学习如何在各种应用程序中使用这些增强功能。

## 快速解决方案

## 使用动态数据类型

正如我们在*深入探讨*一节中所讨论的，动态数据类型是在运行时而非编译时解析的数据类型。让我们创建一个名为*DynamicDataType*的控制台应用程序（也可在CD上找到），以了解动态数据类型的实现。

### 清单7.2：展示使用动态数据类型的示例

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace DynamicDataType
{
    class Program
    {
        static dynamic dyn = 5.56;
        public void Method1(string str, int b)
        {
            Console.WriteLine(str);
            Console.WriteLine(b);
        }
        static void Main(string[] args)
        {
            Program p = new Program();

            //This method compiles and runs successfully.
            p.Method1("Hello", 45);
            //The following lines compiles successfully whereas, shows an error at run time.

            //The value type of dynamic dyn variable is float.
            p.Method1("Hello", dyn); //an integer value is required as the second argument
            p.Method1(dyn, dyn); //a string and integer values are required as first and second arguments
            Console.Read();
        }
    }
}
```

清单7.2的输出如图7.3所示：

![](img/e073a4882197be4ab61103cbe0bcb394_290_0.png)

### 图7.3：显示DynamicDataType应用程序的输出

在打印图7.3所示的结果后，*DynamicDataType*应用程序在运行时引发异常，如图7.4所示：

![](img/e073a4882197be4ab61103cbe0bcb394_291_0.png)

### 图7.4：显示运行时异常的错误消息

编译器在编译时不会对`dyn`变量（属于动态数据类型）进行类型检查。因此，`DynamicDataType`应用程序可以成功编译，并且在编译时不会在以下几行显示任何错误：

```
p.Method1("Hello", dyn);
p.Method1(dyn, dyn);
```

现在让我们学习如何将动态数据类型转换为其他数据类型。

## 转换数据类型

有时，你需要从动态数据类型变量中获取其他数据类型变量的值。为此，你需要将动态类型变量的值转换为其他数据类型的变量。`DynamicConversion`控制台应用程序（也可在CD上找到）演示了将变量转换为动态数据类型的示例。清单7.3显示了`DynamicConversion`应用程序的代码：

### 清单7.3：展示将动态数据类型转换为非动态数据类型以及反向转换的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace DynamicConversion
{
    class Program
    {
        dynamic dynDouble = 5.46;
        dynamic dynString = "test string";
        dynamic dynBool=true;
        dynamic dynDate = System.DateTime.Today;

        public void Method1()
        {
            // Printing the data type for dynamic type variables
            Console.WriteLine(dynDouble.GetType());
            Console.WriteLine(dynString.GetType());
            Console.WriteLine(dynBool.GetType());
            Console.WriteLine(dynDate.GetType());
        }

        public void Method2()
        {
            // taking the values for different variables from respective dynamic variables
            double d = dynDouble;
            string str = dynString;
            bool check = dynBool;
            DateTime date = dynDate;

            //Printing the values
            Console.WriteLine("\nDouble: "+d);
            Console.WriteLine("String: "+str);
            Console.WriteLine("Boolean: "+check);
            Console.WriteLine("DateTime: "+date);
        }

        static void Main(string[] args)
        {
            Program p = new Program();
            p.Method1();
            p.Method2();
            Console.WriteLine("\n");
            Console.WriteLine("Press Enter to quit....");
            Console.Read();
        }
    }
}
```

在清单7.3中，我们声明了四个动态数据类型变量并为其赋值。`p`对象调用`Method1`方法，该方法打印这些变量的数据类型。动态数据类型会根据赋予它们的值隐式选择数据类型，并在控制台屏幕上打印这些值。接下来，`p`对象调用`Method2`方法，该方法从相应的动态变量中获取不同变量的值并打印这些值。

清单7.3的输出如图7.5所示：

![](img/e073a4882197be4ab61103cbe0bcb394_292_0.png)

现在让我们学习如何使用`ExpandoObject`类。

## 使用ExpandoObject类

作为参数传递的`ExpandoObject`类的实例在C#中被视为动态对象。这意味着IntelliSense对对象成员不起作用；因此，当调用不存在的成员时，编译器不会引发任何错误。但是，在程序中调用不存在的成员时，会在运行时发生异常。让我们创建一个名为`UsingExpandoObject`的控制台应用程序（也可在CD上找到），它创建并使用一个方法来打印不同属性的名称和值。清单7.4显示了`UsingExpandoObject`应用程序的代码：

### 清单7.4：展示ExpandoObject类的示例

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Dynamic;

namespace UsingExpandoObject
{
    class Program
    {
        static void Main(string[] args)
        {
            // creating variables of dynamic data type
            dynamic son, father;

            // initializing an object of ExpandoObject class
            son = new ExpandoObject();
            son.Name = "son";
            son.Age = 20;

            father = new ExpandoObject();
            father.Name = "Father";
            father.Age = 48;
            father.Children= 3;

            WriteFamily(father);
            WriteFamily(son);
            Console.WriteLine("\n");
            Console.WriteLine("Press Enter to quit....");
            Console.Read();
        }
        private static void WriteFamily(dynamic member)
        {
            Console.WriteLine("{0} is {1} years old.", member.Name, member.Age);
            // The following statement causes an exception
            // if you pass the father object.
            // Console.WriteLine("Father has {0} children", member.Children);
        }
    }
}
```

清单7.4的输出如图7.6所示：

![](img/e073a4882197be4ab61103cbe0bcb394_293_0.png)

图7.6：显示UsingExpandoObject应用程序的输出

现在让我们学习如何使用DynamicObject类。

## 使用DynamicObject类

让我们创建一个名为`UsingDynamicObject`的控制台应用程序（也可在CD上找到），其中展示了派生自`DynamicObject`类的`DynamicWord`类。`DynamicWord`类包含一个预定义的`Dictionary<string, object>`类型的对象，用于存储键值对。此外，`DynamicWord`类重写了`TrySetMember`和`TryGetMember`方法，以支持新语法。它还包含一个`Count`属性，该属性显示字典中包含多少动态属性。清单7.5展示了`DynamicObject`类的示例：

### 清单7.5：展示DynamicObject类的示例

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Dynamic;

namespace UsingDynamicObject
{
    // The class derived from DynamicObject
    public class DynamicWord : DynamicObject
    {
        // The inner predefined dictionary, which represents collection of keys and values
        Dictionary<string, object> dict = new Dictionary<string, object>();

        // This property returns the number of elements in the inner dictionary.
        public int Cnt
        {
            get
            {
                return dict.Count;
            }
        }

        // This method is called, when you try to get a value of a property not defined in the class.
        public override bool TryGetMember(
            GetMemberBinder binder, out object result)
        {
            // Converting the property name to lowercase so that it become case-insensitive.
            string name = binder.Name.ToLower();

            // Set the result parameter to the property value and return true, whenever property name is found in a dictionary
            // otherwise, return false.
            return dict.TryGetValue(name, out result);
        }

        // This method is called, when you try to set a value of a property not defined in the class.
        public override bool TrySetMember(
            SetMemberBinder binder, object value)
        {
            // Converting the property name to lowercase so that it become case-insensitive.
            dict[binder.Name.ToLower()] = value;

            // This method must always returns true, so that you can always add a value
            return true;
        }
    }

    class Program
    {
        static void Main(string[] args)
```
