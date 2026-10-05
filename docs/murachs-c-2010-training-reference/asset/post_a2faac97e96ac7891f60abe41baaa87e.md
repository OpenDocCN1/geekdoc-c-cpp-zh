
# The exception classes for file I/O

| Class | Description |
|---|---|
| IOException | The base class for exceptions that are thrown during the processing of the stream, file, or directory. |
| DirectoryNotFoundException | Occurs when a directory or file path can't be found. |
| FileNotFoundException | Occurs when a file can't be found. |
| EndOfStreamException | Occurs when an application attempts to read beyond the end of a stream. |

# Code that uses exception classes

```
string dirPath = @"C:\#2010\Files\";
string filePath = dirPath + "Products.txt";
FileStream fs = null;
try {
    fs = new FileStream(filePath, FileMode.Open);
    // code that uses the file stream
    // to read and write data from the file
}
catch (FileNotFoundException) {
    MessageBox.Show(filePath + " not found.", "File Not Found");
}
catch (DirectoryNotFoundException) {
    MessageBox.Show(dirPath + " not found.", "Directory Not Found");
}
catch (IOException ex) {
    MessageBox.Show(ex.Message, "IOException");
}finally {
    if (fs != null)
        fs.Close();
}
```

# Description

- To catch any I/O exception, you can use the IOException.
- To catch specific I/O exceptions, you can use the exception classes that inherit the IOException class such as the three shown in this figure.

Figure 21-4 How to use the exception classes for file I/O

# How to work with text files

To read and write characters in a text file, you use the StreamReader StreamWriter classes. When working with text files, you often need to use the techniques you learned in chapters 4 and 9 to build and parse strings.

# How to write a text file

Figure 21-5 shows how to use the StreamWriter class to write data to a text file. This class lets you write any data to a text file using the Using and StreamWriter methods. When you use the WriteLine method, a line terminator is automatically added to each record. However, the fields in a record are typically separated by special characters, such as tab characters or pipe characters, and you have to add those characters through code.

The example shows how this works. This code creates a StreamReader object for a file with write-only access it creates a StreamWriter object for each file stream. Next, it uses a foreach loop to write the three properties for each Product object in the List<...> collection named products to the file with pipe characters as separators. (In case you're not familiar with the pipe character, it's available from the same key the backslash key on your keyboard.) For the last property, that way, each record will start on a new line. Finally, after all of the records have been written to the file by the foreach loop, the stream writer and file stream are closed.

Both the Write and WriteLine methods of the StreamWriter class are overloaded to accept any type of data. As a result, if you pass a non-string data type to either of these methods, the method converts the data type to a string that represents the data and then it writes that string to the stream. To do that, these methods automatically call the ToString method of the data type. In other words, you write the decimal value that's stored in the Price property of a product to a text file like this:

```
textOut.WriteLine(product.Price);
```

This has the same effect as coding the statement like this:

```
textOut.WriteLine(product.Price.ToString());
```

# The basic syntax for creating a StreamWriter

```
new StreamWriter(stream)
```

# Common methods of the StreamWriter class

| Method | Description |
|---|---|
| Write(data) | Writes the data to the output stream. |
| WriteLine(data) | Writes the data to the output stream and appends a line terminator (usually a carriage return and line feed). |
| Close() | Closes the StreamWriter and the associated FileStream object. |

# Code that writes data from a collection of Product objects to a text file

```
StreamWriter textOut =
new StreamWriter(
new FileStream(path, FileMode.Create, FileAccess.Write));

foreach (Product product in products)
{
    textOut.Write(product.Code + "|");
    textOut.Write(product.Description + "|");
    textOut.WriteLine(product.Price);
}
textOut.Close();
```

# Description

- You can use the Write and WriteLine methods of a StreamWriter object to write data to a text file. If the data type that is passed to these methods isn't already a string, these methods will call the ToString method of the data type to convert it to a string before they write the data.
- If the fields that make up a record are stored in individual variables, you need to concatenate variables to construct each record and you need to add special characters to delimit each field. However, since the WriteLine method adds the line terminator automatically, you can use it to end each record.

![](img/3148667e42d4db35b3d08576aaa1fa01_690_0.png)

# How to read a text file

Figure 21-6 shows how to use the StreamReader class to read data from a text file. To create a StreamReader object, you can use a FileStream object as the argument. Then, you can use the methods shown in this figure to work with the StreamReader object.

The Read methods let you read a single character, a single line, or all of the data from the current position to the end of the stream. In most cases, you'll use ReadLine to read one record. The example shows how you can use the Peek method to see if there is additional data in the file. After all of the records have been read, the stream reader and file stream are closed. Note in this example that the FileStream object is instantiated in OpenOrCreate mode. Then, if the file exists, it is opened. Otherwise, a new file is created with no records.

# The basic syntax for creating a StreamWriter

new StreamWriter(stream)

# Common methods of the StreamReader class

| Method | Description |
|---|---|
| Peek() | Returns the next character in the input stream without advancing to the next position. If no more characters are available, this method returns -1. |
| Read() | Reads the next character from the input stream. |
| ReadLine() | Reads the next line of characters from the input stream and returns it as a string. |
| ReadToEnd() | Reads the data from the current position in the input stream to the end of the stream and returns it as a string. This is typically used to read the contents of an entire file. |
| Close() | Closes the StreamReader object and the associated FileStream. |

# Code that reads data from a text file into a collection of Product objects

```
StreamReader texId = new StreamReader(new FileStream(path, FileMode.Open, FileAccess.Read));

List<Product> products = new List<Product>();
while (texId.Peek() != -1) {
    string row = texId.ReadLine();
    string[] columns = row.Split('|');
    Product product = new Product();
    product.Code = columns[0];
    product.Description = columns[1];
    product.Price = Convert.ToDecimal(columns[2]);
    products.Add(product);
}
texId.Close();
```

# Description

- Use a StreamReader to read data from a text file. Because the records in text files end with a line terminator (usually a carriage return and a line feed), you'll typically use the ReadLine method to read one record at a time.
- If the fields in a record are delimited by special characters, you need to parse the fields using the techniques of chapter 9.
- You can use the Peek method to determine if the input stream is positioned at the end of the stream.
