Next, the class that plays the role of broadcaster is:

```
public class Subject
{ // The Broadcaster

    private double val;

    public Subject(double myValue) { val = myValue; }

    // V1: public event ChangeHandler ch;
    public event EventHandler<ValueChangedEventArgs> valueChanged;

    protected virtual void OnValueChanged(ValueChangedEventArgs e)
    {
        if (valueChanged != null) valueChanged(this, e);
    }

    public double Value
    {
        get { return val; }
        set
        {
            if (val == value) return;

            double oldValue = val;
            val = value;

            // Update the subscriber
            OnValueChanged(new ValueChangedEventArgs(oldValue, val));
        }
    }
}
```

All the subscribers will be updated each time the data in the broadcaster changes. For example, a particular case is when there is more than a 10% relative increase in the old value:

```
public static void MyChange(object sender, ValueChangedEventArgs e)
{
    if ((e.newValue - e.oldValue) / e.oldValue > 0.1)
    {
        Console.WriteLine("Alert, more than 10% rise");
    }
    else
    {
        Console.WriteLine("No news, good news");
    }
}
```