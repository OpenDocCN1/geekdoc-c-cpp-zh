

## 承运商 Schema

```xml
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

    <xsd:complexType name="CarrierRef">
        <xsd:sequence>
            <xsd:element name="carrierID" type="CarrierID"/>
            <xsd:element name="name" type="xsd:string"/>
        </xsd:sequence>
    </xsd:complexType>
</xsd:schema>
```

## 客户 Schema

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xsd:schema
xmlns="http://enterprise.com/customer/schema/customer1"
xmlns:xsd="http://www.w3.org/2001/XMLSchema"
xmlns:tns2="http://enterprise.com/address/schema/address1"
xmlns:tns3="http://enterprise.com/phone/schema/phone1"
targetNamespace="http://enterprise.com/customer/schema/
customer1"
elementFormDefault="unqualified"
attributeFormDefault="unqualified">
<xsd:import namespace="http://enterprise.com/address/schema/
address1"
schemaLocation="http://enterprise.com/address/schema/
address1.0.xsd"/>
<xsd:import namespace="http://enterprise.com/phone/schema/
phone1"
schemaLocation="http://enterprise.com/phone/schema/
phone1.0.xsd"/>

<xsd:simpleType name="CustomerID">
    <xsd:restriction base="xsd:string">
        <xsd:maxLength value="50"/>
    </xsd:restriction>
</xsd:simpleType>

<xsd:complexType name="CustomerRef">
    <xsd:sequence>
        <xsd:element name="customerID" type="CustomerID"/>
        <xsd:element name="name" type="xsd:string"/>
    </xsd:sequence>
</xsd:complexType>

<xsd:complexType name="Customer">
    <xsd:sequence>
        <xsd:element name="customerID" type="CustomerID"/>
        <xsd:element name="name" type="xsd:string"/>
```

```xml
<xsd:complexType name="Product">
    <xsd:sequence>
        <xsd:element name="productID" type="SKU"/>
        <xsd:element name="name" type="xsd:string"/>
        <xsd:element name="manufacturer"
            type="ns0:ManufacturerRef"/>
    </xsd:sequence>
</xsd:complexType>

<xsd:complexType name="ProductRef">
    <xsd:sequence>
        <xsd:element name="productID" type="SKU"/>
        <xsd:element name="name" type="xsd:string"/>
    </xsd:sequence>
</xsd:complexType>
</xsd:schema>
```

## 订单履行 Schema

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xsd:schema
    xmlns="http://enterprise.com/fulfillment/orderFulfillment/schema/orderFulfillment1"
    xmlns:xsd="http://www.w3.org/2001/XMLSchema"
    xmlns:ns0="http://enterprise.com/sales/salesOrder/schema/SalesOrder1"
    xmlns:ns1="http://enterprise.com/product/schema/product1"
    xmlns:ns2="http://enterprise.com/fulfillment/carrier/schema/carrier1"
    targetNamespace="http://enterprise.com/fulfillment/orderFulfillment/schema/orderFulfillment1"
    elementFormDefault="unqualified"
    attributeFormDefault="unqualified">
    <xsd:import
        namespace="http://enterprise.com/sales/salesOrder/schema/SalesOrder1"
        schemaLocation="http://enterprise.com/sales/salesOrder/schema/salesOrder1.0.xsd"/>
    <xsd:import namespace="http://enterprise.com/product/schema/product1"
        schemaLocation="http://enterprise.com/product/schema/product1.0.xsd"/>
    <xsd:import
        namespace="http://enterprise.com/fulfillment/carrier/schema/carrier1"
        schemaLocation="http://enterprise.com/fulfillment/carrier/schema/carrier1.0.xsd"/>

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

## 销售订单接口 Schema

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xsd:schema
xmlns="http://enterprise.com/salesOrder/salesOrderInterface/
schema/SalesOrderInterface1"
xmlns:xsd="http://www.w3.org/2001/XMLSchema"
xmlns:ns0="http://enterprise.com/sales/salesOrder/schema/
SalesOrder1"
targetNamespace="http://enterprise.com/salesOrder/
salesOrderInterface/schema/SalesOrderInterface1"
elementFormDefault="unqualified"
attributeFormDefault="unqualified">
<xsd:import
namespace="http://enterprise.com/sales/salesOrder/schema/
SalesOrder1"
schemaLocation="http://enterprise.com/schema/
salesOrder1.0.xsd"/>

<xsd:complexType name="GetOrderDetailsRequest">
<xsd:sequence>
<xsd:element name="orderID" type="ns0:SalesOrderID"/>
</xsd:sequence>
</xsd:complexType>

<xsd:complexType name="GetOrderDetailsResponse">
<xsd:sequence>
<xsd:element name="salesOrder" type="ns0:SalesOrder"/>
</xsd:sequence>
</xsd:complexType>
</xsd:schema>
```

