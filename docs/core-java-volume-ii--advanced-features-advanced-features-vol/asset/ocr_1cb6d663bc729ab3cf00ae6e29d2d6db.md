# Listing 3.3 read/config.xml

```
```xml
<?xml version="1.0"?>
<!DOCTYPE config SYSTEM "config.dtd">
<config>
  <entry id="background">
    <construct class="java.awt.Color">
      <int>55</int>
      <int>200</int>
      <int>100</int>
    </construct>
  </entry>
  <entry id="currency">
    <factory class="java.util.Currency">
      <string>USD</string>
    </factory>
  </entry>
</config>
```
```

# Listing 3.4 read/config.dtd

```
```dtd
<!ELEMENT config (entry)*>

<!ELEMENT entry (string|int|boolean|construct|factory)*>
<!ATTLIST entry id ID #IMPLIED>

<!ELEMENT construct (string|int|boolean|construct|factory)*>
<!ATTLIST construct class CDATA #IMPLIED>

<!ELEMENT factory (string|int|boolean|construct|factory)*>
<!ATTLIST factory class CDATA #IMPLIED>
<!ATTLIST factory method CDATA "getInstance">

<!ELEMENT string (#PCDATA)>
<!ELEMENT int (#PCDATA)>
<!ELEMENT boolean (#PCDATA)>
```
```

# Listing 3.5 read/config.xsd

```
```xml
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema">
  <xsd:element name="config">
    <xsd:complexType>
      <xsd:sequence>
        <xsd:element name="entry" minOccurs="0" maxOccurs="unbounded">
          <xsd:complexType>
            <xsd:group ref="Object"/>
            <xsd:attribute name="id" type="xsd:ID"/>
          </xsd:complexType>
```
```

(Continues)