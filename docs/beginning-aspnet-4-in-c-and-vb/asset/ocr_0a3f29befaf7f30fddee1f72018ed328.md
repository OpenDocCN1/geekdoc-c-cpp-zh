In this example, you connect a StreamReader class you from the System.IO namespace to the network stream. This allows you to obtain data from the stream as text through the use of higher-level methods, such as ReadLine(). This is an excellent example of the point made in Chapter 29, "Manipulating Files and the Registry," about the benefits of abstracting data movement into the concept of a stream.

Figure 24-1 shows the results of running this sample code.

![](bbox=[0.12, 0.26, 0.78, 0.68])

FIGURE 24-1

The WebClient class also has an OpenWrite() method. This method returns a writable stream for you to send data to a URI. You can also specify the method used to send the data to the host; the default method is POST. The following code snippet assumes a writable directory named accept on the local machine. The code will create a file in the directory with the name newfile.txt and the contents Hello World:

```
```csharp
WebClient webClient = new WebClient();
Stream stream = webClient.OpenWrite("http://localhost/accept/newfile.txt", "PUT");
StreamWriter streamWriter = new StreamWriter(stream);
streamWriter.WriteLine("Hello World");
streamWriter.Close();
```
```

# Uploading Files

The WebClient class also features UploadFile() and UploadData() methods. You use these methods when you need to post an HTML form or to upload an entire file. UploadFile() uploads a file to a specified location given the local filename, whereas UploadData() uploads binary data supplied as an array of bytes to the specified URI (there is also a DownloadData() method for retrieving an array of bytes from a URI):

```
```csharp
WebClient client = new WebClient();
client.UploadFile("http://www.ourwebsite.com/NewFile.htm",
    "C:\WebSiteFiles\NewFile.htm");
byte[] image;
// code to initialize image so it contains all the binary data for
// some .jpg file
client.UploadData("http://www.ourwebsite.com/NewFile.jpg", image);
```
```