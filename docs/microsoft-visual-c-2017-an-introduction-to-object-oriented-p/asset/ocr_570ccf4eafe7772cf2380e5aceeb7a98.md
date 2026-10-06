to a file, or you could create an Employee class that is similar to many you have seen throughout this book. Figure 14-10 shows a typical Employee class that contains three fields and properties for each.

```
class Employee
{
    public int EmpNum {get; set;}
    public string Name {get; set;}
    public double Salary {get; set;}
}
```

**Figure 14-10** An Employee class

To store Employee data to a persistent storage device, you declare a FileStream object to define the characteristics of the stored file. For example:

```
FileStream outFile = new FileStream(FILENAME,
Mode.Create, FileAccess.Write);
```

The FileStream object is then passed to the constructor of a StreamWriter so that text can be written. For example:

```
StreamWriter writer = new StreamWriter(outFile);
```

You can then use the object writeLine() method to write Employee data to the output stream. You can compose strings using text fields and commas. A block of text within a string that represents an entity or field is a token. Each comma that separates tokens is a delimiter, which is a character used to specify the boundary between data in files. Without a delimiter, the process of separating and interpreting tokens is more difficult. For example, suppose you define a delimiter as a comma in the following statement:

```
const string DELIM = ",";
```

Then, when you write data to a file, you can separate the fields with the comma delimiter using a statement as the following:
writer.WriteLine(emp.EmpNum + DELIM + emp.Name + DELIM + emp.Salary);

A delimiter can be any character that is not needed as part of the data in a file, but a comma is commonly used. A file that contains comma-separated values is often called a CSV file. When a comma cannot be used as a delimiter because commas are needed as characters within the data, sometimes you use the Tab character, the pipe character (|), or a comma within quotation marks is used.

The WriteLine() method ends output with a carriage return. When you use this method to create file output, the automatically appended carriage return becomes the record delimiter.