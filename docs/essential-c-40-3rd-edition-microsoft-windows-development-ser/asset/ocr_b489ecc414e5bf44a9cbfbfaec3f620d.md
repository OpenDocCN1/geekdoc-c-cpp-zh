```
```csharp
public void OnTemperatureChanged(float newTemperature)
{
    if (newTemperature > Temperature)
    {
        System.Console.WriteLine("Cooler: On");
    }
    else
    {
        System.Console.WriteLine("Cooler: Off");
    }
}
}
```
```

```
```csharp
class Heater
{
    public Heater(float temperature)
    {
        Temperature = temperature;
    }

    public float Temperature
    {
        get{return _temperature;}
        set{Temperature = value;}
    }
    private float _Temperature;
    public void OnTemperatureChanged(float newTemperature)
    {
        if (newTemperature < Temperature)
        {
            System.Console.WriteLine("Heater: On");
        }
        else
        {
            System.Console.WriteLine("Heater: Off");
        }
    }
}
```
```

The two classes are essentially identical, with the exception of the temperature comparison. (In fact, you could eliminate one of the classes if you used a delegate as a method pointer for comparison within the