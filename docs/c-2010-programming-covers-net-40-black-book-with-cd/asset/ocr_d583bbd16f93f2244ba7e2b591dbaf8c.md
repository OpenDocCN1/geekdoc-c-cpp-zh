After declaring the delegate type, you need to create a delegate object associated with a method. In Listing 6.10, the Print() method is passed to the EmpStatus() method using the following statement:

```
empdataBase.EmpStatus(Print);
```

At the end, after creating a delegate object, the delegate is called using the following statement:

```
ProcEmp(b);
```

Let’s now learn to create multicast delegates.

# Creating Multicast Delegates

C# provides multicast delegates that allows you to combine several delegate handlers for a given event source into a single linked list. This list, in turn, can be called either directly, under program control, or indirectly, by triggering the event mechanism.

The advantage of using multicast delegates is that you can modify the input to those delegates. For example, if you want to keep track of the chain of events that are assigned to a delegate, you could increment a counter and pass it to the delegate handler as an input argument. Alternatively, you could simply bypass certain handlers, if you know about their processing.

The core of the multicast delegate system is the Combine() method. This method allows you to create the chained link list of delegates to be called when the event is fired. Let’s create a Console application, named MultipleDelegates (also available in the CD), which explains the concept of creating a multicast delegate handler. Listing 6.11 shows the code of the Program.cs file of the MultipleDelegates application:

```
Listing 6.11: Showing the Code of the Program.cs File

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace MultipleDelegates
{
    public class EventHandler1Class
    {
        public static void handleEvent1(string s)
        {
            Console.WriteLine("EventHandler1::HandleEvent1 called [{0]}", s);
        }
    }
    public class EventHandler2Class
    {
        public static void handleEvent1(string s)
        {
            Console.WriteLine("EventHandler2::HandleEvent1 called [{0]}", s);
        }
    }
    public class EventClass
    {
        public delegate void OnEventFired(string s);
        private string fs;
        public OnEventFired evf = null;
        public EventClass(string s)
        {
            fs = s;
            onFireEvent();
        }
        public void setString(string s)
        {
            fs = s;
            onFireEvent();
        }
```