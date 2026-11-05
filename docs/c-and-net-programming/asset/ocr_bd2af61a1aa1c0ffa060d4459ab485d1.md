```
d.BDraw();//inherited method

d.DDraw();//own method

}
//Illustration of access modifiers and inheritance scope  2
class Base
{
    protected int var =478 ;
}

class Derived : Base
{
    void Show()
    {
        Base b = new Base();
        Derived d = new Derived();
        b.var = 28; // Error
        d.var = 60; // OK
    }
}



// example2 protected

using System;

class Base
{
    protected int n1;
    protected int n2;
}

class Derived : Base //private inheritance
{
    public static void Main()
    {
        Derived d = new Derived();
        // Direct access to protected members to derived class
        d.n1 = 45;
        d.n2 = 68;
        Console.WriteLine("n1 = {0}, n2 = {1}", d.n1, d.n2);
        Console.ReadLine();
    }
}
```