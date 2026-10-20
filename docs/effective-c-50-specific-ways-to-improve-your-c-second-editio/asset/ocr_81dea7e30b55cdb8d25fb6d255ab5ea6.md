Now let’s move on to reference types. Reference types could support the ICloneable interface to indicate that they support either shallow or deep copying. You could add support for ICloneable judiciously because doing so mandates that all classes derived from your type must also support ICloneable. Consider this small hierarchy:

```
class BaseType : ICloneable
{
    private string label = "class name";
    private int[] values = new int[10];

    public object Clone()
    {
        BaseType rVal = new BaseType();
        rVal.label = label;
        for (int i = 0; i < values.Length; i++)
            rVal.values[i] = values[i];
        return rVal;
    }
}

class Derived : BaseType
{
    private double[] dValues = new double[10];

    static void Main(string[] args)
    {
        Derived d = new Derived();
        Derived d2 = d.Clone() as Derived;

        if (d2 == null)
            Console.WriteLine("null");
    }
}
```

If you run this program, you will find that the value of d2 is null. The Derived class does inherit ICloneable.Clone() from BaseType, but that implementation is not correct for the Derived type: It only clones the base type. BaseType.Clone() creates a BaseType object, not a Derived object. That is why d2 is null in the test program—it’s not a Derived object. However, even if you could overcome this problem, BaseType.Clone() could