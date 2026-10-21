# Debugging Exercises

12.1 Find syntax errors in the following program.

```
using System;
using System.Collections.Generic;
using System.Text;
namespace DebugApp1_chap12
{
    class Program
    {
        static void Main(string[] args)
        {
            Name nm = new Name();
            nm.Name1 = "Steve";
            nm.Address = "Washington";
            nm.ShowInfo();
            Console.ReadLine();
        }
    }
class Name
{
    public string Name1;
    public string Address;
    public void ShowInfo()
    {
        Console.WriteLine("{0} is in city {1}", + Name1, + Address);
    }
}
}
```

12.2 Debug the program given below.

```
using System;
using System.Collections.Generic;
using System.Text;
namespace debugApp2_chap12
{
    class Program
    {
        static void Main(string[] args)
        {
            Name obj = new Name();
            obj.showInfo();
        }
    }
}
```