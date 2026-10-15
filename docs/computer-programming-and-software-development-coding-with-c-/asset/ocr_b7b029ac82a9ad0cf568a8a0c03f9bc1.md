this sample, we will update our application to look in Configuration to decide which data reader to use, in the code, we will update the controller to use the new Configuration, and we will update the user interface, the view, to add a new link to our screen. This will give us the ability to switch to a different data reader without recompiling our application. We only need to update the Configuration to use a new data reader. Here we are back in Visual Studio with the extensibility solution open. This code is in the same state that we left it in the previous demonstration, three links that use three different data readers to get data.

```
```csharp
using PersonReader.CSV;
using PersonReader.Interface;
using PersonReader.Service;
using PersonReader.SQL;
using System;

namespace PersonReader.Factory
{
    public class ReaderFactory
    {
        public IPersonReader GetReader(string readerType)
        {
            switch (readerType)
            {
                case "Service": return new ServiceReader();
                case "CSV": return new CSVReader();
                case "SQL": return new SQLReader();
                default:
                    throw new ArgumentException($"Invalid reader type: {readerType}");
            }
        }
    }
}
```
```

We will change this so the data reader is selected based on what is in a Configuration file. This will let us change the behavior of our application without recompiling it, so let's start by adding Configuration. We do need to know what the valid values are, and for that, we can look in our factory method. So let's go to the PersonReader.Factory project and open the ReaderFactory. This shows us our three current valid values, Service, CSV, and SQL. So let's go