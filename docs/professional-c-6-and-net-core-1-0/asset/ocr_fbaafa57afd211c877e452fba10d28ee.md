```
pDoubles[50] = 3.0;
```

In this code, you allocate enough memory to hold 20 doubles. Then you set sizeof(double) memory locations, starting at the location given by the start of this memory + 50*sizeof(double) to hold the double value 3.0. Unfortunately, that memory location is way outside the area of memory that you have allocated for the doubles. There is no knowing what data might be stored at that address. At best, you might have used some currently unused memory, but it is equally possible that you might have just overwritten some locations in the stack that were being used to store other variables or even the return address from the method currently being executed. Again, you see that the high performance to be gained from pointers comes at a cost; you need to be certain you know what you are doing, or you will get some very strange runtime bugs.

# QuickArray Example

The discussion of pointers ends with a stackalloc example called QuickArray. In this example, the program simply asks users how many elements they want to be allocated for an array. The code then uses stackalloc to allocate an array of longs that size. The elements of this array are populated with the squares of the integers starting with 0, and the results are displayed on the console (code file QuickArray/Program.cs):

```
using static System.Console;

namespace QuickArray
{
    public class Program
    {
        unsafe public static void Main()
        {
            Write("How big an array do you want? \n>");
            string userInput = ReadLine();
            uint size = uint.Parse(userInput);

            long* pArray = stackalloc long[(int) size];
            for (int i = 0; i < size; i++)
            {
                pArray[i] = i*i;
            }

            for (int i = 0; i < size; i++)
            {
                WriteLine($"Element {i} = {*(pArray + i)}");
            }

            ReadLine();
        }
    }
}
```

Here is the output from the QuickArray example:

```
How big an array do you want?
> 15
```