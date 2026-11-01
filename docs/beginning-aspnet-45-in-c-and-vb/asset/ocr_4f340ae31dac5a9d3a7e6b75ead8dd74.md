```
VB.NET
<OperationContract()>
Public Function NameOfYourMethod(parameters) As DataType
```

```
C#
[OperationContract]
public DataType NameOfYourMethod(parameters)
```

Once you've registered the WCF service in a ScriptManager or ScriptManagerProxy control, you can call the service as follows from your client-side JavaScript:

```
NameOfYourService.NameOfYourMethod(
    parameters, successCallback, errorCallback);
```

# Exercise 4 Solution

To expose and use a page method you need to carry out the following steps:

+   1. Set EnablePageMethods on the ScriptManager to True.
+   2. Define a static (Shared in VB.NET) method in your page and apply the WebMethod attribute like this:
+   3. You call the method in JavaScript through the PageMethods object and define a callback method to handle the result of the method:

```
VB.NET
<WebMethod()>
Public Shared Function NameOfYourMethod(parameters) As DataType
...
End Function
```

```
C#
[WebMethod]
public static DataType NameOfYourMethod(parameters) { ... }
```

```
PageMethods.NameOfYourMethod(parameters, successCallback, errorCallback);
```

# CHAPTER 11

# Exercise 1 Solution

To accomplish this, you first need to set the ClientIDMode of VerticalPanel to Static in the markup of Banner.ascx. This makes it easier to work with the client IDs of the controls inside the panel:

```
<asp:Panel ID="VerticalPanel" runat="server" ClientIDMode="Static">
```

Then you need to add a <span> element just below VerticalPanel with the text Hide Banner. The style attribute changes the mouse cursor into a hand so users understand the text is clickable when