The StreamWriter class provides a Write method to add text to the file. The WriteLine method adds text followed by a new line. Both Write and WriteLine have overloaded versions that write various data types into the file: bool, char, string, int, decimal, and so on. They also provide versions that take a format string and parameters much as the string.Format method does.

The StreamWriter provides one other very important method that I want to cover here: Close. The Close method closes the StreamWriter and its associated file. When you use the Write and WriteLine methods, the StreamWriter may actually buffer its output in memory and only write to the file when it has enough data stored up. The Close method forces the StreamWriter to flush its buffer into the file, and until you call Close the data may not actually be in the file. If your program crashes or ends without calling Close, there's a very good chance that some or all of your text will be lost.

The following code shows how a program could save the contents of a TextBox in a file:

```
```csharp
// Write the file, overwriting it if it exists.
using (StreamWriter memoWriter = new StreamWriter("Memo.txt"))
{
    // Write the file.
    memoWriter.Write(memoTextBox.Text);
    memoWriter.Close();
}
```
```

# ## Reading Files

The StreamReader class lets you easily read text from a file. Like the StreamWriter class, StreamReader provides a constructor that takes a parameter giving the name of the file to open.

The StreamReader constructor throws an exception if the file doesn't exist, so your program should verify that the file is there before you try to open it. For example, you can use the File class's static Exists method to see if the file exists.

The StreamReader class provides a Read method that lets you read from the file one or more bytes at a time, but usually you'll want to use its ReadLine and ReadToEnd methods.

As you may be able to guess, ReadLine reads the next line from the file and returns it as a string. ReadToEnd reads the rest of the file from the current position onward and returns it as a string.

The following code reads the file Memo.txt and displays its contents in a TextBox:

```
```csharp
// Read the file.
using (StreamReader memoReader = new StreamReader("Memo.txt"))
{
    memoTextBox.Text = memoReader.ReadToEnd();
    memoReader.Close();
}
```
```

The StreamReader's EndOfStream property returns true if the reader is at the end of the stream. This is particularly useful when you're reading a stream of unknown length. For example, the program can enter a while loop that uses ReadLine to read lines and continue as long as EndOfStream is false.