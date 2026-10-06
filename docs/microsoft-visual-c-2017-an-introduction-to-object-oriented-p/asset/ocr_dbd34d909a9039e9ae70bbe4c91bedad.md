# CHAPTER 5 Looping

![](bbox=[0.137, 0.105, 0.723, 0.373])

**Figure 5-2** Flowchart for the logic of a while loop whose body executes four times

Figure 5-3 shows a C# program that uses the same logic as diagramed in Figure 5-2. After the declarations, the shaded while expression compares number to LIMIT. The two statements execute each time the Boolean expression is true are blocked using a pair of curly braces. Figure 5-4 shows the output.

```
using static System.Console;
class FourHellos
{
    static void Main()
    {
        int number = 1;
        const int LIMIT = 5;
        while(number < LIMIT)
        {
            WriteLine("Hello");
            number = number + 1;
        }
    }
}
```

**Figure 5-3** A program that contains a while loop whose body executes four times