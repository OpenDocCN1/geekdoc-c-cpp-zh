
Perform the following steps to use the dynamic types:

- 1. Start Visual Studio 2010.
- 2. Select **File→New→Project** on the menu bar. The **New Project** dialog box opens.
- 3. Select **Visual C#→Windows** from the **Installed Templates** section in the left pane of the **New Project** dialog box. The project templates available for developing Windows applications in C# are displayed in the middle pane of the **New Project** dialog box.
- 4. Select **Console Application** in the middle pane to create a Console application.
- 5. Enter the name of the application as **DynamicType** (also available on the CD) in the **Name** text box and an appropriate location for the application in the **Location** combo box.
- 6. Click the **OK** button to close the **New Project** dialog box and create the **DynamicType** application.
- 7. Add the code, shown in Listing 3.1, to the **Program.cs** file:

**Listing 3.1: Using the Dynamic Types**

```csharp
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

            p.Method1("Hello", 45);

            dyn = "Welcome";

            p.Method1(dyn, 56);

            p.Method1("Hello", dyn);
            Console.Read();
        }
    }
}
```

In Listing 3.1, a dynamic variable, **dyn**, is declared and initially a float value is assigned to it. A method, **Method1**, is also declared that takes two arguments, first of **string** type and second of **int** type, and displays the values of these arguments. When **Method1** is called for the first time with specific values, it executes successfully and displays the result. Then a string type value is assigned to **dyn**. It shows that the value of a dynamic type variable can be changed dynamically. While calling **Method1** for the second time, variable **dyn** (now having a string value) is passed as a first argument, so it also executes successfully and displays the result. When **Method1** is called for the second time, the dynamic variable is passed as a second argument, which is now referring to a string value while in the declaration of **Method1** it takes an int type value as second argument. Therefore, it compiles successfully and throws an exception at runtime. It shows that a dynamic type variable is bypassed during compilation and does not raise an error at compile time but at runtime it throws an exception.

```csharp
bool check = obj.dynBool;
Console.WriteLine("\nDouble: " + d);
Console.WriteLine("String: " + str);
Console.WriteLine("Boolean: " + check);
Console.WriteLine("\n");
Console.WriteLine("Press Enter to quit...");
Console.Read();
}
}
}
```

In Listing 3.2, three dynamic type variables, dynDouble, dynString, and dynBool, are declared and initially float, string, and bool type values are assigned to them, respectively. Next, an object, obj, of the Program class is created. After that the data types of the values assigned to three dynamic variables are displayed. Then, implicit conversion of dynamic data type to non-dynamic data type is performed. This implies that the value of dynDouble is converted into a double type variable d and the values of dynString and dynBool are converted into string and bool type variables named str and check, respectively. Finally, the values of d, str, and check variables are displayed.

- 8. Press the F5 key on the keyboard to run the application. The output of the application appears, as shown in Fig. C#-3.3:

![](img/9862a98a1a2d3bb14334137965a1ec60_355_0.png)

Now, let’s learn how to perform dynamic operations.

## Performing Dynamic Operations

In the previous sections, you have learned that when you operate the data members that are declared as dynamic, the compiler ignores these members at compile time, it only preserves the information of the members. During runtime, DLR uses this information to resolves their types. The operations performed on these members are known as dynamic operations.

Perform the following steps to perform the dynamic operations:

- 1. *Start* Visual Studio 2010.
- 2. *Select* File→New→Project on the menu bar. The New Project dialog box opens.
- 3. *Select* Visual C#→Windows from the Installed Templates section in the left pane of the New Project dialog box.
- 4. *Select Console Application* in the middle pane to create a Console application.
- 5. Enter the name of the application as **DynamicOperationEx** (also available on the CD) in the **Name** text box and an appropriate location for the application in the **Location** combo box.
- 6. Click the **OK** button to close the **New Project** dialog box and create the **DynamicOperationEx** application.
- 7. Add the code, shown in Listing 3.3, to the **Program.cs** file:

