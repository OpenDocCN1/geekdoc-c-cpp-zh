# Value Types in the lock Statement

C# supports a lock statement for synchronizing code. The statement compiles down to System.Threading.Monitor's Enter() and Exit() methods. These two methods must be called in pairs. Enter() records the unique reference argument passed so that when Exit() is called with the same reference, the lock can be released. The trouble with using value types is the boxing. Therefore, each time Enter() or Exit() is called, a new value is created on the heap. Comparing the reference of one copy to the reference of a different copy will always return false, so you cannot hook up Enter() with the corresponding Exit(). Therefore, value types in the lock statement are not allowed.

Listing 8.7 points out a few more runtime boxing idiosyncrasies and Output 8.2 shows the results.

# LISTING 8.7: Subtle Boxing Idiocyncrasies

```
interface IAngle
{
    void MoveTo(int hours, int minutes, int seconds);
}

struct Angle : IAngle
{
    // ...

    // NOTE: This makes Angle mutable, against the general
    // guideline
    public void MoveTo(int hours, int minutes, int seconds)
    {
        _Hours = hours;
        _Minutes = minutes;
        _Seconds = seconds;
    }
}

class Program
{
    static void Main()
```