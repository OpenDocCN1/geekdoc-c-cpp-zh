# Listing 3.12 (Continued)

```
```java
 */
class EmployeeReader implements XMLReader
{
    private ContentHandler handler;

    public void parse(InputSource source) throws IOException, SAXException
    {
        InputStream stream = source.getByteStream();
        var in = new BufferedReader(new InputStreamReader(stream));
        String rootElement = "staff";
        var atts = new AttributesImpl();

        if (handler == null) throw new SAXException("No content handler");

        handler.startDocument();
        handler.startElement("", rootElement, rootElement, atts);
        String line;
        while ((line = in.readLine()) != null)
        {
            handler.startElement("", "employee", "employee", atts);
            var t = new StringTokenizer(line, "|");

            handler.startElement("", "name", "name", atts);
            String s = t.nextToken();
            handler.characters(s.toCharArray(), 0, s.length());
            handler.endElement("", "name", "name");

            handler.startElement("", "salary", "salary", atts);
            s = t.nextToken();
            handler.characters(s.toCharArray(), 0, s.length());
            handler.endElement("", "salary", "salary");

            atts.addAttribute("", "year", "year", "CDATA", t.nextToken());
            atts.addAttribute("", "month", "month", "CDATA", t.nextToken());
            atts.addAttribute("", "day", "day", "CDATA", t.nextToken());
            handler.startElement("", "hiredate", "hiredate", atts);
            handler.endElement("", "hiredate", "hiredate");
            atts.clear();

            handler.endElement("", "employee", "employee");
        }

        handler.endElement("", rootElement, rootElement);
        handler.endDocument();
    }

}
```
```