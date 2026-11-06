```
~~~
break;
}
}
}
~~~
```

The code returns the following:

```
~~~
The value of x is 3
~~~
```

The value of variable was initialized to 3. After executing the code, the *case* code for 3 will be matched, hence the statement within its block will be executed. If none of the *case* conditions is true, then the *default* section will be executed. This is demonstrated below:

```
~~~
using System;

public class SwitchStatement
{
public static void Main()
{
int a = 5;

switch (a)
{
    case 1:
    Console.WriteLine("The value of x is 1");
    break;
    case 2:
    Console.WriteLine("The value of x is 2");
    break;
    case 3:
    Console.WriteLine("The value of x is 3");
    break;
~~~
```