# TABLE 15-1 HTML document properties (continued)

| Property name | Description |
|---|---|
| Theme | Page theme |
| Trace | Indicates whether tracing is enabled |
| TraceMode | Indicates how traces are to be displayed when tracing is enabled |
| UICulture | Determines which resources are loaded for the page |
| Title | Caption for the title bar |

© 2013 Cengage Learning

As with Windows applications, you can set some properties during design using the Properties window by selecting the individual property and either typing a new value or selecting a value from a dropdown list when available. Doing so adds code to the visual interface file containing the HTML tags (.aspx extension). The value typed for the Text property becomes text that you see on the tab for the Web page when it is launched.

Example 15-3 includes the HTML statements modified as a result of the changes in the property values.

# EXAMPLE 15.3

```
<head runat="server">
<title>HTML Controls Example</title>
</head>
```

As shown in Example 15-3, the property change is made to the .aspx file, which is the file containing the HTML tags. When the pair of attribute names and values were automatically placed in the .aspx markup file, the attribute names were written using lowercase characters.