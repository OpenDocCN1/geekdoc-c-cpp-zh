Dialog programming involves creating a collection of screens, flow logic, menu bars, and ABAP code that when linked together builds an application. At the end of this chapter, you'll know how to create transactions and develop dialog programs.

# 12 Dialog Programming

Dialog programming is very different from the reporting program creation you've seen so far in this book. Whereas reports traditionally provide read-only access to a database, dialog programs allow a user to create and update data. For example, if the user needs an application to create a sales order in which he wants to capture information about the order and save it to the database, we need to develop a dialog program to enable the user to capture various information about the order, validate the data, and save it to the database. However, both report programs and dialog programs can work interchangeably, and both can be used to both read and update data.

Dialog programs are also known as transactions. Dialog programs involve various screens that are called to capture or show data to the user. These programs are accessed through the SAP GUI and form the user interface. Using dialog programs, the user can navigate between screens and interact with the SAP ERP system.

In this chapter, we'll discuss screen processing and how to create various screen elements using Screen Painter. As previously discussed in Chapter 3, Screen Painter is an ABAP Workbench tool used to design dialogs in the SAP system. We'll also discuss how to create various screen objects (GUI statuses) such as menus, buttons on the application toolbar, and so on via the Menu Painter. GUI statuses extend the functionality of the application.

When the screen is processed, the ABAP runtime environment triggers specific screen events. We'll start our discussion in this chapter with an introduction to screen events in Section 12.1, and we'll examine the different attributes of a screen in Section 12.2.