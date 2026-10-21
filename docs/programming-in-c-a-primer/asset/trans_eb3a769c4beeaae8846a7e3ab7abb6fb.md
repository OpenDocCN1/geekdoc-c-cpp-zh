

## 程序 8.7 | 可变参数的概念

```
using System;
class Params
{
    static void Parray ( params int [] arr )
    {
        Console.Write("Array elements are:");
        foreach (int i in arr)
            Console.Write(" " + i);
        Console.WriteLine();
    }
    public static void Main()
    {
        int [] x = { 11, 22, 33 };
        Parray ( x );      // call 1
        Parray ( );        // call 2
        Parray ( 100, 200 );   // call 3
    }
}
```

程序 8.7 的输出为：
Array elements are : 11 22 33
Array elements are :
Array elements are : 100 200

请注意，调用 Parray ( ); 和 Parray ( 100, 200 ); 等价于：
Parray ( new int [] { } );
Parray ( new int [] { 100, 200 } );

我们也可以使用类型为 object 的参数数组。示例：

```
public static void Main()
{
    Oarray ( 10, 20, "abc" );
}
static void Oarray ( params object [] x )
{
    foreach ( object i in x )
    {
        Console.WriteLine( i );
    }
}
```

方法 Oarray 被传递一个对象引用的数组。方法调用会自动构建一个对象数组来保存参数，必要时对值类型进行装箱。

请注意，虽然允许使用参数数组与值参数一起使用，但不允许将 params 修饰符与 ref 和 out 修饰符组合使用。

程序 8.8 使用了将任意数量的参数传递给单个方法的概念。此程序计算作为参数传递给方法 avgVal() 的任意一组数字的平均值。

## 程序 8.8 | PARAMS 示例

```
using System;
class Avg
{
    public int avgVal(params int[] intData)
    {
        int sum=0,avg=0;
        if(intData.Length == 0)
        {
            Console.WriteLine("Error: no arguments.");
            return 0;
        }
        for(int i=0; i < intData.Length; i++)
        {
            sum=sum+intData[i];
        }
        avg=sum/intData.Length;
        return avg;
    }
}
public class ParamsSample
{
    public static void Main()
    {
        Avg objAvg = new Avg();
        int average;
        int num1 = 50, num2 = 100;
        // Calling the Average function using two paramters
        average = objAvg.avgVal(num1, num2);
        Console.WriteLine("Average of two parameter values is: " + average);
        // Calling the Average function using three paramters
        average = objAvg.avgVal(num1, num2, 150);
        Console.WriteLine("Average of three parameter values is: " + average);
        // Calling the Average function using six paramters
        average = objAvg.avgVal(30, 40, 50, 60, 70);
        Console.WriteLine("Average of six parameter values is: " + average);
        // Calling the Average function using an integer array
        int[] args = { 25, 35, 45, 55, 65, 75 };
        average = objAvg.avgVal(args);
        Console.WriteLine("Average of parameter values contained in an array is: " + average);
    }
}
```

```
C:\Chapter 8>ParamsSample
Average of two parameter values is: 75
Average of three parameter values is: 100
Average of six parameter values is: 50
Average of parameter values contained in an array is: 50
C:\Chapter 8>
```

## 8.11 方法重载

C# 允许我们创建多个同名但参数列表和定义不同的<|message|> 方法。这称为方法重载。方法重载用于在需要使用不同输入参数执行相似任务时使用。

重载的方法必须在它们接受的参数的数量和/或类型上有所不同。这使编译器能够根据方法调用中的参数类型和数量决定执行哪个定义。请注意，方法的返回类型在重载解析中不起任何作用。

使用方法重载的概念，我们可以设计一个同名但参数列表不同的<|message|> 方法族。例如，重载的 add( ) 方法处理不同类型的数据，如下所示：

