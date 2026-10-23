Finally, an example of use is:

```
static void Main()
{
    // Define broadcaster with empty event
    Subject s = new Subject(3.90);

    // Define target method for broadcaster's event
    s.valueChanged += MyChange;

    // Change propagation method
    s.Value = 24.0;
}
```

This particular example is interesting because it shows how to apply event notification patterns in C#. The code can be adapted to more general situations such as the Observer pattern and applications involving events in graphical user interfaces (GUIs) and database applications.

We now take the final example of the Observer pattern to monitor the passing of time. We implement the code (which we ported from C#) in C++/CLI. To this end, we create a clock class with an embedded changeable time:

```
using namespace System;
using namespace System::Threading;

public ref class TimeChangeEventArgs : EventArgs
{
public:
    DateTime dt;

    TimeChangeEventArgs(DateTime dt)
    { // Constructor
        this->dt = dt;
    }
};

public ref class Clock
{
public:
    // Define event delegate
    delegate void TimeChangeEventHandler(Object^ sender,
    TimeChangeEventArgs^ e);

    // Event variable to store subscribers. Note, it also works
    // without the "event" keyword but with "event".
    event TimeChangeEventHandler^ OnTimeChange;

    void Run()
    {
```