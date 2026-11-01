
4. Run the application. The result is shown in Figure 18-1.

![](img/cf72ea860016d2d680fc085fc06f265a_599_0.png)

FIGURE 18-1

## How It Works

This application opens its own .cs file to read from. It does so by navigating two directories up the file structure with the `..` string in the following line:

```
FileStream aFile = new FileStream("../../Program.cs", FileMode.Open);
```

The two lines that implement the actual seeking and reading from a specific point in the file are as follows:

```
aFile.Seek(174, SeekOrigin.Begin);
aFile.Read(byteData, 0, 200);
```

The first line moves the file pointer to byte number 174 in the file. This is the `n` of `namespace` in the Program.cs file; the 174 characters preceding it are the using directives. The second line reads the next 200 bytes into the byte array `byteData`.

Note that these two lines were enclosed in try...catch blocks to handle any exceptions that are thrown:

```
try
{
    aFile.Seek(113, SeekOrigin.Begin);
    aFile.Read(byteData, 0, 100);
}
catch (IOException e)
{
    WriteLine("An IO exception has been thrown!");
    WriteLine(e.ToString());
    ReadKey();
    return;
}
```

Almost all operations involving file I/O can throw an exception of type IOException. All production code should contain error handling, especially when dealing with the file system. The examples in this chapter all include a basic form of error handling.

Once you have the byte array from the file, you need to convert it into a character array so that you can display it to the Console. To do this, use the Decoder class from the System.Text namespace. This class is designed to convert raw bytes into more useful items, such as characters:

```
Decoder d = Encoding.UTF8.GetDecoder();
d.GetChars(byteData, 0, byteData.Length, charData, 0);
```

Like the Read() method, the Write() method has three parameters: a byte array containing the data to write to the file stream, the index in the array to start writing from, and the number of bytes to write.

## The StreamWriter Object

Working with arrays of bytes is not most people's idea of fun — having worked with the FileStream object, you might be wondering whether there is an easier way. Fear not, for once you have a FileStream object, you will usually create a StreamWriter or StreamReader and use its methods to manipulate the file. If you don't need the capability to change the file pointer to any arbitrary position, these classes make working with files much easier.

The StreamWriter class enables you to write characters and strings to a file, with the class handling the underlying conversions and writing to the FileStream object for you.

There are many ways to create a StreamWriter object. If you already have a FileStream object, then you can use it to create a StreamWriter:

```
FileStream aFile = new FileStream("Log.txt", FileMode.CreateNew);
StreamWriter sw = new StreamWriter(aFile);
```

A StreamWriter object can also be created directly from a file:

```
StreamWriter sw = new StreamWriter("Log.txt", true);
```

This constructor takes the filename and a Boolean value that specifies whether to append to the file or create a new one:

- If this is set to false, then a new file is created or the existing file is truncated and then opened.
- If it is set to true, then the file is opened and the data is retained. If there is no file, then a new one is created.

Unlike creating a FileStream object, creating a StreamWriter does not provide you with a similar range of options — other than the Boolean value to append or create a new file, you have no option for specifying the FileMode property as you did with the FileStream class. Nor do you have an option to set the FileAccess property, so you will always have read/write privileges to the file. To use any of the advanced parameters, you must first specify them in the FileStream constructor and then create a StreamWriter from the FileStream object, as you do in the following Try It Out.

## TRY IT OUT Writing Data to an Output Stream: StreamWrite\Program.cs

1. Create a new console application called StreamWrite and save it in the directory C:\BegVCSharp\Chapter18.
2. You will be using the System.IO namespace again, so add the following using directives near the top of the Program.cs file:

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IO;
```

3. Add the following code to the Main() method:

```
static void Main(string[] args)
{
    try
    {
        FileStream aFile = new FileStream("Log.txt", FileMode.OpenOrCreate);
        StreamWriter sw = new StreamWriter(aFile);
        bool truth = true;
        // Write data to file.
        sw.WriteLine("Hello to you.");
        sw.Write($"It is now {DateTime.Now.ToLongDateString()}");
        sw.Write("and things are looking good.");
        sw.Write("More than that,");
        sw.Write($" it's {truth} that C# is fun.");
        sw.Close();
    }
    catch (IOException e)
    {
        WriteLine("An IO exception has been thrown!");
        WriteLine(e.ToString());
        ReadLine();
        return;
    }
}
```

4. Build and run the project. If no errors are found, it should quickly run and close. Because you are not displaying anything on the console, it is not a very exciting program to watch.

5. Go to the application directory and find the Log.txt file. It is located in the StreamWrite\bin\Debug folder because you used a relative path.

6. Open the file. You should see the text shown in Figure 18-3.

![](img/cf72ea860016d2d680fc085fc06f265a_603_0.png)

FIGURE 18-3

## How It Works

This simple application demonstrates the two most important methods of the StreamWriter class, Write() and WriteLine(). Both of them have many overloaded versions for performing more advanced file output, but you used basic string output in this example.

The WriteLine() method writes the string passed to it, followed immediately by a newline character. You can see in the example that this causes the next write operation to begin on a new line:

```
sw.WriteLine("Hello to you.");
```

The Write() method simply writes the string passed to it to the file, without a newline character appended, enabling you to write a complete sentence or paragraph using more than one Write() statement. Just as you can write formatted data to the console, you can also write formatted data to files. For example, you can write out the value of variables to the file using interpolated string parameters:

```
sw.Write($"It is now {DateTime.Now.ToLongDateString()}");
```

DateTime.Now holds the current date; the ToLongDateString() method is used to convert this date into an easy-to-read form.

```
sw.Write("More than that,");
sw.Write($"it's {truth} that C# is fun.");
```

Again, you use interpolated string parameters, this time with Write() to display the Boolean value truth — you set this variable to true earlier, and its value is automatically converted into the string “True” for the formatting.

You can use Write() and format parameters to write comma-separated files:

```
[StreamWriter object].Write($"{100}, {"A nice product"}, {10.50}");
```

In a more sophisticated example, this data could come from a database or other data source.

## The StreamReader Object

Input streams are used to read data from an external source. Often, this will be a file on a disk or network location, but remember that this source could be almost anything that can send data, such as a network application or even the Console.

The StreamReader class is the one that you will be using to read data from files. Like the StreamWriter class, this is a generic class that can be used with any stream. In the next Try It Out, you again construct it around a FileStream object so that it points to the correct file.

StreamReader objects are created in much the same way as StreamWriter objects. The most common way to create one is to use a previously created FileStream object:

```
FileStream aFile = new FileStream("Log.txt", FileMode.Open);
StreamReader sr = new StreamReader(aFile);
```

Like StreamWriter, the StreamReader class can be created directly from a string containing the path to a particular file:

```
StreamReader sr = new StreamReader("Log.txt");
```

## TRY IT OUT Reading Data from an Input Stream: StreamRead\Program.cs

1. Create a new console application called StreamRead and save it in the directory C:\BegVCSharp\Chapter18.
