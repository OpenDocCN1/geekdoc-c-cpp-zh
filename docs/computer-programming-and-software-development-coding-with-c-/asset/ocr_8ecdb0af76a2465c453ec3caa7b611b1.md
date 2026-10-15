![](bbox=[0.12, 0.09, 0.91, 0.28])

This is outside the responsibility of our UI code, so we really should move this somewhere else. For that, we will use a factory method to create the appropriate data reader. Let's take a quick look at what a factory method is, and then we'll update the code. To move forward, we will use a factory method for the data reader. A factory method is responsible for getting us an instance of an object. In our case, the factory will return an object that implements our IPersonReader interface. So let's look at this code. The GetReader method returns an IPersonReader.

```
public IPersonReader GetReader(string readerType)
{
    switch (readerType)
    {
        case "Service": return new ServiceReader();
        case "CSV": return new CSVReader();
        case "SQL": return new SQLReader();
        default: throw new ArgumentException(...);
    };
}
```