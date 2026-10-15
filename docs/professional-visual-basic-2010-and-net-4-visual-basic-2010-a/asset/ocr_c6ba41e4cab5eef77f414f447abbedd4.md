In the preceding XSLT file, the XSLT elements are marked in bold. These elements perform operations on the source XML file containing a serialized FilmOrderList object, and generate the appropriate HTML file. Your generated file contains a table (marked by the table tag, <table>) that contains a set of rows (each row marked by a table row tag, <tr>). The columns of the table are contained in table data tags, <td>. Each row containing data (an individual movie order from the serialized object, FilmOrderList) is generated using the XSLT element, for-each, to traverse each <FilmOrder> element within the source XML document. In this case, a shorthand for the location of the FilmOrder element was used: //FilmOrder returns all FilmOrder elements, regardless of their depth in the XML file. Alternately, you could have specified the full path using FilmOrderList/FilmOrders/FilmOrder here.

The individual columns of data are generated using the value-of XSLT element, in order to query the elements contained within each <FilmOrder> element (<Title>, <id>, and <Quantity>).

The code in Sub Main() to create a displayable XML file using the Xs1CompiledTransform object is as follows:

```
Dim xslt As New Xs1CompiledTransform
Dim outputFile As String = "...\output.html"

xslt.Load("...\displayorders.xslt")
xslt.Transform("...\filmorama.xml", outputFile)

Process.Start(outputFile)
```

Code snippet from Transformation

This consists of only five lines of code, with the bulk of the coding taking place in the XSLT file. The previous code snippet created an instance of a System.Xml.Xs1.Xs1CompiledTransform object named xslt. The Load method of this class is used to load the XSLT file you previously reviewed, DisplayOrders.xslt. The Transform method takes a source XML file as the first parameter, which in this case was a file containing a serialized FilmOrderList object. The second parameter is the destination file created by the transform (output.html). The Start method of the Process class is used to display the HTML file in the system default browser. This method launches a process that is best suited for displaying the file provided. Basically, the extension of the file dictates which application will be used to display the file. On a typical Windows machine, the program used to display this file is Internet Explorer, as shown in Figure 9-2.

![](bbox=[0.52, 0.46, 0.885, 0.7])

FIGURE 9-2

> Don't confuse displaying this HTML file with ASP.NET. Displaying an HTML file in this manner takes place on a single machine without the involvement of a Web server.

As demonstrated, the backbone of the System.Xml.Xs1 namespace is the Xs1CompiledTransform class. This class uses XSLT files to transform XML documents. Xs1CompiledTransform exposes the following methods and properties:

+   XmlResolver — This get/set property is used to specify a class (abstract base class, XmlResolver) that is used to handle external references (import and include elements within the style sheet). These