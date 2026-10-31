```
<xsd:simpleType name="ShipmentLineID">
    <xsd:restriction base="xsd:string">
        <xsd:maxLength value="50"/>
    </xsd:restriction>
</xsd:simpleType>

<xsd:simpleType name="ShipmentID">
    <xsd:restriction base="xsd:string">
        <xsd:maxLength value="50"/>
    </xsd:restriction>
</xsd:simpleType>

<xsd:simpleType name="ShipmentStatus">
    <xsd:restriction base="xsd:string">
        <xsd:maxLength value="50"/>
    </xsd:restriction>
</xsd:simpleType>

<xsd:complexType name="ShipmentLineItem">
    <xsd:sequence>
        <xsd:element name="quantity" type="xsd:int"/>
        <xsd:element name="shipmentLineID" type="ShipmentLineID"/>
        <xsd:element name="salesOrderLine" type="ns0:SalesOrderLineID"/>
        <xsd:element name="productShipped" type="ns1:ProductRef"/>
    </xsd:sequence>
</xsd:complexType>

<xsd:complexType name="Shipment">
    <xsd:sequence>
        <xsd:element name="shipmentLineItems" type="ShipmentLineItem" maxOccurs="unbounded"/>
        <xsd:element name="trackingNumber" type="ns2:TrackingNumber"/>
        <xsd:element name="shipmentID" type="ShipmentID"/>
        <xsd:element name="status" type="ShipmentStatus"/>
        <xsd:element name="salesOrder" type="ns0:SalesOrderID"/>
        <xsd:element name="carrier" type="ns2:CarrierRef"/>
    </xsd:sequence>
</xsd:complexType>
</xsd:schema>
```

# Sales Order Interface Schema

```
<?xml version="1.0" encoding="UTF-8"?>
<xsd:schema
xmlns="http://enterprise.com/salesOrder/salesOrderInterface/
schema/SalesOrderInterface1"
```