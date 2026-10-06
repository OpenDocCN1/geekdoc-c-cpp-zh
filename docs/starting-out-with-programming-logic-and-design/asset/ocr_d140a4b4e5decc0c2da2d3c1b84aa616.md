# Figure 14-12 UML diagram for the CellPhone class with data type and parameter notation

| CellPhone |
| --- |
| manufacturer : String |
| modelNumber : String |
| retailPrice : Real |
| CellPhone(manufact : String, retail : Real) |
| modelNum : String, retail |
| setManufacturer(manufact : String) |
| setModelNumber(modNum : String) |
| setRetailPrice(retail : Real) : String |
| getManufacturer() : String |
| getModelNumber() : String |
| getRetailPrice() : Real |

# Access Specification Notation

The UML diagrams in Figures 14-11 and 14-12 list all of the fields and methods in the CellPhone class do not indicate which are private and which are public. In a UML diagram, you have the option to place a - before a field or method name to indicate that it is private, or a + to indicate that it is public. Figure 14-13 shows the UML diagram modified to indicate this notation.

# Figure 14-13 UML diagram for the CellPhone class with access specification notation

| CellPhone |
| --- |
| – manufacturer : String |
| – modelNumber : String |
| – retailPrice : Real |
| + CellPhone(manufact : String,
| + modelNum : String, retail |
| + setManufacturer(manufact : String) |
| + setModelNumber(modNum : String) |
| + setRetailPrice(retail : Real) |
| + getManufacturer() : String |
| + getModelNumber() : String |
| + getRetailPrice() : Real |

# Checkpoint

+   14.14 The typical UML diagram for a class has three sections. What appears in these three sections?
14.15 Suppose a class has a field named description. The field's data type is String. How would you indicate the field's data type in a UML diagram?
14.16 What symbols do you use in a UML diagram to indicate private and public access specification?