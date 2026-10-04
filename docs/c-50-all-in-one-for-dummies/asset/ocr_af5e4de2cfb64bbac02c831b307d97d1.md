# 462 Using the System.Net Namespace

That's all there is to it. The NetworkInformation class contains a bunch of information about the status of the network, current IP addresses, the gateway being used by the current machine, and more.

![](bbox=[0.157, 0.191, 0.223, 0.256])

Keep in mind that the NetworkInformation class will work only on a local machine. If you use this class in an ASP.NET Web Forms application, you will get information about the server.

# Downloading a file from the Internet

You can get a file from the Internet in several of ways, and one of the most common is using FTP. The lightweight FTP protocol is favored because it's secure and supported on many systems.

To build an application that uses FTP, follow these steps:

+   1. Drag a button onto it from the Toolbox.

+   2. Double-click the button to get the Click event handler.

+   3. Add the required imports, System.Net, System.Net.Mail, and System.IO to the top of the code.

+   4. Create a new subroutine called DownloadFile that accepts a remote filename and a filename as strings.

+   5. In the new subroutine, create a new FileStream (called localFileStream) and FTPWebRequest (called ftpRequest) as shown in Listing 4-1.

The FileStream references a local file and accepts the local file that is passed into the subroutine. The FtpWebRequest is the thing for the remote file.

# Listing 4-1: The DownloadFile Method

```
private void DownloadFile(string remoteFile, string localFile)
{
    FileStream localFileStream = new FileStream(localFile, FileMode.OpenCreate);
    FTPWebRequest ftpRequest = (FTPWebRequest)WebRequest.Create(remoteFile);
    ftpRequest.Method = WebRequest.Methods.DownloadFile;
    ftpRequest.Credentials = new NetworkCredential("Anonymous", "bill@sempf.net");
    Stream ftpResponse = ftpRequest.GetResponseStream();
    byte[] buffer = new byte[1024];
    int bytesRead = ftpResponse.Read(buffer, 0, 1024);
    while (bytesRead > 0)
    {
        localFileStream.Write(buffer, 0, bytesRead);
        bytesRead = ftpResponse.Read(buffer, 0, 1024);
    }
    localFileStream.Close();
    ftpResponse.Close();
}
```

* Note