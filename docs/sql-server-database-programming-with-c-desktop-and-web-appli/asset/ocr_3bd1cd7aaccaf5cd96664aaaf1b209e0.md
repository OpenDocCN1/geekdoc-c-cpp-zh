# SQL Server Database Programming with C#

![](bbox=[0.156, 0.091, 0.842, 0.423])

**FIGURE 8.21** The finished page.

Another easy way to build this Faculty page is to add an existing Faculty page Faculty.aspx that can be found from the folder Web Forms under the Students folder in the CRC Fpt site (refer to Figure 1.2 in Chapter 1). Performing the operations to add this existing Faculty page into your project:

+   1- Right-click on our project SQLSelectProject from the Solution Explorer window, and select the Add | Existing Item.
2- Browse to the folder StudentsWeb Forms on the CRC Fpt site and select three items, Faculty.aspx , Faculty.aspx.designer.cs and Faculty.aspx.cs. Then click the Add button to add them into your project. You can also download and save these pages into a temporary folder in your computer and perform this adding action.

Although we have added five buttons into this Faculty page; however, in this section we only take care of the Select and the Back buttons, exactly twos! Click methods, since we want to discuss how to retrieve the queried data from our database and display them in this Faculty page. Other buttons will be used in the following sections later.\Now let's begin to develop the codes for this Faculty page.

# 8.4.8 Develop the Codes to Select the Desired Faculty Information

First let's run the project to build the configuration Web.config to configure all controls we just added into the Faculty page. Click on the IIS Express button to run the project, enter the suitable username and password to open the Selection page. Select the Faculty Information item from this page to open the Faculty page. Click on the Close button that is located at the upper-right corner of this page to close the project.