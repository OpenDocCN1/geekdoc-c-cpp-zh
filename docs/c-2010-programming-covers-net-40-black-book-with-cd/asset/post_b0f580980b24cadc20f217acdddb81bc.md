
## Immediate Solutions

## Using Dynamic Data Type

As we discussed in the *In Depth* section that the dynamic data type is data type that is resolved at runtime, instead of compile time. Let’s create a Console application named the *DynamicDataType* (also available on the CD) to understand the implementation of the dynamic data type.

### Listing 7.2: Showing an Example to Use the Dynamic Data Type

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

The output of Listing 7.2 is shown in Figure 7.3:

![](img/e073a4882197be4ab61103cbe0bcb394_290_0.png)

### Figure 7.3: Displaying the Output of the DynamicDataType Application

After printing the result shown in Figure 7.3, the *DynamicDataType* application throws an exception at run time, as shown in Figure 7.4:

![](img/e073a4882197be4ab61103cbe0bcb394_291_0.png)

### Figure 7.4: Displaying the Error Message for Runtime Exception

The compiler does not type check the dyn variable, which is of dynamic data type, at compile time. Therefore, the DynamicDataType application compiles successfully and does not show any error at the following lines at compile time:

```
p.Method1("Hello", dyn);
p.Method1(dyn, dyn);
```

Let’s now learn to convert dynamic data types into other data types.

## Converting Data Types

Sometimes, you need to obtain the value of variables of other data types from the dynamic data type variables. To do this, you need convert the values of dynamic type variables to other data types variables. The DynamicConversion Console application (also available on the CD) shows an example of converting variables to dynamic data type. Listing 7.3 shows the code of the DynamicConversion application:

### Listing 7.3: Showing the Code to Convert a Dynamic Data Type into a Non-dynamic Data Type and Vice Versa

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

In Listing 7.3, we declare and assign values to four dynamic data type variables. The p object calls the Method1 method, which prints the data types of these variables. The dynamic data types implicitly select the data types according to the values assigned to them and print those values on the console screen. Next, the p object calls the Method2 method, which takes the values for different variables from respective dynamic variables and prints the values.

The output of Listing 7.3 is shown in Figure 7.5:

![](img/e073a4882197be4ab61103cbe0bcb394_292_0.png)

Let’s now learn how to use ExpandoObject classes.

## Using the ExpandoObject Class

The instance of the ExpandoObject class that is passed as a parameter is treated as dynamic objects in C#. This indicates that the IntelliSense does not work for object members; therefore, the compiler does not raise any errors when non-existent members are called. However, an exception occurs at run time when a non-existing member is called in the program. Let’s create a Console application, named UsingExpandoObject (also available on the CD), which creates and uses a method to print the names and values of different properties. Listing 7.4 shows the code of the UsingExpandoObject application:

### Listing 7.4: Showing an Example of the ExpandoObject Class

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

The output of Listing 7.4 is shown in Figure 7.6:

![](img/e073a4882197be4ab61103cbe0bcb394_293_0.png)

Figure 7.6: Showing the Output of the UsingExpandoObject Application

Let’s now learn how to use the DynamicObject class.

## Using the DynamicObject Class

Let’s create a Console application, named UsingDynamicObject (also available on the CD), that shows the DynamicWord class, which is derived from the DynamicObject class. The DynamicWord class holds an object of the predefined Dictionary<string, object> type to store the key-value pairs. Further, the DynamicWord class overrides the TrySetMember and TryGetMember methods to support the new syntax. It also holds a Count property, which shows how many dynamic properties the dictionary contains. Listing 7.5 shows an example of the DynamicObject class:

### Listing 7.5: Showing an Example of the DynamicObject Class

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
