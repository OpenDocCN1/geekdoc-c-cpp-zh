# Value Types

A value type variable contains the data that it is assigned. For example, when you declare an int (integer) variable and assign a value to it, the variable directly contains that value. And when you assign a value type variable to another, you make a copy of it. The following example makes this clear:

```
class Program
{
    static void Main(string[] args)
    {
        int num1, num2;
        num1 = 5;
        num2 = num1;
        Console.WriteLine("num1 is {0}, num2 is {1}", num1, num2);
        
        num2 = 3;
        Console.WriteLine("num1 is {0}, num2 is {1}", num1, num2);
        Console.ReadLine();
        return;
    }
}
```

The output of this program is:

```
num1 is 5, num2 is 5
num1 is 5, num2 is 3
```

As you can observe, num2 is initially assigned a value of num1 (which is 5). When num2 is later modified to become 3, the value of num1 remains unchanged (it is still 5). This proves that the num1 and num2 each contains a copy of its own value.

Following is another example of value type. Point is a structure that represents an ordered pair of integer x and y coordinates that defines a point in a two-dimensional plane (structure is another example of value types). The Point class is found in the System.Drawing namespace and hence to test the following statements you need to import the System.Drawing namespace.

*Chapter 4 discusses structures in more detail.*

```
Point pointA, pointB;
pointA = new Point(3, 4);
pointB = pointA;
Console.WriteLine("point A is {0}, point B is {1}",
    pointA.ToString(), pointB.ToString());

pointB.X = 5;
pointB.Y = 6;
Console.WriteLine("point A is {0}, point B is {1}",
    pointA.ToString(), pointB.ToString());
```