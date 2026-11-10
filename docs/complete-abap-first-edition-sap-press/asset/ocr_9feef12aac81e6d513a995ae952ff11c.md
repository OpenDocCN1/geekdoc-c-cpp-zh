# 10.3.2 Structures

We discussed creating structures in Chapter 5, and most of the steps involved in creating structures are similar to those for creating database tables, discussed earlier in this chapter in Section 10.1.1.

A structure can include elementary data types, other structures, or table types. Structures can be nested to any depth. Structures allow you to centrally maintain the fields when similar fields are used in multiple objects (e.g., programs, function module interfaces, etc.).

The components of a structure can include elementary types, reference types, or boxed types, as shown in the available typing methods in Figure 10.56.

![](bbox=[0.148, 0.356, 0.549, 0.613])

Figure 10.56  Typing Method

The following list defines each of these types:

+   - **Elementary types**  
+     *Elementary types* can be defined by referring to a data element from which the type can take the technical and semantic attributes or to a predefined type for which the data type, length, and any decimals are manually assigned.
+   - **Referenced types**  
+     These can be defined as either data references or object references. Data references can be specified by using a data element that defines a data reference or by using a predefined ABAP Data Dictionary type, length, and any decimals.