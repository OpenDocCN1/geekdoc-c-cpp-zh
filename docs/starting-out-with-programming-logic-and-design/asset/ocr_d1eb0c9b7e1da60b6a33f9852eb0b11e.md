# 14.3 Using the Unified Modeling Language to Design Classes 537

Figure 14-10 General layout of a UML diagram for a class

| Class name goes here -> |
| Fields are listed here -> |
| Methods are listed here -> |

Following this layout, Figure 14-11 shows a simplified UML diagram for our CellPhone class.

Figure 14-11 Simplified UML diagram for the CellPhone class

| CellPhone |
| manufacturer |
| modelNumber |
| retailPrice |
| CellPhone() |
| setManufacturer() |
| setModelNumber() |
| setRetailPrice() |
| getManufacturer() |
| getModelNumber() |
| getRetailPrice() |

# Data Type and Method Parameter Notation

The UML diagram in Figure 14-1 shows only basic information about the CellPhone class. It does not show details such as data types and the method's parameters. To indicate the data type of a field, place a colon followed by the name of the data type after the name of the field. For example, the manufacturer field in the CellPhone class is a String. It could be listed in the UML diagram as:

manufacturer : String

The return type of a method can be listed in the same manner. After the method's name, place a colon followed by the return type. The CellPhone class's getRetailPrice method returns a Real, so it could be listed in the UML diagram as:

getRetailPrice() : Real

Parameter variables and their data types may be inside a method's parentheses. For example, the CellPhone class's setManufacturer method has a String parameter named manufact, so it could be listed in the UML diagram as:

setManufacturer(manufact : String) *

Figure 14-12 shows the UML diagram for the CellPhone class with data type and parameter notation added to it.