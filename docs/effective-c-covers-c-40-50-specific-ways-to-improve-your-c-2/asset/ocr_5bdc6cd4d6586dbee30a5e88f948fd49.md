```
public class WeatherData
{
    public double Temperature { get; set; }
    public int WindSpeed { get; set; }
    public Direction WindDirection { get; set; }
    public override string ToString()
    {
        return string.Format(
            "Temperature = {0}, Wind is {1} mph from the {2}",
            Temperature, WindSpeed, WindDirection);
    }
}
```

```
public class WeatherDataStream : IEnumerable<WeatherData>
{
    private Random generator = new Random();

    public WeatherDataStream(string location)
    {
        // elided
    }

    private IEnumerator<WeatherData> GetElements()
    {
        // Real implementation would read from
        // a weather station.
        for (int i = 0; i < 100; i++)
            yield return new WeatherData
            {
                Temperature = generator.NextDouble() * 90,
                WindSpeed = generator.Next(70),
                WindDirection = (Direction)generator.Next(7)
            };
    }
```

```
#region IEnumerable<WeatherData> Members
public IEnumerator<WeatherData> GetEnumerator()
{
    return getElements();
}
#endregion
```