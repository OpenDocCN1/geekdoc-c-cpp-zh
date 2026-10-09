# Generics and Delegates

The preceding section discussed that the guideline for defining a type for an event is to use a delegate type of EventHandler<TEventArgs>. In theory, any delegate type could be used, but by convention, the first parameter, sender, is of type object and the second parameter, e, should be of a type deriving from System.EventArgs. One of the more cumbersome aspects of delegates in C# 1.0 was that you had to declare a new delegate type whenever the parameters on the handler changed. Every creation of a new derivation from System.EventArgs (a relatively common occurrence) required the declaration of a new delegate data type that used the new EventArgs-derived type. For example, to use TemperatureArgs within the event notification code in Listing 14.15, it would be necessary to declare the delegate type TemperatureChangeHandler that has TemperatureArgs as a parameter (see Listing 14.16).

# LISTING 14.16: Using a Custom Delegate Type

```
public class Thermostat
{
    public class TemperatureArgs: System.EventArgs
    {
        public TemperatureArgs( float newTemperature )
        {
            NewTemperature = newTemperature;
        }

        public float NewTemperature
        {
            get { return _NewTemperature; }
            set { _NewTemperature = value; }
        }
        private float _NewTemperature;
    }

    public delegate void TemperatureChangeHandler(
        object sender, TemperatureArgs newTemperature);

    public event TemperatureChangeHandler
        OnTemperatureChange;

    public float CurrentTemperature
    {
        ...
    }
    private float _CurrentTemperature;
}
```

2.0