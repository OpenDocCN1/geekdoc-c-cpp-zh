```
```xml
</s:schema>
</wsdl:types>
...other definitions...
</definitions>
```
```

These types are all that are required for the SOAP and HTTP requests and responses you saw earlier, and are bound to these operations later in the file. All the types are specified using standard XML schema syntax, for example:

```
```xml
<s:element name="DoSomethingResponse">
  <s:complexType>
    <s:sequence>
      <s:element minOccurs="1" maxOccurs="1" name="DoSomethingResult" type="s:int" />
    </s:sequence>
  </s:complexType>
</s:element>
```
```

This specifies that an element called DoSomethingResponse has a child element called DoSomethingResult that contains an integer. This integer must occur between 1 and 1 times, meaning that it must be included.

If you have access to the WSDL for a web service, you can use it. As you see shortly, this isn't that difficult to do.

After this brief look at SOAP and WSDL, it's time to move on to discuss how you create and consume web services.

# WEB SERVICES

The information about web services in this chapter is divided into two subsections:

+   - “Exposing Web Services,” which addresses writing web services and placing them on web servers.
+   - “Consuming Web Services,” which covers using web services in a client application.

# Exposing Web Services

Web services are exposed by placing code either directly into .asmx files or by referencing web service classes from these files. As with ASP.NET pages, creating a web service in Visual Studio .NET uses the latter method, and you will too for demonstration purposes.

Create a web service project (via File ⇨ New ⇨ Web Site ...) in the C:\ProCSharp\Chapter55 directory and call it PCSWebService1 (see Figure 55-1). Creating a web service project generates a similar set of files as creating a web application project, and you have the same location options for creating the project. In fact, the only difference is that instead of a file called Default.aspx, a file called Service.asmx is created, with code-behind in App_Code/Service.cs.

![](bbox=[0.1, 0.85, 0.8, 0.96])

FIGURE 55-1