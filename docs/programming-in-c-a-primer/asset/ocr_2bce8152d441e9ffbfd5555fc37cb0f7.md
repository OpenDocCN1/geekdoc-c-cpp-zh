+   (c) static double M3 (int x, int y) {}
+   (d) public double M4 (int x, y ) {}
+   (e) private double M5 (int a, int b) {}

# 16.24 Given the following code segment

```
delegate void D1 ( );
class A
{
    public void M ( ) {}
}
```

which of the following delegate instantiation statements are correct?

+   (a) D1 d1 = new D1 (M);
+   (b) D1 d1 = new (A.M);
+   (c) D1 d1 = new D1 (A,M);
+   (d) D1 D1 = new ((new A () ).M);

# Debugging Exercises

16.1 Debug the following program for demonstrating return types of a method in C#.

```
using System;
using System.Collections.Generic;
using System.Text;
namespace debugApp1_chap16
{
    int ResultDisplay(int i, int j);
    class Show
    {
        public static MathsFunc(int x, int y)
        {
            return ((x * x + 2*x*y + y * y) / (x+y));
        }
    }
    class Program
    {
        static void Main(string[] args)
        {
            ResultDisplay rd = new ResultDisplay(Show.Mathsfync());
            int getResult = rd(1, 2);
            Console.WriteLine("The value of the function is " + getResult);
        }
    }
}
```

16.2 Find errors in the following example of delegates in C#.

```
using System;
using System.Collections.Generic;
using System.Text;
namespace debugApp2_chap16
```