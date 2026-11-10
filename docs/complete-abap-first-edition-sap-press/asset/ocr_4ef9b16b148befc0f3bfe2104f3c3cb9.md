![](bbox=[0.128, 0.106, 0.857, 0.384])

Figure 18.71 Currency/Quantity Fields I

![](bbox=[0.13, 0.445, 0.858, 0.63])

Figure 18.72 External Reference to Currency Field

+   10. To maintain the reference fields, first define a variable of type CUKY in Global Data (see Figure 18.70) and then use it as a reference field in the Currency/Quantity Fields section, as shown in Figure 18.73. For this example, we defined a WAERK global variable of type WAERK.
+   
+       In the Currency/Quantity Fields section, use this global variable as the reference field for the NETWR field in both the header and item structure. Under Data Type, select CURR or QUAN based on the type of field.