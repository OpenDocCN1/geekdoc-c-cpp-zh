In Listing 5.7, we have created a class, BinaryOperator, which contains a constructor, BinaryOperator, to initialize its two variables. The BinaryOperator class also contains the ShowData() method to display the value of the class variables and overload the functionality of the + (addition) operator. The + operator is overloaded by using the operator keyword. Next, in the Main() method of the MainClass class, the + operator is used to show the addition of the values of the objects of the BinaryOperator class.

Figure 5.8 shows the output of Listing 5.7:

![](bbox=[0.07, 0.2, 0.82, 0.28])

Figure 5.8: Showing the Output of the BinaryOperatorOverload Application

Let’s now learn how to overload a method.

# Overloading a Method

C# allows you to create more than one method with the same name, but with different signatures. Let’s create an application named MethodOverload (also available on the CD) to learn how to overload a method.

Listing 5.8 shows the code of MethodOverload application:

# Listing 5.8: Showing the Code of the MethodOverload Application

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace MethodOverload
{
public class Shape
{
    public void Area(int Side)
    {
        int SquareArea = Side * Side;
        Console.WriteLine("The Area of Square is: "+SquareArea);
    }
    public void Area(int Length, int Breadth)
    {
        int RectangleArea = Length * Breadth ;
        Console.WriteLine("The Area of Rectangle is: " + RectangleArea);
    }
    public void Area(double Radius)
    {
        double CircleArea = 3.14 * Radius * Radius;
        Console.WriteLine("The Area of Circle is: "+CircleArea);
    }
    public double Area(double Base, double Height)
    {
        double TriangleArea = (Base * Height)/2;
        Console.WriteLine("The Area of Triangle is: "+TriangleArea);
        return TriangleArea;
    }
}
class MainClass
{
    static void Main(string[] args)
    {
        Shape shape = new Shape();
        shape.Area(15);
        shape.Area(10, 20);
        shape.Area(10.5);
        shape.Area(15.5, 20.4);
    }
}
```