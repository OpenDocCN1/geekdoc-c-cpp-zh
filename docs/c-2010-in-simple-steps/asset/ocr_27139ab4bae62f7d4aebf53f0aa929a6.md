| Value | Description |
|---|---|
| Table 11.1: Noteworthy Methods of DynamicObject Class | |
| TrySetMember | Specifies how the operations, which set member values are implemented. Overriding this method in a class that inherits the DynamicObject class helps in specifying the dynamic behavior for such operations, which are used to set a value for a property. |
| TryUnaryOperation | Specifies how unary operations are implemented. Overriding this method in a class that inherits the DynamicObject class helps in specifying the dynamic behavior for unary operations, which include increment, decrement, and many more. |

You can implement the dynamic behavior to your objects by overriding the methods of the DynamicObject class. For instance, if you need to perform binary operations, you can override the TryBinaryOperation method. Now, let's create a console application named DynamicObjectExample to create a dynamic object that overrides the TryGetMember() method; therefore, whenever you access a property, dynamic object returns the name of property as a string by performing the following steps:

+   1. Repeat steps 1 to 3 as discussed earlier while creating the DynamicType application in the Exploring Dynamic Type section of this chapter.
+   2. Enter DynamicObjectExample in the Name text box to specify the name of the application and specify an appropriate location in the Location combo box to save the application. In this case, we have selected the default location, which is c:\users\temp\documents\visual studio 2010\Projects.
+   3. Click the OK button. The DynamicObjectExample application is created.
+   4. Add the highlighted code given in Listing 11.3 in the Program.cs file:

# Listing 11.3: Creating a Dynamic Object

```
```csharp
namespace DynamicObjectExample
{
    public class MyDynamicObject : DynamicObject
    {
        public override bool TryGetMember(GetMemberBinder binder, out object result)
        {
            result = binder.Name;
            return true;
        }
    }
    class Program
    {
        static void Main(string[] args)
        {
            dynamic dObj = new MyDynamicObject();
            Console.WriteLine(dObj.MyDynamicProperty);
            Console.ReadLine();
        }
    }
}
```
```

In Listing 11.3, we have used the TryGetMember() method defined in the DynamicObject class. The TryGetMember() method contains two parameters, binder and result. The binder.Name property of the TryGetMember() method returns the name of the member in which the dynamic operation is performed. In this case, the binder.Name property, returns MyDynamicProperty. The result parameter retrieves the output of the Get operation. Note that when dObj.MyDynamicProperty is called, DLR uses the C# language binder to search for a static definition of this property in the MyDynamicObject class. If no such property is found, DLR calls the TryGetMember() method of the DynamicObject class. This method retrieves information regarding the operation that was invoked through the binder parameter. If the dynamic operation is successful, the TryGetMember() method returns true. However, you must assign the actual result of the operation to the parameter result.

The syntax of TryGetMember() method is as follows:

```
```csharp
public virtual bool TryGetMember(
```
```