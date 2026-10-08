```
{
}
}
```

These lines of code will most certainly work, but the end result is nothing at all. You can run the application if you want by pressing the F5 key. This will cause Visual C# Express to compile and then execute your code. On execution, a black window will be launched which will then close again. This is simply because the application does not have any other functions to perform.

In order to make this program actually do something, you need to insert a couple of lines of code. You should enter the following two lines inside the last set of {}.

```
Console.WriteLine("Hello, world!");
```

```
Console.ReadLine();
```

On entering the lines, your entire program should resemble the following.

```
using System;
```

```
using System.Collections.Generic;
```

```
using System.Text;
```

```
namespace ConsoleApplication1
```

```
{
```

```
class Program
```

```
{
```

```
static void Main(string[] args)
```

```
{
```

```
Console.WriteLine("Hello, world!");
```

```
Console.ReadLine();
```