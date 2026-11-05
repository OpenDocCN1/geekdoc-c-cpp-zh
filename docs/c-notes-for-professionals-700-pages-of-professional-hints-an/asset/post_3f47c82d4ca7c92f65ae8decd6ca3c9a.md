
## Chapter 97: File and Stream I/O

| Parameter | Details |
|---|---|
| path | The location of the file. |
| append | If the file exists, true will add data to the end of the file (append), false will overwrite the file. |
| text | Text to be written or stored. |
| contents | A collection of strings to be written. |
| source | The location of the file you want to use. |
| dest | The location you want a file to go to. |

Manages files.

### Section 97.1: Reading from a file using the System.IO.File class

You can use the System.IO.File.ReadAllText function to read the entire contents of a file into a string.

```
string text = System.IO.File.ReadAllText(@"C:\MyFolder\MyTextFile.txt");
```

You can also read a file as an array of lines using the System.IO.File.ReadAllLines function:

```
string[] lines = System.IO.File.ReadAllLines(@"C:\MyFolder\MyTextFile.txt");
```

### Section 97.2: Lazily reading a file line-by-line via an IEnumerable

When working with large files, you can use the System.IO.File.ReadLines method to read all lines from a file into an IEnumerable<string>. This is similar to System.IO.File.ReadAllLines, except that it doesn't load the whole file into memory at once, making it more efficient when working with large files.

```
IEnumerable<string> AllLines = File.ReadLines("file_name.txt", Encoding.Default);
```

*The second parameter of File.ReadLines is optional. You may use it when it is required to specify encoding.*

It is important to note that calling ToArray, ToList or another similar function will force all of the lines to be loaded at once, meaning that the benefit of using ReadLines is nullified. It is best to enumerate over the IEnumerable using a foreach loop or LINQ if using this method.

### Section 97.3: Async write text to a file using StreamWriter

```
// filename is a string with the full path
// true is to append
using (System.IO.StreamWriter file = new System.IO.StreamWriter(filename, true))
{
    // Can write either a string or char array
    await file.WriteAsync(text);
}
```

### Section 97.4: Copy File

### File static class

File static class can be easily used for this purpose.

```
~~~csharp
File.Copy(@"sourcePath\abc.txt", @"destinationPath\abc.txt");
File.Copy(@"sourcePath\abc.txt", @"destinationPath\xyz.txt");
~~~
```

**Remark:** By this method, file is copied, meaning that it will be read from the source and then written to the destination path. This is a resource consuming process, it would take relative time to the file size, and can cause your program to freeze if you don't utilize threads.

### Section 97.5: Writing lines to a file using the System.IO.StreamWriter class

The `System.IO.StreamWriter` class:

> Implements a TextWriter for writing characters to a stream in a particular encoding.

Using the `WriteLine` method, you can write content line-by-line to a file.

Notice the use of the `using` keyword which makes sure the StreamWriter object is disposed as soon as it goes out of scope and thus the file is closed.

```
~~~csharp
string[] lines = { "My first string", "My second string", "and even a third string" };
using (System.IO.StreamWriter sw = new System.IO.StreamWriter(@"C:\MyFolder\OutputText.txt"))
{
    foreach (string line in lines)
    {
        sw.WriteLine(line);
    }
}
~~~
```

Note that the StreamWriter can receive a second `bool` parameter in its constructor, allowing to Append to a file instead of overwriting the file:

```
~~~csharp
bool appendExistingFile = true;
using (System.IO.StreamWriter sw = new System.IO.StreamWriter(@"C:\MyFolder\OutputText.txt", appendExistingFile))
{
    sw.WriteLine("This line will be appended to the existing file");
}
~~~
```

### Section 97.6: Writing to a file using the System.IO.File class

You can use the `System.IO.File.WriteAllText` function to write a string to a file.

```
~~~csharp
string text = "String that will be stored in the file";
System.IO.File.WriteAllText(@"C:\MyFolder\OutputFile.txt", text);
~~~
```

