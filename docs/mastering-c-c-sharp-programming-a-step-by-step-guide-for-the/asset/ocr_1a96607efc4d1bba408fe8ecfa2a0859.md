```
{
    return x;
}
set
{
    x = value;
    OnPointChanged(); // The method call is added here.
}
}

public double Y
{
    get
    {
        return y;
    }
    set
    {
        y = value;
        OnPointChanged(); // The method call is added here.
    }
}
```

The complete code with the event that has been declared, the method that raises the event, and the code that triggers the event whenever the correct conditions have been met should look like this:

```
using System;
```