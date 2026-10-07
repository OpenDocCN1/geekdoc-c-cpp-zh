# Coding the Publish–Subscribe Pattern with Multicast Delegates

chain. Now, after the first delegate’s method returns, the second delegate is called. To remove delegates from a delegate chain, use the == operator, as shown in Listing 14.6 with Output 14.1.

# Listing 14.6: Using the += and -= Delegate Operators

```
//...
Thermostat thermostat = new();
Heater heater = new(60);
Cooler cooler = new(80);

Action<float> delegate1;
Action<float> delegate2;
Action<float> delegate3;

delegate1 = heater.OnTemperatureChanged;
delegate2 = cooler.OnTemperatureChanged;

Console.WriteLine("Invoke both delegates:");
delegate3 = delegate1;
delegate3 += delegate2;
delegate3(90);

Console.WriteLine("Invoke only delegate2");
delegate3 -= delegate1;
delegate3!(30);
//...
```

Invoke both delegates:
Heater: Off
Cooler: On
Invoke only delegate2
Cooler: Off

You can also use the + and - operators to combine delegates, as shown in Listing 14.7.

# Listing 14.7: Using the + and - Delegate Operators

```
//...
Thermostat thermostat = new();
Heater heater = new(60);
Cooler cooler = new(80);
```