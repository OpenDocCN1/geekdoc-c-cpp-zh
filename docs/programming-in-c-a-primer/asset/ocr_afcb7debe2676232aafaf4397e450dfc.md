# 334 Programming in C#

```
public delegate void MsgHandler();
class Class1
{
public MsgHandler msg;
public void Show()
{
msg();
}
}
class Class2 : Class1
{
public Class2()
{
msg += MsgHandler(Display);
Show();
}
public void Display()
{
Console.WriteLine ("This is an example of working of a delegate.");
}
}
class Program
{
static void Main(string[] args)
{
Class2 cl = new Class2();
cl.Display();
}
}
```



```
using System;
using System.Collections.Generic;
using System.Text;
namespace debugApp3_chap16
{
delegate void Delegate1(int i);
class DelegateExample
{
string name;
static void Main(string[] args)
{
Delegate1 dl1 = new Delegate1(DelegateExample.Show);
DelegateExample de = new DelegateExample();
de.name = "Display method returns ";
Delegate1 dl2 = new Delegate1(de.Display);
Console.WriteLine (dl1(455));
}
}
}
```