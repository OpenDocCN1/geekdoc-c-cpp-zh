![](bbox=[0.36, 0.08, 0.69, 0.35])

# Figure 17.7: Showing the TestPage.html File in the Solution Explorer

As shown in Figure 17.7, in our case, the ASP.NET and HTML test pages of the SampleSilverlightApplication application are SampleSilverlightApplicationTestPage.aspx and SampleSilverlightApplicationTestPage.html, respectively. The default content of the SampleSilverlightApplicationTestPage.aspx file is given as follows:

```
<%@ Page Language="C#" AutoEventWireup="true" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" >
<head runat="server">
<title>SampleSilverlightApplication</title>
<style type="text/css">
html, body {
    height: 100%;
    overflow: auto;
}
body {
    padding: 0;
    margin: 0;
}
#silverlightControlHost {
    height: 100%;
    text-align:center;
}
</style>
<script type="text/javascript" src="silverlight.js"></script>
<script type="text/javascript">
function onSilverlightError(sender, args) {
    var appSource = "";
    if (sender != null && sender != 0) {
        appSource = sender.getHost().Source;
    }

    var errorType = args.ErrorType;
    var iErrorCode = args.ErrorCode;

    if (errorType == "ImageError" || errorType == "MediaError") {
        return;
    }
```