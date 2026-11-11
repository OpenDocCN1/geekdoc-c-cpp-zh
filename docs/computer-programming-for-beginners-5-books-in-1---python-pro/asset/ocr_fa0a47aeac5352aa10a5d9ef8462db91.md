```
Console.WriteLine("Temperature: {0,4:N1} F", x);
}
public void DisplayHexadecimal(int dec)
{
    if (beforeDisplayEvent != null)
        beforeDisplayEvent();

    Console.WriteLine("Hexadecimal: {0:X}", dec);
}
}
}
```

The *DisplayHelper* is a publisher class responsible for publishing the *beforeDisplay* event. After every *display* method, it first checks to determine whether the *beforeDisplayEvent* is not null then it calls the *beforeDisplayEvent()* method.

We now need to create a subscriber. Consider the class given below:

```
using System;

public class MyProgram
{

public static void Main()
{
NumberClass nc = new NumberClass(200);
nc.DisplayMoney();
nc.DisplayNumber();
}
}

class NumberClass
{
    private DisplayHelper _displayHelper;
```