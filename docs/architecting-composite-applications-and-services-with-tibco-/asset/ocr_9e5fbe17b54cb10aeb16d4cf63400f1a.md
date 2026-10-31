# WSDLs and Schemas from Examples

# Sales Order Example

This appendix contains a subset of the schema and WSDL definitions from the Sales Order example. The definitions included here are those corresponding to Figure 9-12, with the exception that the WSDL for the Sales Order Status Interface is not shown.

# Sales Order Service Interface WSDL

The following shows the WSDL for the Sales Order Service Interface showing only the getOrderDetails() operation and its supporting definitions.

```
<?xml version="1.0" encoding="UTF-8"?>
<definitions
    xmlns="http://schemas.xmlsoap.org/wsdl/"
    xmlns:ns="http://enterprise.com/salesOrder/
    salesOrderInterface/
    schema/SalesOrderInterface1"
    xmlns:tns="http://example.com/salesOrder/
    SalesOrderInterface/
    wsdl/salesOrderInterface1"
    xmlns:xsd="http://www.w3.org/2001/XMLSchema"
```