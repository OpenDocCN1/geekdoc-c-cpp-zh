# the basic syntax for creating a StreamReader object

new StreamReader(stream)

# Common methods of the StreamReader class

| Method | Description |
| Peek() | Returns the next available character in the input stream without advancing to the next position. If no more characters are available, this method returns -1. |
| Read() | Reads the next character from the input stream. |
| ReadLine() | Reads the next line of characters from the input stream and returns it as a string. |
| ReadToEnd() | Reads the data from the current position in the input stream to the end of the stream and returns it as a string. This is typically used to read the contents of an entire file. |
| Close() | Closes the StreamReader object and the associated FileStream. |

# Code that reads data from a text file into a collection of Product objects

```
StreamReader texId = new StreamReader(new FileStream(path, FileMode.OpenOrCreate, FileAccess.Read));

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

+   - Use a StreamReader to read data from a text file. Because the records in text files end with a line terminator (usually a carriage return and a line feed), you'll typically use the ReadLine method to read one record at a time.
- If the fields in a record are delimited by special characters, you need to parse the fields using the techniques of chapter 9.
- You can use the Peek method to determine if the input stream is positioned at the end of the stream.

![](bbox=[0.051, 0.936, 0.373, 0.951])