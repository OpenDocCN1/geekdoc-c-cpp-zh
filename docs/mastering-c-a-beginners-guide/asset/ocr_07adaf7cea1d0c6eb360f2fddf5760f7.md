You will find many constants in the framework itself, e.g., in the Math class, where a constant for pi (3.14) has been defined:

But of course, you should learn how to declare some constants of our own. A constant can be defined in the scope of a method, in the following way:

```
+-
static void Main(string[] args)
{
    const int TheAnswerToLife = 42;
    Console.WriteLine("The answer to life, the universe and everything: " +
TheAnswerToLife);
}
```

However, most constants are declared on the class level so that they can be accessed (but not changed, of course) from all class methods and even outside of the class, depending on the visibility. A constant will act as a static member of the class, meaning that you can access it without instantiating the class. With that in mind, let’s try a complete example where two constants are defined—a private and a public constant:

```
using System;
namespace Constants
{
    class Program
    {
    static void Main(string[] args)
    {
```