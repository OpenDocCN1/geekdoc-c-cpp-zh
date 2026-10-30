

a long list of label styles. Access accurately creates a report design based on the label style you select. You can then open the report in Design mode and customize it as needed.

## FIGURE 20.4

rptCustomerMailingLabels, a typical mailing label report.

![](img/1e45673ab6eca9d20e67635ff5b9b318_646_0.png)

## Distinguishing between reports and forms

The main difference between reports and forms is the intended output. Whereas forms are primarily for data entry and interaction with the users, reports are for viewing data (either onscreen or in hard-copy form). Calculated fields can be used with forms to display an amount based on other fields in the record. With reports, you typically perform calculations on groups of records, a page of records, or all the records included in the report. Anything you can do with a form—except input data—can be duplicated by a report. In fact, you can save a form as a report and then refine it in the Report Design window.

## Creating a Report, from Beginning to End

The report process begins with your desire to view data, but in a way that differs from a form or datasheet display. The purpose of the report is to transform raw data into a meaningful set of information. The process of creating a report involves several steps:

- 1. Define the report layout.
- 2. Assemble the data.
- 3. Create the report with the Access Report Wizard.
- 4. Print or view the report.
- 5. Save the report.

## Defining the report layout

You should begin by having a general idea of the layout of your report. You can define the layout in your mind, on paper, or interactively using the Report Designer. When laying out a report, consider how the data should be sorted (for example, chronologically or by name), how the data should be grouped (for example, by invoice number or by week), and how the size of the paper used to print the report will constrain the data.

> NOTE
> An Access report often is expected to duplicate an existing paper report or form used by the application's consumers. In that case, the layout is already defined.

## Assembling the data

After you have a general idea of the report layout, assemble the data needed for the report. Access reports use data from two primary sources:

- ■ A single database table
- ■ A recordset produced by a query

You can join tables in a query and use the query's recordset as the record source for your report. A query's recordset appears to an Access report as if it were a single table.

As you learned in Chapter 8, you use queries to specify the fields, records, and sort order of the records stored in tables. Access treats a recordset's data as if it were a single table (for processing purposes) in datasheets, forms, and reports. When the report is run, Access matches data from the recordset or table against the bound controls specified in the report and uses the data available at that moment to produce the report.

> NOTE
> Reports don't follow the sort order specified in an underlying query. Reports are sorted at the report level. It's a waste of time to sort data in a query that is used solely to populate a report because the data is re-sorted and rearranged by the report itself.

In the following example, you use data from tblProducts to create a relatively simple tabular report.

## Creating a report with the Report Wizard

Access enables you to create virtually any type of report. Some reports, however, are easier to create than others, especially when the Report Wizard is used as a starting point. Like form wizards, the Report Wizard gives you a basic layout for your report, which you can then customize.

The Report Wizard simplifies laying out controls by stepping you through a series of questions about the report that you want to create. In this chapter, you use the Report Wizard to create tabular and columnar reports.

## Creating a new report

The Ribbon contains several commands for creating new reports for your applications. The Create tab of the Ribbon includes the Reports group, which contains several options such as Report, Labels, and Report Wizard. For this exercise, click the Report Wizard button. The first screen of the Report Wizard (shown in Figure 20.5) appears.

## FIGURE 20.5

The first screen of the Report Wizard after selecting a data source and fields.

![](img/1e45673ab6eca9d20e67635ff5b9b318_648_0.png)

In Figure 20.5, tblProducts has been selected as the data source for the new report. You can do this by selecting table tblProducts in the Navigation pane before clicking the Report Wizard button or by selecting tblProducts from the Tables/Queries drop-down list. Under the Tables/Queries drop-down list is a list of available fields. When you click a field in this list and click the right-pointing arrow, the field moves from the Available Fields list to the report's Selected Fields list. For this exercise, select Product ID, Category, Description, QtyInStock, RetailPrice, and Cost, in that order.

## Tip

Double-clicking any field in the Available Fields list adds it to the Selected Fields list. You can also double-click any field in the Selected Fields list to remove it from the box.

You're limited to selecting fields from the original record source you started with. You can select fields from other tables or queries by using the Tables/Queries drop-down list in the Report Wizard. As long as you've specified valid relationships so that Access properly links the data, these fields are added to your original selection and you use them on the report. If you choose fields from unrelated tables, a dialog box asks you to edit the relationship and join the tables. Or you can return to the Report Wizard and remove the fields.

After you've selected your data, click Next to go to the next step in the wizard.

## Selecting the grouping levels

The next dialog box enables you to choose which field(s) to use for grouping data. Figure 20.6 shows the Category field selected as the data grouping field for the report. The field selected for grouping determines how data appears on the report, and the grouping fields appear as group headers and footers in the report.

## FIGURE 20.6

Specifying the report's grouping.

![](img/1e45673ab6eca9d20e67635ff5b9b318_649_0.png)

Groups are most often used to combine data that is logically related. This example groups products by product category because users will want to see products in the same category adjacent to each other for comparison purposes. Another example is choosing to group invoice data on CustomerID so that each customer's sales history appears as a group on the report. You use CustomerID because it's a unique field and you won't get two customers grouped together. Then you can use the report's group headers and footers to display the customer name and any other information specific to each customer.

The Report Wizard lets you specify as many as four group fields for your report. You use the Priority buttons to change the grouping order on the report. The order you select for the group fields is the order of the grouping hierarchy.

Select the Category field as the grouping field and click the > button to specify a grouping based on category values. Notice that the picture changes to show Category as a grouping field, as shown in Figure 20.6. Each of the other fields (ProductID, Description, QtyInStock, RetailPrice, and Cost) selected for the report will appear in the Category group's details section.

## Defining the group data

After you select the group field(s), click the Grouping Options button at the bottom of the dialog box to display the Grouping Intervals dialog box, which enables you to further define how you want groups displayed on the report.

For example, you can choose to group by only the first character of the grouping field. This means that all records with the same first character in the grouping field are grouped. If you group a customers table on CustomerName, and then specify grouping by the first character of the CustomerName field, a group header and footer appears for all customers whose name begins with the same character. This specification groups all customer names beginning with the letter A, another group for all records with customer names beginning with B, and so on.

The Grouping Intervals drop-down displays different values for various data types:

- Text: Normal, 1st Letter, 2 Initial Letters, 3 Initial Letters, 4 Initial Letters, 5 Initial Letters
- Numeric: Normal, 10s, 50s, 100s, 500s, 1000s, 5000s, 10000s, 50000s, 100000s
- Date: Normal, Year, Quarter, Month, Week, Day, Hour, Minute

Normal means that the grouping is on the entire field. In this example, use the entire Category field.

Notice that the grouping options simplify creating reports grouped by calendar months, quarters, years, and so on. This means that you can easily produce reports showing sales, payroll, or other financial information needed for business reporting.

If you displayed the Grouping Intervals dialog box, click the OK button to return to the wizard, and then click the Next button to move to the sorting screen of the wizard.

