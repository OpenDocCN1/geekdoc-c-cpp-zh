Using the new lambda expressions in C# 3.0, the preceding event handler can also be written like this:

```
public Form1()
{
    InitializeComponent();
    this.button1.Click += (object sender, EventArgs e) =>
    {
        MessageBox.Show("Button clicked!");
    };
}
```

# Handling Events

Let's take a look at how to handle events using a couple of simple examples. The Timer class (located in the System.Timers namespace) is a class that generates a series of recurring events at regular intervals. You usually use the Timer class to perform some background tasks, such as updating a ProgressBar control when downloading some files from a server, or displaying the current time.

The Timer class has one important event that you need to handle — Elapsed. The Elapsed event is fired every time a set time interval has elapsed.

The following program shows how you can use the Timer class to display the current time in the console window:

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Runtime.Remoting.Messaging;
using System.Timers;
namespace Events
{
    class Program
    {
        static void Main(string[] args)
        {
            Timer t = new Timer(1000);
            t.Elapsed += new ElapsedEventHandler(t_Elapsed);
            t.Start();
            Console.ReadLine();
        }

        static void t_Elapsed(object sender, ElapsedEventArgs e)
        {
            Console.SetCursorPosition(0, 0);
            Console.WriteLine(DateTime.Now);
        }
    }
}
```