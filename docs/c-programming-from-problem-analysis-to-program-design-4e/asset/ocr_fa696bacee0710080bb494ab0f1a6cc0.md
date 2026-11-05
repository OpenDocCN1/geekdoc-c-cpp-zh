**NOTE** From the Data Sources window, you can drag items (tables and/or columns) onto your form. After the items are placed on the form, you can then customize the way they are displayed. This is illustrated in the sections that follow.

When you select Add New Data Source from the Data Sources window or the PROJECT menu, you are first prompted to choose a data source type. Options of Database, Service, Object, and SharePoint are available, as shown in Figure 14-6. If you are using the Express version, your selections may look different. You will not, for example, see SharePoint, as one of the options.

![](bbox=[0.2, 0.4, 0.9, 0.77])

FIGURE 14-6 Connect to a database

As shown in Figure 14-6, selecting Database enables you to create a typed dataset object or an entity data model for the application. The typed dataset object corresponds directly to the underlying database table(s). A typed dataset defines a schema that exposes the tables and their columns as object properties. This makes manipulating the dataset much easier because you can reference the tables and columns directly by name.

When a dataset object is available for the application, the DataSet Designer tool is available to you. The DataSet Designer provides another visual representation of the objects contained in the dataset object. It enables you to set relationships between tables and add additional queries to your application. You will explore the DataSet Designer later in this chapter.