## 销售订单 Schema

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xsd:schema
xmlns="http://enterprise.com/sales/salesOrder/schema/
SalesOrder1"
xmlns:xsd="http://www.w3.org/2001/XMLSchema"
xmlns:ns0="http://enterprise.com/address/schema/address1"
xmlns:ns1="http://enterprise.com/product/schema/product1"
targetNamespace="http://enterprise.com/sales/salesOrder/
schema/SalesOrder1"
elementFormDefault="unqualified"
attributeFormDefault="unqualified">
<xsd:import namespace="http://enterprise.com/address/schema/
address1"
schemaLocation="http://enterprise.com/address/schema/
address1.0.xsd"/>
<xsd:import namespace="http://enterprise.com/product/schema/
product1"
schemaLocation="http://enterprise.com/product/schema/
product1.0.xsd"/>
```

## 索引

- A
  - 在命名结构中避免使用缩写，188
  - 抽象架构模式
    - 概述，8
    - 作为参考架构，13
    - 用于展示依赖关系，112
  - 抽象定义，WSDL，176–177
  - 服务抽象
    - 概述，122–123
    - 服务规范内容，124
    - 服务规范文档，420
    - 服务规范示例，128
  - 抽象服务，174–175, 178–180
  - Accept Queue Size 参数，HTTP 连接器，345
  - Acceptor 线程，HTTP 连接器，345–347
  - 访问控制，服务联邦，402–403, 405–406
  - 访问点，143, 405–406
  - 访问速率，基准测试结果，332–334
  - 账户与资金转账，Payment Manager，77–81
  - Acknowledge Mode 参数，JMS 流程启动器，360–361
  - 在命名结构中避免使用首字母缩略词，188
  - 操作，Hawk 规则，51–52
  - 操作，UML 活动图，437–439
  - Activation Limit 调优参数，ActiveMatrix BusinessWorks，367–368
  - ActiveMatrix 部署选项，31–33
  - ActiveMatrix 适配器。另请参阅 TIBCO ActiveMatrix® Adapters
  - ActiveMatrix Administrator。另请参阅 TIBCO ActiveMatrix® Administrator
  - ActiveMatrix 复合实现，307–308
  - ActiveMatrix® Decisions。另请参阅 TIBCO ActiveMatrix® Decisions
  - ActiveMatrix 服务总线故障转移，390–391
  - ActiveMatrix Lifecycle Governance Framework。另请参阅 TIBCO ActiveMatrix® Lifecycle Governance Framework
  - ActiveMatrix Product Portfolio。另请参阅 TIBCO ActiveMatrix® Product Portfolio
  - ActiveMatrix® Service Bus。另请参阅 TIBCO ActiveMatrix® Service Bus
  - ActiveMatrix® Service Grid。另请参阅 TIBCO ActiveMatrix® Service Grid
  - UML 活动图
    - 记录流程模式映射，7
    - 记录触发行为，113
    - 符号参考，437–440
  - 适配器。另请参阅 TIBCO ActiveMatrix® Adapters
    - 通过适配器的外部访问交互，38–39
    - Hawk，53–54, 56
    - 使用适配器的单线程解决方案，276
    - TIBCO Adapter for Files，62–63
    - TIBCO Adapter for IBM i，61–62
  - 地址位置
    - SOAP，200–202
    - 其中变量的值，209–210
    - 对 SOAP 端点进行版本管理，168
  - 地址模式，WSDL 销售订单示例，444–445
  - AeRMsg 格式，BusinessConnect，64
  - 聚合，UML 类图符号，430–431
  - 警报，Hawk 事件服务，55
  - AMI（应用程序微代理接口）接口，Hawk Agent，56
  - 附录
    - 服务规范文档，423
    - 解决方案架构文档，417
  - 复合应用程序，304
  - 《Architecting BPM Solutions with TIBCO®》（即将出版，TIBCO Press 和 Addison-Wesley），426
  - 《Architecting Complex Event Processing Solutions with TIBCO®》（即将出版，TIBCO Press 和 Addison-Wesley），425

