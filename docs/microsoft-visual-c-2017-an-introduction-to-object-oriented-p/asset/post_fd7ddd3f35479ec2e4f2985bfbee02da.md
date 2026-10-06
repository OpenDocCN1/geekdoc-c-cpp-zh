
6. Save the program, and then compile and execute it. Figure 13-11 shows the output when the program is executed several times. When the user enters a sale amount of $1,000 and an S, a 5 percent discount is applied. When the user enters P for the same amount, a 10 percent discount is applied. When the user enters X with the same amount, a 5 percent discount is applied, followed by a 10 percent discount, which produces a net result of a 14.5 percent discount.

```
Enter amount of sale 1000
Enter S for standard discount, P for preferred discount
or X for extreme discount S
New sale amount is $950.00

Enter amount of sale 1000
Enter S for standard discount, P for preferred discount
or X for extreme discount P
New sale amount is $900.00

Enter amount of sale 1000
Enter S for standard discount, P for preferred discount
or X for extreme discount X
New sale amount is $855.00
```

**Figure 13-11** Three executions of the DiscountDelegateDemo2 program

For static methods such as StandardDiscount and PreferredDiscount, encapsulates the method to be called. When creating a class that contains instance methods, you create delegate objects that encapsulate both an instance of the class and a method of the instance. You will create this type of delegate in the next section.

## Declaring and Using Both Custom and Built-in Event Handlers

To declare your own event, use a delegate. An event provides a way for the clients of a class to dictate methods that should execute when an event occurs. The clients identify methods to execute by assigning the delegate with the method that should execute when the event occurs. Just the event handlers that are automatically created in the IDE, each of your own event handler requires two arguments: the object where the event was initiated (the sender) and an EventArgs object that contains event information, or you can use the EventArgs class static field named Empty, which represents an event that contains no data. In other words, using the EventArgs.Empty field simply tells the client that an event has occurred, without specifying details. For example, you can declare a delegate event handler named ChangedEventHandler, as follows:

```csharp
public delegate void ChangedEventHandler(object sender, EventArgs e);
```

The ChangedEventHandler can be any legal identifier you choose. This delegate defines the set of arguments that will be passed to the method that handles the event. The delegate ChangedEventHandler can be used in a client program that handles events.

For example, Figure 13-12 contains the ChangedEventHandler delegate and a simple class that is similar to many classes you have created. The Student class contains just two data fields and will generate an event when the data in either field changes.

```csharp
public delegate void ChangedEventHandler(object sender, EventArgs e);

public class Student
{
    private int idNum;
    private double gpa;
    public event ChangedEventHandler Changed
    {
        get
        {
            return idNum;
        }
        set
        {
            idNum = value;
            OnChanged(EventArgs.Empty);
        }
    }
}
```

**Figure 13-12** The Student class (continues)

(continued)

```csharp
    public double Gpa
    {
        get {
            return gpa;
        }
        set {
            gpa = value;
            OnChanged(EventArgs.Empty);
        }
    }
    private void OnChanged(EventArgs e)
    {
        Changed(this, e);
    }
```

**Figure 13-12** The Student class

The class in Figure 13-12 contains fields that hold an ID number and grade point average for a Student. The first shaded statement in the figure defines a third attribute of the Student—an event named Changed. The declaration for an event looks like a field, but instead of being an int or a double, it is a EventHandler. The event is declared as public, which is conventional, but you can use any accessibility modifier.

The Student event changed (Changed) looks like an ordinary field. However, you cannot assign values to the event as easily as you can to data fields. You can take two actions on an event: you can compose a new delegate onto it using the += operator, and you can remove a delegate from it using the -= operator. For example, to addChanged to Changed of a Student object stu, you would write the following:
`stu.Changed += new EventHandler(StudentChanged);`

In the Student class, each setter accessor assigns a value to the appropriate class instance field. However, when either idNum or gpa changes, the method in the Student class named OnChanged() is also called, using EventArgs.Empty as the argument. The value of EventArgs.Empty is a read-only instance of EventArgs. You can pass it to any method that accepts an EventArgs parameter.

The OnChanged() method calls Changed() using two arguments: a reference to the Student object that was changed and the empty EventArgs object. Calling Changed() is also known as invoking the event.

If no client has wired to the event, the Changed field will be null, rather than referring to the delegate that should be called when the event is invoked. Programmers often check for null before invoking the event, as in the following example:

```csharp
if (Changed != null)
    Changed(this, e);
```

For simplicity, the example in Figure 13-12 does not bother checking for null.

Figure 13-13 shows an EventListener class that listens for Student events. This class contains a Student object that is assigned a value using the parameter to the EventListener class constructor.

```csharp
class EventListener
{
    private Student stu;
    public EventListener(Student student)
    {
        stu = student;
    }
    private void StudentChanged(object sender, EventArgs e)
    {
        WriteLine("Student has changed.");
        WriteLine("ID# {0} GPA {1}", stu.IdNum, stu.Gpa);
    }
}
```

**Figure 13-13** The EventListener class

Figure 13-14 shows a program that demonstrates using the Student and EventListener classes. The program contains a single Main() method, which declares a Student and EventListener. Three assignments are made. Because this program is registered to listen for events from the Student, each change in a data field changes only the value of the data field, but it also executes the StudentChanged method.

```csharp
using System;
using static System.Console;

class DemoStudentEvent
{
    static void Main()
    {
        Student oneStu = new Student();
        EventListener listener = new EventListener(oneStu);
        oneStu.IdNum = 2345;
        oneStu.IdNum = 4567;
        oneStu.Gpa = 3.2;
    }
}
```

**Figure 13-14** The DemoStudentEvent program

```
The student has changed.
ID# 2345 GPA 0
The student has changed.
ID# 4567 GPA 0
The student has changed.
ID# 4567 GPA 3.2
```

**Figure 13-15** Output of the DemoStudentEvent program

## Using the Built-in EventHandler

The C# language allows you to create events using any delegate type. However, the .NET Framework provides guidelines you should follow if you are developing a class that others use. These guidelines indicate that the delegate type for an event should take exactly two parameters: a parameter indicating the source of the event, and an EventArgs parameter that encapsulates any additional information about the event. For events that do not use additional information, the .NET Framework has already defined an appropriate delegate type named EventHandler.

Figure 13-16 shows all the code necessary to demonstrate an EventHandler. Note the following changes from the classes used in the DemoStudentEvent program:

- No delegate is declared explicitly in the Student class.
- In the first statement with shading in the Student class, the event is associated with the built-in delegate EventHandler.
- In the second statement with shading, which appears in the EventListener class, the delegate composition uses EventHandler.
