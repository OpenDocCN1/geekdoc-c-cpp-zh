One good source of information is Microsoft’s “Control Styles and Templates” web page at msdn.microsoft.com/cc278075 (VS.95).aspx. That page provides links to other pages that describe the features available to different control templates.

These web pages also show the default templates used by the controls. The Button control’s default template is 84 lines long and fairly complicated. Some are much longer and much more complex.

In addition to using Microsoft’s web pages, you can make a control tell you about its template. The ShowTemplate example program displays the default template for a control. In the following figure, that control is the Slider in the upper-left corner. To see the template used by a different kind of control, replace the Slider with a different control, name it Target, and run the program.

![](bbox=[0.22, 0.3, 0.73, 0.56])

The ShowTemplate program uses the following code to display the Target control’s template:

```
private void btnShowTemplate_Click(object sender, RoutedEventArgs e)
{
    XmlWriterSettings writer_settings = new XmlWriterSettings();
    writer_settings.Indent = true;
    writer_settings.IndentChars = "    ";
    writer_settings.NewLineOnAttributes = true;

    StringBuilder sb = new StringBuilder();
    XmlWriter xml_writer = XmlWriter.Create(sb, writer_settings);

    XamlWriter.Save(Target.Template, xml_writer);

    txtResult.Text = sb.ToString();
}
```

![](bbox=[0.18, 0.6, 0.26, 0.7])