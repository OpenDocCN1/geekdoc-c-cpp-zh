# 464 Using the System.NetNamespace

```
private void DownloadWebFile(string remoteFile, string localFile)
{
    FileStream localFileStream = new FileStream(localFile, FileMode.OpenOrCreate);
    WebRequest request = WebRequest.Create(remoteFile);
    request.Method = WebRequestMethods.Http.Get;
    WebResponse response = request.GetResponse();
    Stream responseStream = response.GetResponseStream();
    byte[] buffer = new byte[1024];
    int bytesRead = responseStream.Read(buffer, 0, 1024);
    while (bytesRead > 0)
    {
        localFileStream.Write(buffer, 0, bytesRead);
        }
        bytesRead = responseStream.Read(buffer, 0, 1024);
    }
    localFileStream.Close();
    responseStream.Close();
```

You need to pass a web address, so your subroutine call looks like this:

```
DownloadWebFile("http://your.server.com/sampleFile.bmp",
"C:\sampleFile.bmp");
```

Note the changes, marked as bold. WebRequest is now a WebRequest rather than an FtpWebWebRequest. Also, the Method property of webRequest has been changed to WebRequestMethods.Http.Get. Finally, the Credentials property has been removed because the credentials are no longer required.

# E-mailing a status report

E-mail is a common requirement of networked systems. If you are working in an enterprise environment, you are going to write a larger scale application to handle all e-mail requirements, rather than make individual application-e-mail.

However, if you are writing a stand-alone product, it might require e-mail support. Because I have to be writing a stand-alone application, that is exactly what I'm going to do.

E-mail is a server-based operation, so if you don't have an e-mail server that you can use to send from, this might be hard. Many ISP's no longer allow relaying, which is sending an outgoing message without first having an account and logging in. Therefore, you might have trouble testing this part of the sample.

If you are in a corporate environment, however, you can usually talk to your e-mail administrator and get permission to use the e-mail server. Because outgoing requests are usually harnessed inside the firewall, relaying is often available. To build your e-mail function, follow these steps:

![](bbox=[0.135, 0.355, 0.225, 0.418])