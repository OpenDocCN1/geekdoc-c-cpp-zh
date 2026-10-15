controls in the page. The default value of the ClientIDMode property is AutoID at page level and at the control level the default value is Inherit. If you want to define a default setting for the ClientIDMode property, so that the setting is common for all controls in all pages in an application, you can set the ClientIDMode value in the configuration file.

+   - Improving the GridView and ListView controls. In the previous versions of ASP.NET, if you select 4th item on the 2nd page and then move to the 3rd page, the 4th item in the 3rd page was also selected. This was because the row selection in a GridView or ListView control was based on the row index on the page. This problem has been solved in ASP.NET 4.0, by including a new feature known as persisted selection in the GridView and ListView control. This feature can be enabled by setting the EnablePersistedSelection property of the control to True. In addition to this, the earlier version of the ListView control required you to specify a layout template, which contained a server control with a known ID. This has been removed in the new version of ListView control, and it now more easy to work with the control.

+   - Introducing the QueryExtender control that helps in making filtering easy. In ASP.NET, filtering excludes data, which do not meet a specified criterion, from being displayed in the data source control. This requires you to use the Where clause. However, in the LinqDataSource control, the Where clause was not able to expose the full functionality. Therefore, in this version of ASP.NET, the QueryExtender control has been introduced, which provides the following advantages:

+   - Better filtering of data in comparison to using the Where clause
+   - Can be used with not only the LinqDataSource control but also with EntityDataSource control
+   - Provides multiple options to filter data, which can be used either individually or together

+   - Eliminating exceptions that used to arise in the earlier versions of ASP.NET with respect to markup code that did not conform to HTML, XHTML, or accessibility standards

# Dynamic Data

The Dynamic Data feature of ASP.NET 4.0 helps the developers in developing data-driven Web applications. It also helps in inferring the appearance and behavior of data entities retrieved from the database. Some of these enhancements are as follows:

+   - Including a Rapid Application Development (RAD) experience to help the developers in building a data-driven Web application.
+   - Defining of constraints in the data model that are used for automatic validation by the developers.
+   - Using filed templates that are a part of the Dynamic Data application to easily change the markup code generated for the GridView and DetailsView controls.

The basic purpose of the Dynamic Data feature is to enable the Dynamic Data functionality for any ASP.NET application. A new set of controls is introduced in ASP.NET to help in using the Dynamic Data feature. These controls are given as follows:

+   - The DynamicControl control
+   - The DynamicDataManager control
+   - The DynamicEntity control
+   - The DynamicFilter control
+   - The DynamicHyperLink control
+   - The DynamicValidator control

# ASP.NET Chart Control

A new control, the Chart control, has been introduced in ASP.NET 4.0 include simple charts for statistical and financial analysis. Therefore, the Chart control helps the developers to create rich and professional looking data visualization solutions. It includes a wide range of chart options, such as pie, area, range, point, circular, accumulation, data, distribution, and doughnut.

The various features included in the Chart control are as follows:

+   - Helps in data binding