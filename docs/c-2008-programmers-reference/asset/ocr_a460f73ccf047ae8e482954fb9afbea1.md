```
ws.GetSignatureCompleted +=
    new EventHandler<Signature.ServiceReference1.
GetSignatureCompletedEventArgs>(ws_GetSignatureCompleted);
//---calls the web service method---
ws.GetSignatureAsync();
}
catch (Exception ex)
{
    txtStatus.Text = ex.ToString();
}
}
```

Here, you call the Web service to retrieve the saved signature. When the Web Service call returns, the ws_GetSignatureCompleted event handler will be called.

Code the ws_GetSignatureCompleted event handler as follows:

```
void ws_GetSignatureCompleted(
object sender,
Signature.ServiceReference1.GetSignatureCompletedEventArgs e)
{
    txtStatus.Text = "Signature loaded from WS!";
    DrawSignature(e.Result);
}
```

Save the Signature project. In Solution Explorer, right-click on the SignatureWebSite project and select Add Silverlight Link (see Figure 19-77).

![](bbox=[0.38, 0.74, 0.78, 0.9])

Figure 19-77