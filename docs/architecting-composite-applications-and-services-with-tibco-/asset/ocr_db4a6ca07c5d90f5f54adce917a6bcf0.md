# Carrier Schema

```
<?xml version="1.0" encoding="UTF-8"?>
<xsd:schema
    xmlns="http://enterprise.com/fulfillment/schema/carrier"
    xmlns:xsd="http://www.w3.org/2001/XMLSchema"
    xmlns:ns0="http://enterprise.com/address/schema/address1"
    xmlns:ns1="http://enterprise.com/phone/schema/phone1"
    targetNamespace="http://enterprise.com/fulfillment/schema/
      carrier"
    elementFormDefault="unqualified"
    attributeFormDefault="unqualified">
    <xsd:import
        namespace="http://enterprise.com/address/schema/address1"
        schemaLocation="http://enterprise.com/address/schema/address1.0.xsd"/>
    <xsd:import
        namespace="http://enterprise.com/phone/schema/phone1"
        schemaLocation="http://enterprise.com/phone/schema/
          phone1.0.xsd"/>

    <xsd:simpleType name="TrackingNumber">
        <xsd:restriction base="xsd:string">
            <xsd:maxLength value="50"/>
        </xsd:restriction>
    </xsd:simpleType>

    <xsd:simpleType name="CarrierID">
        <xsd:restriction base="xsd:string">
            <xsd:maxLength value="50"/>
        </xsd:restriction>
    </xsd:simpleType>

    <xsd:complexType name="Carrier">
        <xsd:sequence>
            <xsd:element name="carrierID" type="CarrierID"/>
            <xsd:element name="name" type="xsd:string"/>
            <xsd:element name="address" type="ns0:Address"/>
            <xsd:element name="phone" type="ns1:Phone"/>
        </xsd:sequence>
    </xsd:complexType>
</xsd:schema>
```