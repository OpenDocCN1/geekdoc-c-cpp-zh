
## Execution Environments

There are times when you want to describe how a collection of components are deployed and wired together. UML has a concept known as an Execution Environment that is ideal for this purpose. Figure A-11 shows an execution environment as it would be displayed in a class diagram. However, all this diagram shows is that the environment exists.

### Execution Environment Structure

The usefulness of the execution environment concept emerges when you show its structure using a composite structure diagram (Figure A-12). Here an environment is shown with three parts: a serviceConsumer (whose type is unspecified), an instance of a BankingService (with the instance unnamed), and an accountsDatabase. Also shown are connectors between the parts, here being used to represent communications channels.

![](img/b8d8132a583ad73d511c4c1bb92e2df7_471_0.png)

**Figure A-11:** *Execution Environments in a Class Diagram*

![](img/b8d8132a583ad73d511c4c1bb92e2df7_471_1.png)

**Figure A-12:** *Composite Structure of an Execution Environment*

### Ports

One thing that is missing from this picture is the Bank Service Interface and an understanding that this is the interface being used by the serviceConsumer. To indicate this, we add what is known as a port to the part (Figure A-13) and associate the Banking Service Interface with the port. The channel from the service consumer is now associated with the port to indicate the use of that interface.

You’ve probably noticed another difference with this diagram: the surrounding frame indicating that this is a production environment has been removed. The display of this frame is optional, and in most of the diagrams used in this book the frame display has been removed.

Adding the port to this diagram did more than just add a box to the diagram: It altered the definition of the Banking Service. The newly added port can be displayed in a class diagram in two ways (Figure A-14). One is to turn on the display of the port region in the class, as has been done on the left. The other is to turn on the display of the port as a square on the margin of the class, as has been done on the right.

A port can be used to indicate either the presentation of a service interface or a reference to a service interface presented by another component.

![](img/b8d8132a583ad73d511c4c1bb92e2df7_472_0.png)

Figure A-13: Adding a Port in the Production Environment

![](img/b8d8132a583ad73d511c4c1bb92e2df7_472_1.png)

Figure A-14: Showing a Port on the Banking Service Class

## Activity Diagrams

### Actions and Control Flow

An activity diagram is used to describe behavior in the form of structured sequences of actions. Figure A-15 shows two actions related by a control flow. The semantics of this is that action A is performed and, when it is completed, action B is performed. The Control Flow arrow is used to indicate this sequencing.

### Artifacts

Actions sometimes require inputs and produce outputs. These are generically referred to as artifacts and are represented as objects in UML. Figure A-16 shows an action consuming one artifact and producing another.

![](img/b8d8132a583ad73d511c4c1bb92e2df7_473_0.png)

Figure A-15: Actions in an Activity Diagram

![](img/b8d8132a583ad73d511c4c1bb92e2df7_473_1.png)

Figure A-16: Artifacts Produced and Consumed by an Action

### Structured Activities

An action can be a structured activity (Figure A-17).

### Call Operation Action

If you need to indicate that the action is the invocation of a specific interface operation, use the Call Operation Action (Figure A-18).

### Decisions, Forks, and Joins

Activity diagrams have some specialized activities. Figure A-19(a) is a decision activity in which either action B or C is performed based on the logical outcome of the decision. In (b), a fork activity indicates that after action D is performed, both actions E and F occur in parallel. In (c), a join activity indicates that after both actions G and H are completed, action I is performed.

![](img/b8d8132a583ad73d511c4c1bb92e2df7_474_0.png)

Figure A-17: Structured Activity

![](img/b8d8132a583ad73d511c4c1bb92e2df7_474_1.png)

Figure A-18: Call Operation Action

![](img/b8d8132a583ad73d511c4c1bb92e2df7_474_2.png)

Figure A-19: Decisions, Forks, and Joins

![](img/b8d8132a583ad73d511c4c1bb92e2df7_476_0.png)

