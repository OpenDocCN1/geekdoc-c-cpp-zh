```
public float CurrentTemperature
{
    get(return _CurrentTemperature;)
    set
    {
        if (value != CurrentTemperature)
        {
            _CurrentTemperature = value;
            if(OnTemperatureChange != null)
            {
                foreach(
                    TemperatureChangeHandler handler in
                    OnTemperatureChange.GetInvocationList() )
                {
                    try
                    {
                        handler(value);
                    }
                    catch(Exception exception)
                    {
                        Console.WriteLine(exception.Message);
                    }
                }
            }
        }
    }
}
private float _CurrentTemperature;
}
```

```
OUTPUT 13.2:
Enter temperature: 45
Heater: On
Error in the application
Cooler: Off
```

This listing demonstrates that you can retrieve a list of subscribers from a delegate's GetInvocationList() method. Enumerating over each item in this list returns the individual subscribers. If you then place each invocation of a subscriber within a try/catch block, you can handle any error conditions before continuing with the enumeration loop. In this sample, even though the delegate listener throws an exception, cooler still receives notification of the temperature change.