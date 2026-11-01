When you create a document-level project, you can choose to create a new document or to copy an existing document as a starting point for your development. You can also choose the type of document to create. For a Word document, for example, you can choose to create .docx (the default), .doc, or .docm documents (.docm is a macro-enabled document). The dialog box for this is shown in Figure 49-3.

![](bbox=[0.48, 0.15, 0.88, 0.48])

FIGURE 49-3

# Application-Level Add-Ins

Application-level add-ins are different from document-level customizations in that they are available throughout their targeted Office application. You can access add-in code, which might include menus, document manipulations, and so on, regardless of what documents are loaded.

When you start an Office application such as Word, it will look for associated add-ins that have entries in the registry and will load any assemblies that it needs to.

# SharePoint Workflow Templates

These projects provide a template to create SharePoint workflow applications. These are used to manage the flow of documents within SharePoint processes. By creating a project of this type, you can execute custom code at key times during the document lifecycle.

# Project Features

There are several features that you can use in the various VSTO project types, such as interactive panes and controls. The project type you use determines the features that are available to you. The following tables list these features according to the projects in which they are available.

Document-Level Customization Features

| FEATURE | DESCRIPTION |
|---|---|
| Actions pane | Actions panes are dialog boxes that are hosted inside the action pane of Word or Excel. You can display whatever controls you like here, which makes this an extremely versatile way of extending documents and applications. |
| Data cache | Data caching enables you to store data that is used in your documents externally to those documents in cached data islands. These data islands can be updated from data sources or manually, and enable the Office documents to access data when data sources are offline or unavailable. |
| Endpoints for VBA code | As discussed earlier, VSTO enables VBA interoperability. In document-level customizations, you can provide endpoint methods that can be called from VBA code. |
| Host controls | Host controls are extended wrappers around existing controls in the Office object model. You can manipulate and data-bind to these objects. |
| Smart Tags | Smart Tags are objects that are embedded in Office documents and that have typed content. They are automatically detected within the content of Office documents; for example, a stock quote Smart Tag is added automatically when the application detects appropriate text. You can create your own Smart Tag types and define operations that can be performed on them. |