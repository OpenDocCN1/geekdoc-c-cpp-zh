In the statement, `trans` is an XSLT or a Simple Transformation (ST) program. If XML is provided for both the source and result, the XML document will be transformed into a different XML document using the specified transformation.

A parameter list, structure, or internal table can be used to serialize or deserialize data into ABAP data objects. Because XSLT expects data in XML format for transformation and can't interpret ABAP data directly, the ABAP data is implicitly transformed into ABAP Serialization XML (asXML) before it's processed by XSLT.

# 19.7.1 Serialization

During serialization, ABAP data is first converted to asXML using a predefined transformation ID, the result of which is used as the source for XSLT. If ID itself is used for the ID in the transformation, then the asXML itself is output without further transformation.

Listing 19.5 shows sample code to transform the data in an ABAP structure to XML. The `DISPLAY_XML_STRING` function module displays the XML output, as shown in Listing 19.5.

```
DATA : BEGIN OF sflight,
         carrid TYPE s_carr_id VALUE 'AA',
         connid TYPE s_conn_id VALUE '0017',
       END OF sflight.
DATA xmlstr TYPE xstring.

CALL TRANSFORMATION ID
  SOURCE FLIGHT = sflight
  RESULT XML xmlstr.

CALL FUNCTION 'DISPLAY_XML_STRING'
  EXPORTING xml_string = xmlstr.
```

**Listing 19.5** XML Transformation

![](bbox=[0.148, 0.724, 0.615, 0.868])

**Figure 19.125** XML Output