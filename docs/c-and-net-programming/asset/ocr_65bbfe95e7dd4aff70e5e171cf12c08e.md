# 17.2 XML Syntax

![](bbox=[0.0901, 0.1178, 0.913, 0.3312])

**Fig. 17.2.1 XML syntax**

# 1. XML Declaration

```
```xml
<?xml version="1.0"?>
<note>
<to>RaviW</to>
<from>AviiW</from>
<heading>Greetings</heading>
<body>Wish you happy 2017</body>
</note>
```
```

The first line in the document :

*The XML declaration* should always be included. It defines the XML version of the document, here it is 1.0 specification of XML.

The XML document can optionally have an XML declaration. It is written as below :

`<?xml version="1.0" encoding="UTF-8"?>`

Where *version* is the XML version and *encoding* specifies the character encoding used in the document.

# Rules for XML declaration

+   - The XML declaration is case sensitive and must begin with "<?xml>" where "xml" is written in lower-case.
+   - If document contains XML declaration, then it strictly needs to be the first statement of the XML document.
+   - The XML declaration strictly needs be the first statement in the XML document.
+   - An HTTP protocol can override the value of *encoding* that is put in the XML declaration.

```
```xml
<?xml version="1.0"?>
```
```