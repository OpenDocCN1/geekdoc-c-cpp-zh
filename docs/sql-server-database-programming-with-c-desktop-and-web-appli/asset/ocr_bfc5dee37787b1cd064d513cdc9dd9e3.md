# 598 SQL Server Database Programming with C#

+   A. First the namespace System.Data is declared the DataSet class is located under that namespace and we need to use that class in this piece of codes.
B. Three class-level variables are created; the Boolean dsflag is used to hold the running status of the DataSet query method, and the instance wsDataSet is used to query data with DataSet method. The instance for wsSqlResult holds the running status of our Web methods in our service project.
C. As the project runs, each time the server performs some action, an event or a request is generated and that is sent to the database and the Server (if it is the same server). Then the Server will post back a Refresh page to the control each time it received it (IsPostBack = true). Each time the happened, the Page_Load() method will be activated and attached to the end of the combobox ComboName. To avoid duplication, we need to check the IsPostBack property of the page and add each member into the combobox only once when the project starts (IsPostBack = false). Refer to Section 8.4.9.1 in Chapter 8 for more detailed discussion about the AutoPostBack property.
D. One point is that we used a same namespace WebClientInsert we built three related files, Course.aspx, Course.aspx.designer.cs, and added them in Section 9.4.1. Thus, you do not need to prefix any other namespace for all GUI controls in the Designer View of the Course page, including the combobox ComboName. Otherwise, we need to provide a different namespace if you built Course page under a different project. Do not get confused about this namespace with our current project's name they even looked identical. The reason for this identity is that we used a project that has the same name as our current project's name to build the Course page to reduce the coding jobs by using the same namespace.
E. The first family is selected as a default and one is displayed in the combobox control ComboName as the project runs.
F. For inserting methods, Stored Procedure Method and the DataSet Method, are added into another combobox, ComboMethod, to enable users to select one of them to perform inserting action as the project runs. The first method is selected as a default.

Your finished codes for the Page_Load() method should match that is shown in Figure 9.84. The next step is to develop the codes for the Insert button's click method.

# 9.4.3.2 Develop Codes for the Insert Button Click Method

The function of this piece of codes is to insert a new record count that is stored in six textbox in the Web page as the Insert button is clicked. This piece of codes is basically identical with those in the same method on the Windows-based client project we developed in the last section. Then we can copy those codes from and paste them into our current method with a few modifications.

Open the finished client project WebClientInsert Project from the ClassDBProjects:Chapter 9:Insert from the CRC Press FTP site (refer to Figure 1.2, in Chapter I). Copy all codes from Insert button's click method and paste them into the Insert's click method in our current Web-based client project WebClientInsert Project.

The only modification is to add one String variable errMsg that is used to store the returned error information from calling different methods. In addition, all message boxes MsgBox() should be replaced by the Write() method of the Response of the server class since MsgBox() can only be used in the same client.

Your finished codes for the Insert button's click method should match that one is shown in Figure 9.85. The modification parts have been highlighted in bold.