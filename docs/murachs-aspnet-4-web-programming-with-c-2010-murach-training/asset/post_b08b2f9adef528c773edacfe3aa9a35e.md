
## The design of the Cart page

![](img/c024ccf88e28c30c07dd410d4342288f_100_0.png)

### Description

- The Cart page displays the items in the shopping cart in a list box control. To load the list box, it uses the shopping cart information that's saved in session state by the Order page.
- The user can select any item in the shopping cart and then click the Remove Item button to remove the item from the cart. If the user clicks the Remove Item button without selecting an item, a message is displayed that asks the user to select the item to be removed.
- To remove all the items from the cart, the user can click the Empty Cart button.
- After reviewing the cart, the user can click the Continue Shopping button to return to the Order page and order additional products.
- If the user clicks the Check Out button, a message is displayed that indicates that the check out function hasn't been implemented yet.

Figure 3-2 The Cart page of the Shopping Cart application

## The files and folders used by the Shopping Cart application

Figure 3-3 summarizes the files and folders used by the Shopping Cart application. By default, Visual Studio 2010 places new web page files and their related code-behind files in the application's root folder, but other files used by the application are placed in special folders. The first table in this figure lists the most commonly used special folders. Besides these folders, though, you can also create your own folders. For example, it's common to create an Images folder to store any image files used by the application.

The App_Code, App_Data, App_Themes, and Bin folders are used for certain types of files required by the application. For instance, class files (other than the class files for web pages) are stored in the App_Code folder, and any database files used by the application are stored in the App_Data folder. In contrast, the App_Themes folder is used to store any theme data, which you'll learn more about in chapter 11. And the Bin folder is used to store any compiled assemblies, such as class libraries, that are used by the application.

Note that the special folders aren't available to the application through normal means. For example, you can't store an image file in the App_Data folder and then refer to it in the ImageUrl attribute of an Image control. The only exception is that you can refer to the App_Data folder in a connection string for an Access database.

The second table in this figure lists the specific files and folders that make up the Shopping Cart application. As you can see, the App_Code folder contains three class files named CartItem.cs, CartItemList.cs, and Product.cs that define the CartItem, CartItemList, and Product classes required by the application. And the App_Data folder contains an Access database named Halloween.mdb.

The Shopping Cart application also includes a folder named Images. This folder includes just one image file, banner.jpg, which provides the banner that's displayed at the top of each page. However, this folder also includes a subfolder named Products, which includes a separate image file for each product in the Products table of the database. Because the Products table includes a column named ImageFile that provides the file name for each product's image, the application can display the correct image for each product.

Finally, the root folder for the application contains two files for each of the application's web pages: one for the page itself, the other for the code-behind file. For example, the Cart.aspx file contains the aspx code that defines the Cart page, and the Cart.aspx.cs file is the code-behind file that contains the C# code for the Cart page.

Please note that the root folder also contains a web.config file. This file is added automatically when you create an application.

## The Solution Explorer for the Shopping Cart application

![](img/c024ccf88e28c30c07dd410d4342288f_102_0.png)

### Special folders used in ASP.NET 4 applications

| Folder | Description |
|---|---|
| App_Code | Non-page class files that are compiled together to create a single assembly. |
| App_Data | Database files used by the application. |
| App_Themes | Themes used by the application. |
| Bin | Compiled code used by the application. |

### Files in the Shopping Cart application

| Folder | File | Description |
|---|---|---|
| App_Code | CartItem.cs | A class that represents an item in the shopping cart. |
| App_Code | CartItemList.cs | A class that represents the shopping cart. |
| App_Code | Product.cs | A class that represents a product. |
| App_Data | Halloween.mdb | The Access database file that contains the Halloween database. |
| Images | Banner.jpg | An image file that displays the banner used at the top of each page. |
| Images\Products | (multiple) | Contains an image file for each product in the database. |
| (root) | Cart.aspx | The aspx file for the Cart page. |
| (root) | Cart.aspx.cs | The code-behind file for the Cart page. |
| (root) | Order.aspx | The aspx file for the Order page. |
| (root) | Order.aspx.cs | The code-behind file for the Order page. |
| (root) | web.config | The application configuration file. |

### Description

- The Images folder is a custom folder that I created to hold the image files used by this application. The Products subfolder contains the image files for the products in the Products table of the Halloween database.

## How to add a class to a web site

As you just saw in the previous figure, the Shopping Cart application requires three business classes named Product, CartItem, and CartItemList. To use these classes with the web site, you can use the techniques presented in figure 3-4.

To add a new class to the web site, you use the Add New Item dialog box shown in this figure. From this dialog box, you select the Class template, enter the name for the class, and then click the Add button. When you do, Visual Studio will create a declaration for the new class. Then, you can complete the class by coding its properties and methods.

Before you create a new class, you'll typically add the special **App_Code** folder to the web site so that you can add the class directly to this folder. However, you can also add a new class without first adding the **App_Code** folder. To do that, just select Add New Item from the shortcut menu for the project. Then, when you click the Add button to add the class, Visual Studio will display a dialog box that indicates that the class should be placed in an **App_Code** folder and asks if you want to place the class in that folder. If you click the Yes button on this dialog box, Visual Studio will create the **App_Code** folder and place the new class in it.

To add an existing class to a web site, you use the Add Existing Item command as described in this figure. Then, the class file that you select is copied to your web site.

If the existing class you want to use is stored in a *class library*, you can use that class by adding a reference to the class library to your web site as described in this figure. One of the advantages of using class libraries is that the source code is stored in a single location. Then, if you need to modify a class, you can just modify the code in the class library and it will be available to any web sites that use that library. In contrast, if you copy a class to each web site that uses it, you have to modify the code in each web site.

### The dialog box for adding a new class to the App_Code folder

![](img/c024ccf88e28c30c07dd410d4342288f_104_0.png)

### Two ways to open the Add New Item dialog box

- Right-click the App_Code folder in the Solution Explorer if it already exists, and then choose Add New Item from the shortcut menu.
- Click on the App_Code folder in the Solution Explorer to select it, and then choose the Website→Add New Item command.

### How to add a new class to a web site

- From the Add New Item dialog box, select the Class template, name the class, and click the Add button. Visual Studio will create the declaration for the class.
- If you try to add a class directly to the project instead of to the App_Code folder, Visual Studio will warn you that the class should be placed in the App_Code folder and ask you if you'd like to place the class in this folder. If you click the Yes button, Visual Studio will create the App_Code folder if necessary and place the class in this folder.

### How to add an existing class to a web site

- To add a class from another project to a web site, right-click the App_Code folder in the Solution Explorer and select Add Existing Item. Then, locate the class file you want to add, select it, and click the Add button. The file is copied to your project.

### How to use a class that's part of a class library

- Right-click the project in the Solution Explorer and select Add Reference from the shortcut menu. Click the Browse tab in the dialog box that's displayed, and then locate and select the .dll file for the class library you want to use. The class library is added to the project's Bin folder, which is created if it doesn't already exist. To use the classes in the class library without qualification, add a using statement for the class library.