```
// Method definitions
int add ( int a, int b ) { ... } //Method1
int add ( int a, int b, int c ) { ... } //Method2
double add ( float x, float y ) { ... } //Method3
double add ( int p, float q ) { ... } //Method4
double add ( float p, int q ) { ... } //Method5
```

```
//Method calls
int m = add ( 5, 10 ); //calls method1
double x = add ( 15, 5.0F ); //calls method4
double x = add ( 1.0F, 2.0F ); //calls method3
int m = add ( 5, 10, 15 ); //calls method2
double x = add ( 2.0F, 10 ); //calls method5
```

- 1. 编译器尝试找到实际参数类型相同且使用该方法的精确匹配。
- 2. 如果找不到精确匹配，则编译器尝试使用隐式转换将实际参数转换为目标类型，然后使用匹配唯一的方法。如果转换产生多个匹配，则编译器将生成错误消息。

程序 8.9 说明了方法重载。

## 程序 8.9 方法重载

```
using System;
class Overloading
{
    public static void Main()
    {
        Console.WriteLine(volume (10));
        Console.WriteLine(volume(2.5 F, 8));
        Console.WriteLine(volume(100L,75,15));
    }
    static int volume ( int x )                 // cube
    {
        return ( x * x * x );
    }
    static double volume ( float r , int h )    // cylinder
    {
        return ( 3.14519 * r * r * h );
    }
    static long volume ( long l , int b , int h )   // box
    {
        return ( l * b * h );
    }
}
```

程序 8.9 的输出为：
1000
157.2595
112500

程序 8.10 演示了 C# 中方法重载的另一个示例，使用 Multiply 方法进行整数和浮点数乘法。

## 程序 8.10 方法重载的另一个示例

```
class Mult
{
    public void Multiply(ref int first, ref int second,out int result)
    {
        result=first*second;
    }
    public void Multiply(ref float first, ref float second,out float result)
    {
        result=first*second;
    }
}
public class MethodsExample
{
    public static void Main()
    {
```

```
```csharp
Mult multObj = new Mult();
int intFirst = 33;
int intSecond = 5;
int intResult=0;
System.Console.WriteLine("Integer Values Before Multiplication:");
System.Console.WriteLine("\tFirst Integer: {0}\n\tSecond Integer: {1}\n\tInteger Result: {2}", intFirst,intSecond,intResult);
multObj.Multiply(ref intFirst, ref intSecond,out intResult);
System.Console.WriteLine("Integer Values After Multiplication:");
System.Console.WriteLine("\tFirst Integer: {0}\n\tSecond Integer: {1}\n\tInteger Result: {2}", intFirst,intSecond,intResult);
float floatFirst = 33f;
float floatSecond = 5f;
float floatResult=0f;
System.Console.WriteLine("\nFloat Values Before Multiplication:");
System.Console.WriteLine("\tFirst Float: {0}\n\tSecond Float: {1}\n\tFloat Result: {2}", floatFirst,floatSecond,floatResult);
multObj.Multiply(ref floatFirst, ref floatSecond,out floatResult);
System.Console.WriteLine("Float Values After Multiplication:");
System.Console.WriteLine("\tFirst Float: {0}\n\tSecond Float: {1}\n\tFloat Result: {2}", floatFirst,floatSecond,floatResult);
```
```

```
```
Integer Values Before Multiplication:
First Integer: 33
Second Integer: 5
Integer Result: 0

Integer Values After Multiplication:
First Integer: 33
Second Integer: 5
Integer Result: 165

Float Values Before Multiplication:
First Float: 33
Second Float: 5
Float Result: 0

Float Values After Multiplication:
First Float: 33
Second Float: 5
Float Result: 165
```
```

## 案例研究

Harish Chadda 先生在艾哈迈达巴德的 B.N. Colony 拥有一栋两层楼的房子。他每年都要向市政公司缴纳房屋的房产税。目前，Chadda 先生每年使用计算器手动计算房产税。因此，计算过程中会出现错误，Chadda 先生无法按时缴纳税款。Chadda 先生还需要花费大量时间

