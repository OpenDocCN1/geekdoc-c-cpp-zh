# 14.2 Classes 529

The setManufacturer method has a String parameter named manufact. When the method is called, a string must be passed to it as an argument. In line 9, the value passed to the manufact parameter is assigned to the manufacturer field.

The setModel method appears in lines 12 through 14. The method has a String parameter namedNum. When the method is called, a string must be passed to it as an argument. In line 13, the value passed to the modNum parameter is assigned to the modelNumber field.

TheRetailPrice method has a Real parameter named retail. When the method is called, a Real value must be passed to it as an argument. In line 17, the value passed to the retail parameter is assigned to the retailPrice field.

# Class Listing 14-3

![](bbox=[0.338, 0.497, 0.378, 0.532])

1 Class CellPhone
2 // Field declarations
3 Private String manufacturer
4 Private String modelNumber
5 Private Real retailPrice
6
7 // Method definitions
8 Public Module setManufacturer(String manufact)
9 Set manufacturer = manufact
10 End Module
11
12 Public Module setModelNumber(String modNum)
13 Set modelNumber = modNum
14 End Module
15
16 Public Module setRetailPrice(Real retail)
17 Set retailPrice = retail
18 End Module
19
20 Public Function String getManufacturer()
21 Return manufacturer
22 End Function
23
24 Public Function String getModelNumber()
25 Return modelNumber