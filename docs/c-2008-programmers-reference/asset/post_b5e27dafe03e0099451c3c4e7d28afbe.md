
To understand the difference, consider the following class definitions — Class1 and Class2:

```csharp
namespace DelegatesVsEvents
{
    class Program
    {
        static void Main(string[] args)
        {
        }
    }

    class Class1
    {
        public delegate void Class1Delegate();
        public Class1Delegate del;
    }

    class Class2
    {
        public delegate void Class2Delegate();
        public event Class2Delegate evt;
    }
}
```

In this code, Class1 exposes a public delegate del, of type Class1Delegate. Class2 is similar to Class1, except that it exposes an event evt, of type Class2Delegate. del and evt each expect a delegate, with the exception that evt is prefixed with the event keyword.

To use Class1, you create an instance of Class1 and then assign a delegate to the del delegate using the "=" operator:

```csharp
static void Main(string[] args)
{
    //---create a delegate---
    Class1Delegate d1 =
        new Class1.Class1Delegate(DoSomething);

    Class1 c1 = new Class1();

    //---assign a delegate to del of c1---
    c1.del = new Class1.Class1Delegate(d1);
}

static private void DoSomething()
{
    //...
}
```

Next, define a delegate called AlarmClockEventHandler with the following signature:

```csharp
public delegate void AlarmClockEventHandler(object sender, AlarmClockEventArgs e);
```

Replace the original TimesUp event statement with the following statement, which uses the AlarmClockEventHandler class:

```csharp
//---public event EventHandler TimesUp;---
public event AlarmClockEventHandler TimesUp;
```

Add a Message property to the class so that users of this class can set a message that will be returned by the event when the time is up:

```csharp
public string Message { get; set; }
```

Modify the onTimesUp virtual method by changing its parameter type to the new AlarmClockEventArgs class:

```csharp
protected virtual void onTimesUp(AlarmClockEventArgs e)
{
    if (TimesUp != null)
        TimesUp(this, e);
}
```

Finally, modify the t_Elapsed event handler so that when you now call the onTimesUp() method, you pass in an instance of the AlarmClockEventArgs class containing the message you want to pass back to the event handler:

```csharp
void t_Elapsed(object sender, ElapsedEventArgs e)
{
    if (DateTime.Now >= this.AlarmTime)
    {
        onTimesUp(new AlarmClockEventArgs(this.Message));
        t.Stop();
    }
}
```

Here's the complete program:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Timers;

public class AlarmClockEventArgs : EventArgs
{
    public AlarmClockEventArgs(string Message)
    {
        this.Message = Message;
    }
    public string Message { get; set; }
}

public delegate void AlarmClockEventHandler(object sender, AlarmClockEventArgs e);

class AlarmClock
{
    Timer t;

    public event AlarmClockEventHandler TimesUp;
    protected virtual void onTimesUp(AlarmClockEventArgs e)
    {
        if (TimesUp != null)
            TimesUp(this, e);
    }

    public DateTime AlarmTime { get; set; }
    public string Message { get; set; }

    public AlarmClock()
    {
        t = new Timer(100);
        t.Elapsed += new ElapsedEventHandler(t_Elapsed);
    }

    public void Start()
    {
        t.Start();
    }

    void t_Elapsed(object sender, ElapsedEventArgs e)
    {
        if (DateTime.Now >= this.AlarmTime)
        {
            onTimesUp(new AlarmClockEventArgs(this.Message));
            t.Stop();
        }
    }
}
```

With the modified AlarmClock class, your program will now look like this:

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

Figure 7-10 shows the output when the AlarmClock fires the TimesUp event.

![](img/a977a875c7c627b45d939729705a252e_263_0.png)

Figure 7-10

### Summary

This chapter discussed what delegates are and how you can use them to invoke other functions, as well as how you can use delegates to implement callbacks so that your application is more efficient and responsive. One direct application of delegates is events, which make GUI operating systems such as Windows possible. One important difference between delegates and events is that you cannot assign a delegate to an event by using the = operator.

## Strings and Regular Expressions

One of the most common data types used in programming is the string. In C#, a string is a group of one or more characters declared using the string keyword. Strings play an important part in programming and are an integral part of our lives — our names, addresses, company names, email addresses, web site URLs, flight numbers, and so forth are all made up of strings. To help manipulate those strings and pattern matching, you use regular expressions, sequences of characters that define the patterns of a string. In this chapter, then, you will:

- Explore the System.String class
- Learn how to represent special characters in string variables
- Manipulate strings with various methods
- Format strings
- Use the StringBuilder class to create and manipulate strings
- Use Regular Expressions to match string patterns

### The System.String Class

The .NET Framework contains the System.String class for string manipulation. To create an instance of the String class and assign it a string, you can use the following statements:

```csharp
String str1;
str1 = "This is a string";
```

C# also provides an alias to the String class: string (lowercase “s”). The preceding statements can be rewritten as:

```csharp
string str1; //---equivalent to String str1;---
str1 = "This is a string";
```

Here's this code's output:

```
T
h
i
s

i
s

a

s
t
r
i
n
g
```

### Escape Characters

Certain characters have special meaning in strings. For example, strings are always enclosed in double quotation marks, and if you want to use the actual double-quote character in the string, you need to tell the C# compiler by "escaping" the character's special meaning. For instance, say you need to represent the following in a string:

"I don't necessarily agree with everything I say." Marshall McLuhan

Because the sentence contains the double-quote characters, simply using a pair of double-quotes to contain it will cause an error:

```csharp
//---error---
string quotation;
quotation = ""I don't necessarily agree with everything I say." Marshall McLuhan";
```

To represent the double-quote character in a string, you use the backslash (`\`) character to turn off its special meanings, like this:

```csharp
string quotation =
    "\"I don't necessarily agree with everything I say.\" Marshall McLuhan";
Console.WriteLine(quotation);
```

The output is shown in Figure 8-1.

![](img/a977a875c7c627b45d939729705a252e_266_0.png)

Figure 8-1

A backslash, then, is another special character. To represent the `C:\Windows` path, for example, you need to turn off the special meaning of `\` by using another `\`, like this:

```csharp
string path = "C:\\Windows";
```

What if you really need two backslash characters in your string, as in the following?

```
"\\servername\\path"
```

In that case, you use the backslash character twice, once for each of the backslash characters you want to turn off, like this:

```csharp
string UNC = "\\\\servername\\path";
```

In addition to using the `\` character to turn off the special meaning of characters like the double-quote (`"`) and backslash (`\`), there are other escape characters that you can use in strings.

One common escape character is the `\n`. Here's an example:

```csharp
string lines = "Line 1\nLine 2\nLine 3\nLine 4\nLine 5";
Console.WriteLine (lines);
```

The `\n` escape character creates a newline, as Figure 8-2 shows.

![](img/a977a875c7c627b45d939729705a252e_267_0.png)

Figure 8-2

You can also use `\t` to insert tabs into your string, as the following example shows (see also Figure 8-3):

```csharp
string column1 = "Column 1\tColumn 2\tColumn 3\tColumn 4";
string column2 = "\t5\t25\t125";
Console.WriteLine(column1);
Console.WriteLine(column2);
```

![](img/a977a875c7c627b45d939729705a252e_267_1.png)

Figure 8-3
