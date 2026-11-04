To understand the difference, consider the following class definitions — Class1 and Class2:

```
namespace DelegatesVsEvents
{
    class Program
    {
        static void Main(string[] args)
        {
        }
    }

    class Class1
    {
        public delegate void Class1Delegate();
        public Class1Delegate del;
    }

    class Class2
    {
        public delegate void Class2Delegate();
        public event Class2Delegate evt;
    }
}
```

In this code, Class1 exposes a public delegate del, of type Class1Delegate. Class2 is similar to Class1, except that it exposes an event evt, of type Class2Delegate. del and evt each expect a delegate, with the exception that evt is prefixed with the event keyword.

To use Class1, you create an instance of Class1 and then assign a delegate to the del delegate using the "=" operator:

```
static void Main(string[] args)
{
    //---create a delegate---
    Class1Delegate d1 =
        new Class1.Class1Delegate(DoSomething);

    Class1 c1 = new Class1();

    //---assign a delegate to del of c1---
    c1.del = new Class1.Class1Delegate(d1);
}

static private void DoSomething()
{
    //...
}
```