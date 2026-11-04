That’s all there is to it. The `NetworkInformation` class contains a bunch of information about the status of the network, current IP addresses, the gateway being used by the current machine, and more.

![](bbox=[0.154, 0.189, 0.23, 0.261])

Keep in mind that the `NetworkInformation` class will work only on a local machine. If you use this class in an ASP.NET Web Forms application, you will get information about the server.

# Downloading a File from the Internet

You can get a file from the Internet in one of several ways, and one of the most common is by using FTP. The lightweight FTP protocol is favored because it’s secure and supported on many systems.

To build an application that uses FTP, follow these steps:

+   1. **Drag a button onto the form from the Toolbox.**
+   2. **Double-click the button to get the** `Click` **event handler.**
+   3. **Add the required imports,** `System.Net`, `System.Net.Mail`, **and** `System.IO` **to the top of the code.**
+   4. **Create a new subroutine called** `Download_File` **that accepts a remote filename and a local filename as strings.**
+   5. **In the new subroutine, create a new** `FileStream` **(called** `localFileStream`**) and** `FtpWebRequest` **(called** `ftpRequest`**), as shown in Listing 4-1.**

The `FileStream` references a local file and accepts the local file that is passed into the subroutine. The `FtpWebRequest` is the same thing for the remote file.

# Listing 4-1: The DownloadFile Method

```
```csharp
private void DownLoadFile(string remoteFile, string localFile)
{
    FileStream localFileStream = new FileStream(localFile, FileMode.OpenOrCreate);
    FtpWebRequest ftpRequest = (FtpWebRequest)WebRequest.Create(remoteFile);
    ftpRequest.Method = WebRequestMethods.Ftp.DownloadFile;
    ftpRequest.Credentials = new NetworkCredential("Anonymous", "bill@semf.net");
    WebResponse ftpResponse = ftpRequest.GetResponse();
    Stream ftpResponseStream = ftpResponse.GetResponseStream();
    byte[] buffer = new byte[1024];
    int bytesRead = ftpResponseStream.Read(buffer, 0, 1024);
    while (bytesRead > 0)
    {
        localFileStream.Write(buffer, 0, bytesRead);
        bytesRead = ftpResponseStream.Read(buffer, 0, 1024);
    }
    localFileStream.Close();
    ftpResponseStream.Close();
}
```
```