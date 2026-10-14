
## Perspective

This chapter has introduced you to the basic concepts of relational databases and described how you use SQL and ADO.NET classes to work with the data in a relational database. With that as background, you’re now ready to learn how to develop ASP.NET database applications.

In the next four chapters, then, you’ll learn how to use SQL data sources and five of the data controls to build database applications. After that, Chapter 17 will show you how to use object data sources to build 3-layer database applications. Although you don’t need to use ADO.NET directly when you use SQL data sources, you do need to use ADO.NET directly when you use object data sources.

## Terms

- Microsoft SQL Server Express
- Microsoft SQL Server 2008
- relational database
- table
- record
- row
- field
- column
- primary key
- composite primary key
- non-primary key
- unique key
- unique key constraint
- unique constraint
- index
- foreign key
- foreign key table
- primary key table
- one-to-many relationship
- one-to-one relationship
- many-to-many relationship
- linking table
- data type
- system data type
- null value
- default value
- identity column
- check constraint
- SQL dialect
- Transact-SQL
- result table
- result set
- calculated column
- join
- inner join
- ADO.NET
- ActiveX Data Objects .NET
- dataset
- data table
- .NET data provider
- data adapter
- command
- connection
- disconnected data architecture
- concurrency
- concurrency control
- optimistic concurrency
- concurrency exception
- last in wins
- data reader
- connection string

## How to use SQL data sources

In this chapter, you’ll learn how to use the SqlDataSource control, which lets you access data from a SQL Server database with little or no programming. Along the way, you’ll also learn how to use the DataList control, which lets you create lists of data.

- How to create a SQL data source .................................... 404
- A Product List application that uses two SQL data sources .................. 404
- How to create a SqlDataSource control ................................... 406
- How to define the connection ............................................ 408
- How to save the connection string in the web.config file .................. 410
- How to configure the Select statement ................................... 412
- How to create a Where clause ............................................ 414
- How select parameters work .............................................. 416
- How to use custom statements and stored procedures ........................ 418
- How to enter custom statements .......................................... 418
- How to select stored procedures ......................................... 418
- How to create a Select statement with the Query Builder ................... 420
- How to define the parameters ............................................ 422
- How to use the DataList control ......................................... 424
- How the DataList control works .......................................... 424
- How to define the templates for a data list ............................... 426
- How to format a data list ............................................... 428
- How to use data binding ................................................. 430
- How to bind a list control to a data source ............................... 430
- How to bind the controls in a template .................................. 432
- The aspx file for the Product List application ............................ 434
- How to use the advanced features of a SQL data source ..................... 436
- How to create a data source that can update the database .................. 436
- How to change the data source mode ...................................... 438
- How to use caching ...................................................... 438
- Perspective .............................................................. 440

### 3.1 RSM 和映射图

本节介绍 RSM 和映射图的相关定义和关系。映射图定义为有向图 G，每条边 E=(u,v) 带权值，表示输入与输出之间的映射关系。

RSM 是一种射线选择方法，用于从给定的输入集合中选择最优映射路径。该方法通过迭代计算权重矩阵，并在每次迭代中更新映射状态。

- RSM 算法的时间复杂度为 O(n²)
- 空间复杂度为 O(n)
- 适用于大规模映射问题

图 1 展示了 RSM 的映射过程。初始状态为输入节点集合，经过多次迭代后收敛到最终映射结果。

```c
#define N 1000
void RSM(float *in, float *out) {
    for (int i = 0; i < N; i++) {
        out[i] = in[i] * 2.0f;
    }
}
```

上述代码演示了 RSM 的核心计算逻辑。每次迭代对输入数组进行加权变换，并输出到目标数组。

> 注意：RSM 算法需要保证映射图的连通性，否则可能无法收敛到全局最优解。

| 参数 | 值 | 说明 |
|------|----|------|
| alpha | 0.5 | 学习率 |
| beta | 0.1 | 衰减因子 |
| gamma | 0.9 | 动量参数 |

### The Product List application displayed in a web browser

![](img/c024ccf88e28c30c07dd410d4342288f_424_0.png)

### Description

- The Product List application uses two SqlDataSource controls to get category and product data from a SQL Server database and display it in two bound controls.
- The drop-down list near the top of the form displays the product categories. This control is bound to the first data source control.
- The DataList control, which is bound to the second data source control, displays the data for the products that are in the category that’s selected in the drop-down list.
- This application requires no C# code in the code-behind file.

### How to create a SqlDataSource control

Figure 13-2 shows how to create a SqlDataSource control. As you will see, this process is similar to the one for creating an AccessDataSource control. To get the process started, you can drag a SqlDataSource control onto the form you’re developing.

Since a data source control isn’t displayed on the page when the application is run, it doesn’t matter where you drop this control. But it does make sense to place it near the control that it will be bound to. Once you’ve got the data source control on the form, you can use its smart tag menu to run the Configure Data Source command, which brings you to the dialog box in the next figure.

You can also create a SqlDataSource control using the Choose Data Source command in the smart tag menu of a bindable control. The exact technique for doing that varies depending on the control you’re binding. For a drop-down list, for example, you select the Choose Data Source command to start the Data Source Configuration Wizard. Then, you can choose New Data Source from the drop-down list in the first dialog box that’s displayed and click OK. That displays the dialog box shown in this figure. From this dialog box, you can select the Database icon and click OK, which drops the data source control onto the form next to the bindable control and brings you to the dialog box in the next figure.

The technique for creating a SQL data source from a DataList control is similar. The only difference is that the Choose Data Source command in the control’s smart tag menu includes a drop-down list that lets you select New Data Source. When you do that, the Data Source Configuration Wizard dialog box shown in this figure is displayed just as it is for a drop-down list.

### The starting dialog box of the Data Source Configuration Wizard

![](img/c024ccf88e28c30c07dd410d4342288f_426_0.png)

### Aspx code generated for a basic SqlDataSource control

```aspx
<asp:SqlDataSource ID="SqlDataSource1" runat="server"
    ConnectionString="<%$ ConnectionStrings:HalloweenConnectionString %>"
    SelectCommand="SELECT [CategoryID], [LongName] FROM [Categories]
        ORDER BY [LongName]">
</asp:SqlDataSource>
```

### Basic SqlDataSource control attributes

| Attribute | Description |
|---|---|
| ID | The ID for the SqlDataSource control. |
| runat | Must specify "server". |
| ConnectionString | The connection string. In most cases, you should use a <%$ expression to specify the name of a connection string saved in the web.config file (see figure 13-4). |
| ProviderName | The name of the provider used to access the database. Values can be System.Data.Odbc, System.Data.OleDb, System.Data.OracleClient, or System.Data.SqlClient. The default is System.Data.SqlClient. |
| SelectCommand | The SQL Select statement executed by the data source to retrieve data. |

### Description

- To create a SqlDataSource control, drag the control from the Data group of the Toolbox onto the form. Then, choose Configure Data Source from the control’s smart tag menu and proceed from there.
- You can also create a SQL data source using the Choose Data Source command in the smart tag menu of a bindable control. When you use this command, the dialog box shown above is displayed. Then, you can select the Database icon and proceed from there.
