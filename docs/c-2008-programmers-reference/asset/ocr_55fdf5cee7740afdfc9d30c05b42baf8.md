# # Part I: C# Fundamentals

With the modified AlarmClock class, your program will now look like this:

```
```csharp
namespace Events
{
    class Program
    {
        static void c_TimesUp(object sender, AlarmClockEventArgs e)
        {
            Console.WriteLine(DateTime.Now.ToShortTimeString() + ": " + e.Message);
        }

        static void Main(string[] args)
        {
            AlarmClock c = new AlarmClock()
            {
                //---alarm to sound off at 16 May 08, 9.50am---
                AlarmTime = new DateTime(2008, 5, 16, 09, 50, 0, 0),
                Message = "Meeting with customer."
            };
            c.TimesUp += new AlarmClockEventHandler(c_TimesUp);
            c.Start();
            Console.ReadLine();
        }
    }
}
```
```

Figure 7-10 shows the output when the AlarmClock fires the TimesUp event.

![](bbox=[0.384, 0.563, 0.571, 0.602])

Figure 7-10

# # Summary

This chapter discussed what delegates are and how you can use them to invoke other functions, as well as how you can use delegates to implement callbacks so that your application is more efficient and responsive. One direct application of delegates is events, which make GUI operating systems such as Windows possible. One important difference between delegates and events is that you cannot assign a delegate to an event by using the = operator.