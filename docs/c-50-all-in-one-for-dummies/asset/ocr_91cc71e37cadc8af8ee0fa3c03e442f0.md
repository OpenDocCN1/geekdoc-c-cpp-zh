# 756 Making an ASMX Service

4. Change the Name to ANewService and the Solution to Chapter 2.

An example is shown in Figure 2-1.

5. Click OK.

This process generates a project that has all the right references for a web application project in ASP.NET and gives you a sample file to start with.

# Analyzing the file setup

Right-click the project and choose Add New Item. The dialog box has all the usuals. The last item is Web Service, which is what you want. Select it and name it TheService.asmx.

Note that although tTheService.asmx (and the usual code-behind file) is created, the map file has only one line in it:

```
<@ WebService Language="C#" CodeBehind="TheService.asmx.cs" Class="ANewService.TheService" %>
```

This is design. Nothing appears in the map file. All the magic is in the code-behind.

![](bbox=[0.25, 0.513, 0.873, 0.843])

Figure 2-1: Make a new web service.