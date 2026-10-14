# How to use object data sources

This chapter is designed to introduce you to the use of object data sources as an alternative to the Access or SQL data sources that you’ve already learned about. The benefit of using object data sources is that they let you use a three-layer design in which the data access code is kept in data access classes. This lets you separate the presentation code from the data access code, but still lets you use the data binding features of ASP.NET.

To write the data access classes that are used with object data sources, you need to be able to use ADO.NET, which isn’t presented in this book. But even if you don’t understand ADO.NET, this chapter will show you how to use object data sources with existing data access classes. Then, you’ll be able to decide whether you want to use object data sources in your applications and whether you want to learn how to use ADO.NET.

+   An introduction to object data sources ................................ 566
+   How 3-layer applications work in ASP.NET ..................................... 566
+   How to use the ObjectDataSource control ..................................... 568
+   How to configure an ObjectDataSource control ............................... 570
+   How to work with bound controls ............................................. 570
+   A Product List application ................................................ 572
+   The aspx file ................................................................ 574
+   The ProductDB class ........................................................ 576
+   How to create a data access class ........................................... 578
+   How to design a data access class ........................................... 578
+   How to create a select method ............................................... 580
+   How to create update, delete, and insert methods ............................ 582
+   How to use attributes to mark a data access class ........................... 584
+   A Category Maintenance application .......................................... 586
+   The design .................................................................. 586
+   The aspx file ............................................................... 586
+   The code-behind file ....................................................... 590
+   The Category class ......................................................... 592
+   The CategoryDB class ....................................................... 594
+   How to use paging with object data sources .................................. 598
+   How to create an ObjectDataSource control that provides for paging ...... 598
+   How to create a data access class that provides for paging ................ 600
+   Perspective ................................................................ 602