```
```csharp
Console.WriteLine("Enumerator Name:"+TColor.ToString()+"\t\tConstant: "+ (int)TColor);
TColor = Color.Green;
Console.WriteLine("Enumerator Name:"+TColor.ToString()+"\t\tConstant: " + (int)TColor);
TColor = Color.Yellow;
Console.WriteLine("Enumerator Name:"+TColor.ToString()+"\t\tConstant: " + (int)TColor);
Console.ReadLine();
```
```

In the preceding code snippet, a variable named **TColor** of the **Color** enumeration type is created. The TColor variable is then assigned the Red enumerator of the Color enumeration. The value of the enumerator and the underlying constant is then displayed using the **Console.WriteLine()** method. Note that **(int)** prefixed to the TColor variable in the **Console.WriteLine()** method obtains the underlying constant of an enumerator.

# ## Structs

The struct type is represented by the struct keyword. It is a user-defined data type that contains several programming elements, such as variables, methods, properties, and events of different data types. The struct type allows you to create a variable that you can use to access different types of values. Being a value type, structs have a fixed size. In addition, when you assign a variable of struct type to another variable of struct type, the value in the first variable is copied to the second variable. The following code snippet shows how to create a struct type:

```
```csharp
public struct Rectangle
{
    int Length, Breadth;
    public Rectangle(int l, int b)
    {
        Length = l;
        Breadth = b;
    }
    public double Area()
    {
        return (Length * Breadth);
    }
}
```
```

In the preceding code snippet, a struct type named **Rectangle** is created by using the **struct** keyword. The **Rectangle** struct has two variables, **Length** and **Breadth**, of the int type. It also contains two methods, **Rectangle()** and **Area()**. The **Rectangle()** method is a constructor for the **Rectangle** type. It provides initial values to the **Length** and **Breadth** variables. The **Area()** method returns the area of a rectangle by multiplying the values in the **Length** and **Breadth** variables.

After creating the struct type, you can create variables of the struct type and use its variables, methods, and other elements. The following code snippet shows how to use a struct type:

```
```csharp
Rectangle Rect1 = new Rectangle(30,20);
Console.WriteLine("Area of Rect1= " + Rect1.Area());
Console.ReadLine();
```
```

In the preceding code snippet, a variable, Rect1, of the **Rectangle** type is created by calling the constructor of the **Rectangle** type. The values, 30 and 20, are passed to the constructor to set the **Length** and **Breadth** variables of the **Rectangle** type. The **Area()** method is then called on the **Rect1** variable to calculate the area.

Let's now learn about the reference types in C#.

# ## Reference Types

Reference types are those data types that work with the references or memory addresses of data rather than the data itself. When you assign a variable of a reference type to another variable of a reference type, the address of the first variable is copied and assigned to the second variable. This implies that there are two variables having the same memory address; and therefore, changes made to one variable affect the other variable.