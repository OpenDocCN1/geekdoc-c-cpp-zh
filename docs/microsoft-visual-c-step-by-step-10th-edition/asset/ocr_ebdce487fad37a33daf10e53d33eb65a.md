```
TextReader reader = new StreamReader(filename);
string line;
while ((line = reader.ReadLine()) is not null)
{
    Console.WriteLine(line);
}
reader.Close();
```