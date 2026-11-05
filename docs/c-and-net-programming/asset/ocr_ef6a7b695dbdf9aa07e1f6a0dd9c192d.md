```
writer.close();
}
}
```

# Output

(text 'I am an Indian' will be written in File 'fourth.txt')
(again 'I love my country' is appended-added at end in 'fourth.txt')

# Example 5

```
//Illustration of using StreamWriter and StreamReader
using System;
using System.IO;

namespace FileApplication
{
class Program
{
static void Main(string[] args)
{
string[] names = new string[] {"Pune", "Chennai"} ;
using (StreamWriter swr = new StreamWriter("City.txt"))
{
foreach (string s in names)
{
swr.WriteLine(s);
}
}

// Read and show each line from the file.
string line = "";
using (StreamReader srd = new StreamReader("names.txt"))
{
while (((line = srd.ReadLine()) != null)
{
Console.WriteLine(line);
}
}
}
}
}
```