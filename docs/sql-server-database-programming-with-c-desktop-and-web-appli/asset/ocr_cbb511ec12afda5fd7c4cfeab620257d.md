# SQL Server Database Programming with C#

| Type | ID | Text | TabIndex | BackColor | Font |
|---|---|---|---|---|-|
| Label | Label1 | Make Your Selection: | 0 | #E0E0E0 | Bold/Large |
| DropDown | ComboSelection | | 1 | | |
| Button | cmdSelect | Select | 2 | | Bold/Medium |
| Button | cmdExit | Exit | 3 | | Bold/Medium |

**FIGURE 8.14** Controls for the selection method may move any of the controls to any desired location on the Web page.

![](bbox=[0.248, 0.23, 0.752, 0.395])

**FIGURE 8.15** The finished selection page.

# ### 8.4.6 Develop The Codes for the Selection Page to Open The Other Page

First let's run the Selection page to build the Web configuration file. Click on the **IIS** express to run this page, and then click the **Close** button that is located on the upper-right corner of the page to close it.

Right-click on the **Selection.aspx** from the Solution Explorer and click on the **View Code** item to open the code page for the Selection Web form. First let's add a SQL Data-related namespaces on the top of this page to provide a reference to all components of the SQL Data Provider:

```
using System.Data;
using System.Data.SqlClient;
```

Then enter the codes that shown in Figure 8.16 into the **Page_load()** method to add all selection items into the combobox **ComboSelection** to allow users to make their selection as the project.

The function of this piece of coding is straightforward. Three pieces of CSE dept information are added into the combobox **ComboSelection** using the **Add()** method, and these pieces of information will be selected by the user as the project results.

Next we need to create the codes for two buttons "Select". First let's do the coding for the **Select** button. Right-click on the **Selection.aspx** from the Solution Explorer window and click on the **View Designer** item to open the Selection Web form, and then

Double-click the **Select** button to open its method. Enter the codes that are shown in Figure 8.17 into this method.

The function of this piece of coding is easy. Based on the information selected by the user, the related Web page is opened using the server's **Response** object, precisely by using the **Redirect()** method of the server's **Response** object. All of these three pages will be created and discussed in the following sections.