**Listing 3.3: Showing the Code to Perform Dynamic Operations**

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace DynamicOperationsEX
{
    public class Program
    {
        public dynamic Method1(dynamic dvar)
        {
            dynamic dynVar = "This is a local variable";
            int num = 10;
            if (dvar is int)
            {
                return dynVar;
            }
            else
            {
                return num;
            }
        }
        public static void Main(string[] args)
        {
            Program obj = new Program();
            Console.WriteLine(obj.Method1(20));
            Console.WriteLine(obj.Method1("Dynamic Value"));
            dynamic dynObj = new Program();
            Console.WriteLine(dynObj.Method1(25));
            Console.ReadLine();
        }
    }
}
```

In Listing 3.3, a dynamic method, **Method1**, is declared that accepts a **dynamic** argument and returns a dynamic value. In Method1, two variables dynVar and num are declared. The dynVar variable is dynamic type and stores a string value while num is an int type variable. The returned value depends upon the type of the value that is passed to Method1 as parameter. If the value passed to Method1 is of int type, it returns the value assigned to the dynVar variable else it returns the value assigned to num.

- 8. Press the F5 key on the keyboard to run the application. The output of the application appears, as shown in Fig. C#-3.4:

![](img/9862a98a1a2d3bb14334137965a1ec60_356_0.png)

Let’s now learn about the DynamicObject and ExpandoObject classes.

## Creating Objects of the DynamicObject and ExpandoObject Classes

The **System.Dynamic** namespace contains a number of classes and interfaces that help you in dynamic programming. The two most important classes of this namespace are **DynamicObject** and **ExpandoObject**. These classes help you to implement runtime features in your application. The **DynamicObject** and **ExpandoObject** classes are described as follows:

- **DynamicObject**: Enables you to define the dynamic behavior for an object. You cannot instantiate this class directly; therefore, to implement the dynamic behavior, you must create a class inheriting the **DynamicObject** class and override the necessary methods.
- **ExpandoObject**: Refers to a class whose members can be explicitly added and removed from an application at runtime. This class implements the **IDynamicMetaObjectProvider** interface that enables you to pass the object of this class to a function of a dynamic language.

Let’s learn to use these classes.

### The DynamicObject Class

The **DynamicObject** class allows you to define the specific operations that can be performed on dynamic objects as well as the methods to perform those operations.

Perform the following steps to use the **DynamicObject** class in an application:

- 1. *Start* **Visual Studio 2010**.
- 2. *Select* **File→New→Project** on the menu bar. The **New Project** dialog box opens.
- 3. *Select* **Visual C#→Windows** from the **Installed Templates** section in the left pane of the **New Project** dialog box.
- 4. *Select* **Console Application** in the middle pane to create a Console application.
- 5. Enter the name of the application as **DynamicObjectExample** (also available on the CD) in the **Name** text box and an appropriate location for the application in the **Location** combo box.
- 6. *Click* the **OK** button to close the **New Project** dialog box and create the **DynamicObjectExample** application.
- 7. *Add* the code, shown in Listing 3.4, to the **Program.cs** file:

**Listing 3.4: Using the DynamicObject Class**

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Dynamic;
namespace DynamicObjectExample
{
    public class MyDynamicObject : DynamicObject
    {
        public override bool TryGetMember(GetMemberBinder binder, out object
            result)
        {
            result = binder.Name;
            return true;
        }
    }
    class Program
    {
        static void Main(string[] args)
        {
            dynamic dobj = new MyDynamicObject();
            Console.WriteLine(dobj.MyDynamicProperty);
            Console.ReadLine();
        }
    }
}
```

In Listing 3.4, a class **MyDynamicObject** is created that inherits the **DynamicObject** class and overrides the **TryGetMember()** method defined in the **DynamicObject** class. The **TryGetMember()** method contains two parameters, **binder** and **result**. The **binder.Name** property of the **TryGetMember()** method returns the name of the member on which the dynamic operation is performed. In this case, the **binder.Name** property returns **MyDynamicProperty**. The **result** parameter retrieves the output of the