You can also use the `System.IO.File.WriteAllLines` function which receives an `IEnumerable<String>` as the second parameter (as opposed to a single string in the previous example). This lets you write content from an array of lines.

```
~~~csharp
string[] lines = { "My first string", "My second string", "and even a third string" };
System.IO.File.WriteAllLines(@"C:\MyFolder\OutputFile.txt", lines);
~~~
```

## Chapter 98: Networking

### Section 98.1: Basic TCP Communication Client

This code example creates a TCP client, sends "Hello World" over the socket connection, and then writes the server response to the console before closing the connection.

```csharp
// Declare Variables
string host = "stackoverflow.com";
int port = 9999;
int timeout = 5000;

// Create TCP client and connect
using (var _client = new TcpClient(host, port))
using (var _netStream = _client.GetStream())
{
    _netStream.ReadTimeout = timeout;

    // Write a message over the socket
    string message = "Hello World!";
    byte[] dataToSend = System.Text.Encoding.ASCII.GetBytes(message);
    _netStream.Write(dataToSend, 0, dataToSend.Length);

    // Read server response
    byte[] recvData = new byte[256];
    int bytes = _netStream.Read(recvData, 0, recvData.Length);
    message = System.Text.Encoding.ASCII.GetString(recvData, 0, bytes);
    Console.WriteLine(string.Format("Server: {0}", message));
}// The client and stream will close as control exits the using block (Equivalent but safer than calling Close());
```

### Section 98.2: Download a file from a web server

Downloading a file from the internet is a very common task required by almost every application you're likely to build.

To accomplish this, you can use the "System.Net.WebClient" class.

The simplest use of this, using the "using" pattern, is shown below:

```csharp
using (var webClient = new WebClient())
{
    webClient.DownloadFile("http://www.server.com/file.txt", "C:\\file.txt");
}
```

What this example does is it uses "using" to make sure that your web client is cleaned up correctly when finished, and simply transfers the named resource from the URL in the first parameter, to the named file on your local hard drive in the second parameter.

The first parameter is of type "System.Uri", the second parameter is of type "System.String"

You can also use this function as an async form, so that it goes off and performs the download in the background, while your application gets on with something else, using the call in this way is of major importance in modern applications, as it helps to keep your user interface responsive.

When you use the Async methods, you can hook up event handlers that allow you to monitor the progress, so that

### Section 98.4: Basic UDP Client

This code example creates a UDP client then sends "Hello World" across the network to the intended recipient. A listener does not have to be active, as UDP is connectionless and will broadcast the message regardless. Once the message is sent, the client's work is done.

```
byte[] data = Encoding.ASCII.GetBytes("Hello World");
string ipAddress = "192.168.1.141";
string sendPort = 55600;
try
{
    using (var client = new UdpClient())
    {
        IPEndPoint ep = new IPEndPoint(IPAddress.Parse(ipAddress), sendPort);
        client.Connect(ep);
        client.Send(data, data.Length);
    }
}
catch (Exception ex)
{
    Console.WriteLine(ex.ToString());
}
```

Below is an example of a UDP listener to complement the above client. It will constantly sit and listen for traffic on a given port and simply write that data to the console. This example contains a control flag 'done' that is not set internally and relies on something to set this to allow for ending the listener and exiting.

```
bool done = false;
int listenPort = 55600;
using(UdpClient listener = new UdpClient(listenPort))
{
    IPEndPoint listenEndPoint = new IPEndPoint(IPAddress.Any, listenPort);
    while(!done)
    {
        byte[] receivedData = listener.Receive(ref listenPort);

        Console.WriteLine("Received broadcast message from client {0}", listenEndPoint.ToString());

        Console.WriteLine("Decoded data is:");
        Console.WriteLine(Encoding.ASCII.GetString(receivedData)); //should be "Hello World" sent from above client
    }
}
```