**Figure A-22:** *Swimlanes with Structure*

### Swimlanes with Structure

The component represented by a swimlane may have a sub-structure. If so, you can indicate the actions being performed by the individual sub-components by adding structure to the corresponding swimlane (Figure A-22).

### Collaborations

A collaboration is a structured set of interactions between a number of participants—in other words, a process. In a UML class diagram it is represented by an oval with a dotted-line boundary (Figure A-23). This enables you to indicate, for example, the artifacts that are generated and consumed by various processes.

The behavioral structure of a collaboration is shown using an activity diagram.

![](img/b8d8132a583ad73d511c4c1bb92e2df7_476_1.png)

**Figure A-23:** *Collaboration*

## State Machines

### States and Transitions

State machines consist of states and transitions (Figure A-24). Each machine has an initial state, a final state, and one or more intermediate states. A machine may only be in one state at a time. Transitions between states are labeled with the conditions under which the state transition is taken.

### Composite States

States can be composites of sub-states (Figure A-25). When State A transitions to the composite state, sub-state X is entered as indicated by the arrow from the composite to the sub-state. In this diagram, there are two possible exits from the composite state. If condition 1 occurs at any time, regardless of the sub-state, the machine will transition to state B. If condition 2 occurs while the composite is in sub-state Y, then a transition to State C will occur.

### Orthogonal States

Sometimes a state is really a composition of two state machines. Such states are referred to as orthogonal states (Figure A-26). In the example, when the orthogonal state is entered, it is simultaneously in sub-state K and in sub-state X. Transitions between K and J are independent of transitions between X and Y.

![](img/b8d8132a583ad73d511c4c1bb92e2df7_477_0.png)

Figure A-24: *States and Transitions*

## WSDLs and Schemas from Examples

### Sales Order Example

This appendix contains a subset of the schema and WSDL definitions from the Sales Order example. The definitions included here are those corresponding to Figure 9-12, with the exception that the WSDL for the Sales Order Status Interface is not shown.

### Sales Order Service Interface WSDL

The following shows the WSDL for the Sales Order Service Interface showing only the getOrderDetails() operation and its supporting definitions.

```xml
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
targetNamespace="http://example.com/sales/salesOrder/
  salesOrderInterface/wsdl/salesOrderInterface1"
<import namespace="http://example.com/sales/salesOrder/
  salesOrderInterface/schema/SalesOrderInterface1"
  location="enterprise.com/salesOrder/salesOrderInterface
  /schema/SalesOrderInterface1.xsd"/>

<message name="getSalesOrderDetailRequest">
  <part name="part1" type="ns:GetOrderDetailsRequest"/>
</message>

<message name="getOrderDetailsResponse">
  <part name="part1" type="ns:GetOrderDetailsResponse"/>
</message>

<portType name="SalesOrderInterface">
  <operation name="getOrderDetails">
    <input message="tns:getSalesOrderDetailRequest"/>
    <output message="tns:getOrderDetailsResponse"/>
  </operation>
</portType>
</definitions>
```

### Address Schema

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xsd:schema
  xmlns="http://enterprise.com/address/schema/address1"
  xmlns:xsd="http://www.w3.org/2001/XMLSchema"
  targetNamespace="http://enterprise.com/address/schema/
    address1"
  elementFormDefault="unqualified"
  attributeFormDefault="unqualified">

  <xsd:simpleType name="ISOCountryCode">
    <xsd:restriction base="xsd:int"/>
  </xsd:simpleType>

  <xsd:complexType name="Address">
    <xsd:sequence>
      <xsd:element name="address1" type="xsd:string"/>
      <xsd:element name="address2" type="xsd:string"/>
      <xsd:element name="city" type="xsd:string"/>
      <xsd:element name="state" type="xsd:string"/>
      <xsd:element name="postalCode" type="xsd:string"/>
      <xsd:element name="countryCode" type="ISOCountryCode"/>
```
