

CustomerID 和 SalespersonID 字段存储来自另一张表的外键，就像子表单上的 ProductID 一样。PaymentMethod 和 TaxRate 字段则有些不同。例如，PaymentMethod 控件并不存储指向 tblPaymentType 的外键。相反，它存储文本，而 tblPaymentType 仅存储常见的付款类型。类似地，tblTaxRates 存储一些可供选择的常见税率。对于 PaymentMethod 和 TaxRate 两者，请确保将 Limit To List 属性设置为 No，以便用户可以输入适当的值。

还请注意，我们希望存储在 tblSales 表中的来自 tblTaxRates 的值来自第二列。要存储正确的值，请将 TaxRate 的 Bound Column 属性更改为 2。由于 PaymentMethod 只有一个列，而你希望为 TaxRate 显示两列，请将两个控件的 Column Widths 属性留空。当 Column Widths 为空时，Access 会显示所有列并选择最适合数据的宽度。

## 保存记录

表单行为的最后一个区域是保存记录。前面，你将 Cycle 属性设置为 Current Record，以防止用户离开最后一个字段时记录发生变化。你可以通过命令按钮控制表单的流程。要创建用于保存记录的命令按钮，请按照以下步骤操作：

- 1. **从功能区的 设计 选项卡的 控件 组中，选择 按钮 控件并将其放置在表单上。**
- 2. **在 命令按钮向导 的第一个屏幕中，选择 记录导航 和 转到下一条记录，然后单击 下一步。**
- 3. **在向导的下一个屏幕中，选中 显示所有图片 复选框并选择 保存记录 图片，然后单击 下一步。**
- 4. **在向导的最后一个屏幕中，将按钮命名为 cmdSave 并单击 完成。**

使用命令按钮转到下一条记录会自动保存当前记录。它提供的保存界面比简单地离开最后一个字段更熟悉。它还显示一条新的、空的记录以便进行更多数据输入。

你还应为用户提供取消输入发票的方式。在表单上添加另一个命令按钮，并在向导中从 记录操作 组中选择 撤消记录。选择撤消的默认图片并将按钮命名为 cmdCancel。

最后，你需要添加一个允许用户关闭表单的按钮。你将 Control Box 属性设置为 No，以便表单右上角的 X 被隐藏。添加一个使用 表单操作 类别中的 关闭表单 操作的按钮。将按钮命名为 cmdClose。

## 更改表单的外观

最后一步是让表单变得美观。在主表单上，调整控件的宽度和放置位置，并将命令按钮放置在右下角附近。在子表单中，通过将 SalesLineItemID 和 InvoiceNumber 列的右边界一直向左拖动，使其宽度为零。要拖动这些列的边界，你需要以 表单 视图查看表单。图 19.22 显示了控件的放置位置。

### FIGURE 19.22

Controls placed on a form.

![](img/1e45673ab6eca9d20e67635ff5b9b318_639_0.png)

最后，调整表单上控件的制表符顺序。单击功能区 设计 选项卡上的 制表符顺序 控件以显示制表符顺序对话框，如图 19.23 所示。设置制表符顺序后，将 InvoiceNumber 控件的 Tab Stop 属性更改为 No。发票号是 AutoNumber 字段，因此用户无需访问该字段。

### FIGURE 19.23

Setting the tab order of controls.

## Presenting Data with Access Reports

## IN THIS CHAPTER

- Looking at the different types of Access reports
- Creating reports with the Report Wizard
- Creating a report from scratch
- Improving a report's appearance

Reports provide a great way to view and print data from your database. You can display information highly summarized, with a lot of detail, or anywhere in between, and you can view or print your information in many different formats. You can add multilevel totals, statistical comparisons, and pictures and graphics to a report.

In this chapter, you learn to use the Report Wizard as a starting point. You also learn how to create reports from scratch and discover what types of reports you can create with Access.

> **ON THE WEB**
> In this chapter, you create new reports using the Report Wizard and by creating a blank report without using a wizard. You use tables created in previous chapters. The Chapter20.accdb database file on the book's website contains the completed reports described in this chapter.

## Introducing Reports

Reports present a customized view of your data. Report output is viewed onscreen or printed to provide a hard copy of the data. Very often, reports provide summaries of the information contained in the database. Data can be grouped and sorted in any order and can be used to create totals that perform statistical operations on data. Reports can include pictures and other graphics as well as memo fields. If you can think of a report you want, Access probably supports it.

## Identifying the different types of reports

Three basic types of reports are used by most businesses:

- **Tabular reports:** Print data in rows and columns with groupings and totals. Variations include summary and group/total reports.
- **Columnar reports:** Print data and can include totals and graphs.
- **Mailing label reports:** Create labels that work with a variety of manufacturers.

## Tabular reports

Tabular reports are similar to a table displaying data in rows and columns. Figure 20.1 is a typical tabular report (rptProductsSummary) displayed in Print Preview.

### FIGURE 20.1

A tabular report (rptProductsSummary) displayed in Print Preview.

![](img/1e45673ab6eca9d20e67635ff5b9b318_643_0.png)

Unlike forms or datasheets, tabular reports often group data by one or more fields. Often, tabular reports calculate and display subtotals or statistical information for numeric fields in each group. Some reports include page totals and grand totals. You can even have multiple snaked columns so that you can create directories (such as telephone books). These types of reports often use page numbers, report dates, or lines and boxes to separate information. Reports may have color and shading and display pictures, business graphs, and memo fields. A special type of summary tabular report has all the features of a detail tabular report but omits record details.

## Columnar reports

Columnar reports generally display one or more records per page, but they do so vertically. Columnar reports display data very much as a data entry form does, but they're used strictly for viewing data and not for entering it. Figure 20.2 shows part of a columnar report (rptProducts) in Print Preview.

### FIGURE 20.2

A columnar report showing report controls distributed throughout the entire page.

![](img/1e45673ab6eca9d20e67635ff5b9b318_644_0.png)

Another type of columnar report displays one main record per page (like a business form) but can show many records within embedded subreports. An invoice is a typical example. This type of report can have sections that display only one record and at the same time have sections that display multiple records from the “many” side of a one-to-many relationship—and even include totals.

Figure 20.3 shows an invoice report (rptInvoice) from the Collectible Mini Cars database system in Report view.

### FIGURE 20.3

An invoice report (rptInvoice).

![](img/1e45673ab6eca9d20e67635ff5b9b318_645_0.png)

In Figure 20.3, the information in the top portion of the report is on the “main” part of the report, whereas the product details near the bottom of the figure are contained in a subreport embedded within the main report.

## Mailing label reports

Mailing labels (shown in Figure 20.4) are also a type of report. Access includes a Label Wizard to help you create this type of report. The Label Wizard enables you to select from

