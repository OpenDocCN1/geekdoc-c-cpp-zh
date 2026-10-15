```
custs.Add(new Customer(1007, "Puja", 20));
custs.Add(new Customer(1008, "Francesco", 30));
custs.Add(new Customer(1009, "Feni", 40));
custs.Add(new Customer(10010, "Era", 50));
custs.Add(new Customer(10011, "Raj", 60));
custs.Add(new Customer(10012, "Vijay", 20));
custs.Add(new Customer(10013, "Mudita", 30));
custs.Add(new Customer(10014, "Nancy", 40));
custs.Add(new Customer(10015, "Kapil", 10));
return custs;
```

Now, let’s run the application by pressing the F5 key on the keyboard. The output of the application is as shown in Figure 27.6:

![](bbox=[0.2, 0.27, 0.8, 0.65])

Figure 27.6: Displaying the Output of the LINQtoObject Application

# Creating a LINQ to XML Application

As you have already learned, LINQ to XML is a LINQ-enabled XML programming interface that enables you to work with XML. You can display the XML data as your output by using LINQ to XML. You can use LINQ to XML to run queries against XML data. Let’s create an application, LINQtoXML (available on the CD), in which you can actually work with the XML in .NET Framework. Now, modify the code in the Default.aspx page, as shown in Listing 27.6:

# Listing 27.6: Showing the Code for the Default.aspx Page

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs"
Inherits="_Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
```