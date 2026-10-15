# # Chapter 4 How to Use CSV & SQL Data Readers

In addition to the ServiceReader, we want to have a reader that can read a CSV file and one that can talk to a SQL database. I have already created these readers, so we can add them to our application and see how to use the interface to consolidate our code. Let's start by adding the CSVReader. For this, I'll on the Readers folder and say Add, Existing Project, and then we'll navigate to our Solution folder, which is already open. Then we'll go to PersonReader.CSV and open the PersonReader.CSV.csproj file. So let's go to our PersonReader.CSV project and open the CSVReader class. And then let's collapse to definitions so we can see things a little easier. So here we can see that our CSVReader class implements the IPersonReader interface, and that means that it does have our two methods, GetPeople and GetPerson.

```
```csharp
using [...]

namespace PersonReader.CSV
{
    public class CSVReader : IPersonReader
    {
        public ICSVFileLoader FileLoader { get; set; }

        public CSVReader()[...]

        public IEnumerable<Person> GetPeople()[...]

        public Person GetPerson(int id)[...]

        private List<Person> ParseData(IReadOnlyCollection<string> csvData)[...]
    }
}
```
```

And if we look at the GetPeople method, it looks quite a bit different than what we had in our ServiceReader. It's actually loading