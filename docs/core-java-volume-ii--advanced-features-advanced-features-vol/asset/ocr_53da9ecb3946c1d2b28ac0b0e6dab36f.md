```
```xml
<config>
    <entry id="title">
        <font>
            <name>Helvetica</name>
            <size>36</size>
        </font>
    </entry>
    <entry id="body">
        <font>
            <name>Times Roman</name>
            <size>12</size>
        </font>
    </entry>
    <entry id="background">
        <color>
            <red>0</red>
            <green>50</green>
            <blue>100</blue>
        </color>
    </entry>
</config>
```
```

The XML format allows you to express the hierarchy and record repeated elements without contortions.

The format of an XML file is straightforward. It looks similar to an HTML file. There is a good reason for that—both XML and HTML are descendants of the venerable Standard Generalized Markup Language (SGML).

SGML has been around since the 1970s for describing the structure of complex documents. It has been used with success in some industries that require ongoing maintenance of massive documentation—in particular, the aircraft industry. However, SGML is quite complex, so it has never caught on in a big way. Much of that complexity arises because SGML has two conflicting goals. SGML wants to make sure that documents are formed according to the rules for their document type, but it also wants to make data entry easy by allowing shortcuts that reduce typing. XML was designed as a simplified version of SGML for use on the Internet. As is often true, simpler is better, and XML has enjoyed the immediate and enthusiastic reception that has eluded SGML for so long.

> **NOTE:** You can find a very nice version of the XML standard, with annotations by Tim Bray, at www.xml.com/axml/axml.html.

Even though XML and HTML have common roots, there are important differences between the two.